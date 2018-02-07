Attach Game Script
============================

The __UnityAnalyticsIntegration__ script can be attached to any [GameObject](GameObjects) in any [Scene](CreatingScenes) in your game to initialize the Unity Analytics SDK. We recommend you attach the script to a __GameObject__ in the first __Scene__ of your game to ensure you begin capturing as much user engagement data as possible. 

In this example, we will attach the script to __MainCamera__.
First, locate and select "Main Camera" in the __Hierarchy__ tab on the left hand side of the Editor.

![](../uploads/Main/AnalyticsBasicAttachGameScript.gif)

Drag your script from the Projects tab and drop it on the Main Camera __GameObject__. In the __Inspector__ window, with Main Camera selected, you should see that the script was assigned to the Main Camera as a Component.

Note: You can also add a script to a __GameObject__ by selecting the __GameObject__ in your __Hierarchy__ and adding the desired script Component to it in the __Inspector__.
