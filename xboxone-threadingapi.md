Threading
=========

Much of the XDK API requires asynchronous callbacks that will be invoked on separate threads.  Unity handles this asynchronous behavior in the core of Unity and within the [plugins](xboxone-plugins).  If you use your own threads or implement your own code that uses asynchronous XDK calls, you must be careful with threading hazards with Unity objects.  Accessing GameObjects and other Unity classes is not thread safe, and you must avoid doing so on worker threads.

Unity Event Queue
-----------------

The __Unity Event Queue__ (__UEQ__) is a new feature that provides a way to send events and messages between different systems in your code.  Events can be queued up from any number of threads, and they will be processed on Unity's main thread.  This can be used in your own native plugins to facilitate communication between code systems, plugins, or to make sure a callback is processed on Unity's main thread where it is safe to access Unity classes.

If you look at the source for the [plugins](xboxone-plugins),you will find a file named _UnityEventQueue.h_. This has code that you can use to utilize the __UEQ__ from your native plugins. There is no way to directly use the __UEQ__ in your game's scripts. The following details will use pieces from that header to explain how the __UEQ__ works. The [plugins](xboxone-plugins) also serve as a great guide to using events effectively.

_Keep in mind that the following code is C++ code, not C# code._


IEventQueue
-----------

The __IEventQueue__ interface provides access to the __UEQ__.  This is not an interface that is meant to be inherited from.  You can get a reference to the __UEQ__ through the __UnitySetEventQueue__ function.


````
class IEventQueue
 {
 public:
 	template<typename T>
 	void SendEvent(T & payload);
 
 	virtual void AddHandler(EventHandler * handler);
 	virtual bool RemoveHandler(EventHandler * handler);
 };
````

###SendEvent
Adds an event to the __UEQ__.  This can be called from any thread.  The event type must be registered and adhere to the guidelines described in **Events**.

###AddHandler
Adds a handler so it will process events.  This must be called on Unity's main thread.  If you must add a handler on a worker thread, you can use the __AddEventHandler__ event.  It is not necessary to add your own handler for the __AddEventHandler__ event.

###RemoveHandler
Removes a handler so it will no longer process events.  This must be called on Unity's main thread.  If you must add a handler on a worker thread, you can use the __AddEventHandler__ event.  It is not necessary to add your own handler for the __AddEventHandler__ event.

Events
------

Events are payloads that let you communicate with other systems.  The event can be an empty struct that simply acts as a notification that something has happened, or it can carry information along with it.  When the __UEQ__ is processed, the event is given to an __EventHandler__.

````
struct SimpleEvent
{
	SimpleEvent() {}
};
REGISTER_EVENT_ID(<<something unique>>,<<something else unique>>,SimpleEvent)
````
###__REGISTER_EVENT_ID__
This is a macro that lets the __UEQ__ know how to use your event by providing the information needed to associate your event with __EventHandlers__.  The first two parameters should be two separate, unique values.  The values must be literal unsigned 64-bit values (IE: use the "ULL" suffix).  These values separate an event from all other events, even others used by Unity or other plugins.  If you use a value that is shared with another event, __EventHandlers__ will receive multiple event types.
###Event Type Guidelines
There are a few rules you must follow when creating an event's type.

* Events must be POD types.  Constructors and destructors will not be called, ergo events cannot be used to handle allocations or reference counted resources.
* The __UEQ__ is a finite size, and because of this it is advised that you keep your events small.  Any event that is more than 512 bytes in size will result in undefined behavior.


EventHandler
------------

An __EventHandler__ takes care of processing events.  It is stored in the __UEQ__ and handed the event that the handler is associated with.  There can be multiple handlers for a single event.  It is also possible to have a handler process multiple events, and this is best done by using the __ClassBasedEventHandler__ or the __StaticFunctionEventHandler__.  

The __UEQ__ processes all queued events each frame.  This normally occurs at the end of the frame, but this is guaranteed.  To prevent deadlocks, the queue may be processed immediately when it becomes full.  Because of this, your handler should not expect to be invoked at a certain point within your games frame.

