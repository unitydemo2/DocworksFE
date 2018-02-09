#2D and 3D Mode Settings

When creating a new project, you can specify whether to start the Unity Editor in 2D mode or 3D mode. However, you also have the option of switching the editor between 2D Mode and 3D Mode at any time. You can read more about [the difference between 2D and 3D projects here](2Dor3D). This page provides information about how to switch modes, and what exactly changes within the editor when you do.

##Switching Between 3D and 2D Modes
To change modes between 2D or 3D mode:

1. Bring up to the __Editor Settings Inspector__, via the __Edit>Project Settings>Editor__ menu. 
2. Then set  __Default Behavior Mode__ to either __2D__ or __3D__. 

You can find out more about the __Editor Settings Inspector__ on the [Editor Settings](class-EditorManager) page.

![Default Behavior Mode in the Editor Settings Inspector sets the project to 2D or 3D](../uploads/Main/BehaviorMode.png) 


##2D vs 3D Mode Settings
2D or 3D  mode determines some settings for the Unity Editor. These are listed below.

###In 2D Project Mode:
* Any images you import are assumed to be 2D images (__Sprites__) and set to __Sprite__ mode.
* The __Sprite Packer__ is enabled.
* The __Scene View__ is set to 2D.
* The default game objects do not have real time, directional light.
* The camera's default position is at 0,0,-10. (It is 0,1,-10 in 3D Mode.)
* The camera is set to be __Orthographic__. (In 3D Mode it is __Perspective__.)
* In the Lighting Window:
    * __Skybox__ is disabled for new scenes.
    * __Ambient Source__ is set to __Color__. (With the color set as a dark grey: RGB: 54, 58, 66.)
    * __Precomputed Realtime GI__ is set to off.
    * __Baked GI__ is set to off.
    * __Auto-Building__ set to off.

###In 3D Project Mode:
* Any images you import are NOT assumed to be 2D images (__Sprites__).
* The __Sprite Packer__ is disabled.
* The __Scene View__ is set to 3D.
* The default game objects have real time, directional light.
* The camera's default position is at 0,1,-10. (It is 0,0,-10. in 2D Mode.)
* The camera is set to be __Perspective__. (In 2D Mode it is __Orthographic__.)
* In the Lighting Window:
    * __Skybox__ is the built-in default __Skybox Material__.
    * __Ambient Source__ is set to __Skybox__.
    * __Precomputed Realtime GI__ is set to on.
    * __Baked GI__ is set to on.
    * __Auto-Building__ is set to on.
