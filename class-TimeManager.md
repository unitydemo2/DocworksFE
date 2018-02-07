#Time Manager

The __Time Manager__ (menu: __Edit &gt; Project Settings &gt; Time__) lets you set a number of properties that control timing within your game.

![](../uploads/Main/TimeSet.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Fixed Timestep__ |A framerate-independent interval that dictates when physics calculations and __FixedUpdate()__ events are performed. |
|__Maximum Allowed Timestep__ |A framerate-independent interval that caps the worst case scenario when frame-rate is low. Physics calculations and __FixedUpdate()__ events will not be performed for longer time than specified. |
|__Time Scale__ |The speed at which time progresses. Change this value to simulate bullet-time effects. A value of 1 means real-time. A value of .5 means half speed; a value of 2 is double speed. |
|__Maximum Particle Timestep__ | A framerate-independent interval that controls the accuracy of the particle simulation. When the frame time exceeds this value, multiple iterations of the particle update are performed in one frame, so that the duration of each step does not exceed this value. For example, a game running at 30fps (0.03 seconds per frame) could run the particle update at 60fps (in steps of 0.0167 seconds) to achieve a more accurate simulation, at the expense of performance. |

##Details

The Time Manager lets you set properties globally, but it is often useful to set them from a script during gameplay (for example, setting _Time Scale_ to zero is a useful way to pause the game). See the page on [Time and Framerate Management](TimeFrameManagement) for full details of how time can be managed in Unity.

---

<span class="page-edit"> 2017-05-18  <!-- include IncludeTextNewPageSomeEdit --></span>

<span class="page-history">__Maximum Particle Timestep__ added in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>