````
class EventHandler
{
public:
	virtual void HandleEvent ( EventId & id, void * data );
	virtual EventId HandlerEventId();
};
````

###HandleEvent
This is where you will add logic to process the event.  When the desired event type is found in the __UEQ__, __HandleEvent__ will be called on Unity's main thread.  It will be given the EventId along with the event.  The event must be cast back to the appropriate type.  

EventHandler Utilities
----------------------

There are a few utilities available that help create new handlers or adapt existing code to use events.

###__ClassBasedEventHandler__
This class template implements the boiler plate code needed to have an __EventHandler__ and forwards processing to a type you specify.  This can be a useful tool if you want to make an existing class an __EventHandler__.

````
template< typename EVENTTYPE, typename OBJECTTYPE >
 class ClassBasedEventHandler : public EventHandler 
 {
 	ClassBasedEventHandler( OBJECTTYPE * handler = NULL );
 
 	ClassBasedEventHandler<EVENTTYPE,OBJECTTYPE> * 
 		SetObject( OBJECTTYPE * handler );
 };
````
__EVENTTYPE__ is the type of your event object, and __OBJECTTYPE__ is the type of your underlying handler object.  Create a __ClassBasedEventHandler__ instance with a proper underlying handler object, and pass the __ClassBasedEventHandler__ instance to the __IEventQueue-&gt;AddHandler__ function.

The underlying handler object must provide a __HandleEvent__ function like the standard __Handler__, but there are notable differences in the function signature.  It need not be virtual, the EventId is not passed as a parameter, and the event parameter is typed as a reference to the event type rather than a **void ***.  Because the event parameter is typed more strongly than with the __EventHandler__ class, you can use the __ClassBasedEventHandler__ along with function overloading to make the same class handle multiple events.

````
class SomeClass
{
public:
	void HandleEvent ( SpecificEvent & data ) { }
};
````


###__StaticFunctionEventHandler__
This class template implements the boiler plate code needed to have an __EventHandler__ and forwards processing to a static function that you specify.  This can be a useful tool if you want to make an existing function an __EventHandler__.

````
template< typename EVENTTYPE >
 class StaticFunctionEventHandler : public EventHandler
 {
 public:
 	typedef void (*HandlerFunction)(const EVENTTYPE & payload);
 
 	StaticFunctionEventHandler( HandlerFunction handlerCallback );
 };
````
__EVENTTYPE__ is the type of your event object.  Create a __ClassBasedEventHandler__ instance with proper handling function, and pass the __ClassBasedEventHandler__ instance to the __IEventQueue::AddHandler__ function.

Your function must have the same signature as the __StaticFunctionEventHandler::HandlerFunction__ typedef. Because the event parameter is typed more strongly than with the __EventHandler__ class, you can use the __StaticFunctionEventHandler__ along with function overloading to use several functions of the same name handle different events.
  
###__AddEventHandler__ Event
This event can be used to safely add a new event handler from a worker thread.  Create an instance of this event and set it with the correct __EventHandler__, then pass it to __IEventQueue::SendEvent__ function.

````
struct AddEventHandler
{
	AddEventHandler( EventHandler * handler ) : m_Handler(handler) {}
	EventHandler * m_Handler;
};
````

###__RemoveEventHandler__ Event
This event can be used to safely remove an existing event handler from a worker thread.  Create an instance of this event and set it with the correct __EventHandler__, then pass it to __IEventQueue::SendEvent__ function.

````
struct RemoveEventHandler
{
	RemoveEventHandler( EventHandler * handler ) : m_Handler(handler) {}
	EventHandler * m_Handler;
};
````


UnitySetEventQueue
------------------

To get a proper reference to the __UEQ__, a native plugin must export a function named _UnitySetEventQueue_.  This function will get called by Unity when the plugin is loaded.  It must have the function signature shown below.  It takes in one parameter which will be a pointer to the __UEQ__.  


````
UnityEventQueue::IEventQueue * g_internalQueue;
DLL_EXPORT void UnitySetEventQueue(void * queue)
{
  internalQueue = (UnityEventQueue::IEventQueue*)queue;
 
}
````