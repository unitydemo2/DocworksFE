#Time Manager

The __Time Manager__ (menu: __Edit &gt; Project Settings &gt; Time__) lets you set a number of properties that control timing within your game.

![](../uploads/Main/TimeSet.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Fixed Timestep__ |A framerate-independent interval that dictates when physics calculations and __FixedUpdate()__ events are performed. |
|__Maximum Allowed Timestep__ |A framerate-independent interval that caps the worst case scenario when frame-rate is low. Physics calculations and __FixedUpdate()__ events will not be performed for longer time than specified. |
|__Time Scale__ |The speed at which time progresses. Change this value to simulate bullet-time effects. A value of 1 means real-time. A value of .5 means half speed; a value of 2 is double speed. |

##Details

The Time Manager lets you set properties globally but it is often useful to set them from a script during gameplay (for example, setting _Time Scale_ to zero is a useful way to pause the game). See the page on [Time and Framerate Management](TimeFrameManagement) for full details of how time can be managed in Unity.