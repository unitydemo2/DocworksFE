Event System
=================

The Event System is a way of sending events to objects in the application based on input, be it keyboard, mouse, touch, or custom input. The Event System consists of a few components that work together to send events.

Overview
----------------------------------
When you add an Event System component to a GameObject you will notice that it does not have much functionality exposed, this is because the Event System itself is designed as a manager and facilitator of communication between Event System modules. 

The primary roles of the Event System are as follows:

- Manage which GameObject is considered selected
- Manage which Input Module is in use
- Manage Raycasting (if required)
- Updating all Input Modules as required

Input Modules
----------------------
An input module is where the main logic of how you want the Event System to behave lives, they are used for

- Handling Input
- Managing event state
- Sending events to scene objects.

Only one Input Module can be active in the Event System at a time, and they must be components on the same GameObject as the Event System component.

If you wish to write a custom input module it is recommended that you send events supported by existing UI components in Unity, but you are also able to extend and write your own events as detailed in the Messaging System documentation.

Raycasters
---------------
Raycasters are used for figuring out what the pointer is over. It is common for Input Modules to use the Raycasters configured in the scene to calculate what the pointing device is over. 

There are 3 provided Raycasters that exist by default:


- Graphic Raycaster - Used for UI elements
- Physics 2D Raycaster - Used for 2D physics elements
- Physics Raycaster - Used for 3D physics elements

If you have a 2d / 3d Raycaster configured in your scene it is easily possible to have non UI elements receive messages from the Input Module. Simply attach a script that implements one of the event interfaces.