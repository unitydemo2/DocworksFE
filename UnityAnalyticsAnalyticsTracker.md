Analytics Tracker Component
=============

The Analytics API automatically sends events to the Analytics Service under certain circumstances. However, custom events can also be sent using user-defined triggers. These can be configured and implemented entirely in the Editor as well as from script.

Attach an Analytics Tracker component to any GameObject to send a custom event via the Analytics API.


![Analytics Tracker Component](../uploads/Main/analyticsTrackerScript.png)



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Event Name__|Set a name for the custom event.|
|__Trigger__|Specify the immediate cause of the event being sent. See notes on Triggers below for more information.|
|__Parameters__|Set a list of keys/values. Parameter data can be either static, where you specify set strings to send as the parameter data, or it can be arbitrary fields of arbitrary components attached to a provided GameObject. See notes on Parameters below for more information.|

## Triggers

The __Trigger__ specifies the immediate cause of the event being sent.


![Anayltics Tracker Trigger](../uploads/Main/analyticsTrackerScriptExternal.png.png)


### External events

An event can leverage most standard methods in the MonoBehaviour life cycle, but it can also be triggered from an external source. For example, the __External__ event trigger can be tied (entirely through the Editor) to a UI Button component’s click event:


![Analytics Tracker External Events](../uploads/Main/ButtonScript.png)


In this example, a GameObject called __MyAnalyticsTracker__ has an Analytics Tracker component with its __Trigger__ type set to __External__. This button component can trigger the event by invoking __AnalyticsTracker.TriggerEvent__ in its __OnClick__ event.

## Parameters

Use this field to set a list of keys/values. Parameter data can be either __static__, where you specify set strings to send as the parameter data, or arbitrary fields of arbitrary components attached to a provided GameObject.

### Static parameters


![Static Parameters](../uploads/Main/staticparameters.png)


Here, the parameter is marked as __Static__. In this example, the key is named "name" and the value is named “value”. You can change these to whatever you like. The data sent with the event for this parameter will always be the same.

### Non-static parameters


![Non-Static Parameters](../uploads/Main/nonstaticanalytics.png)


This image shows a list of parameters registered as event data. The value is set to the __boolParameter__ field of the user-defined class __TestAnalyticsDataObject__, and attached to a GameObject named __ExampleGameObject__. The event contains the contents of this field at the time when the event is sent. This could be set to any public field that resolves to a string, number or boolean.


