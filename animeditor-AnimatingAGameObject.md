#Animating a Game Object

Once you have saved the new Animation clip Asset, you are ready to begin adding keyframes to the clip. To begin editing an Animation Clip for the selected Game Object, click on the __Animation Record button__. This will enter __Animation Record Mode__, where changes to the Game Object are recorded into the __Animation Clip__.


![Record button](../uploads/Main/AnimationEditorAnimationModeButton.png) 


You can stop the __Animation Record Mode__ at any time by clicking the __Animation Mode button__ again. This will revert the __Game Object__ to the state it was in prior to entering the Animation Mode.

The changes you make to the GameObject will be recorded as keyframes at the current time shown by the red line in the Animation Window. 

You can animate any property of the object by manipulating the object while in Animation Record Mode. Moving, Rotating or Scaling the object will add corresponding keyframes for those properties in the animation clip. Adjusting values directly in the object's inspector will also add keyframes while in Record mode. This applies to any property in the inspector, including numeric values, checkboxes, colours, and most other values.

Any animated properties of the GameObject are shown listed in the property list on the left-hand side of the Animation Window. Properties which are not animated are not shown in this window. Any new properties that you animate, including properties on child objects, are added to the property list area as soon as you start animating them.

__Transform__ properties are special in that the __.x__, __.y__, and __.z__ properties are linked, so that curves are added three at a time.

You can also add animatable properties to the current GameObject (and its children) by clicking the __Add Property__ button. Clicking this button shows a pop up list of the GameObject's animatable properties. These correspond with the properties you can see listed in the inspector.

![The animatable properties of a GameObject are revealed when you click the __Add Property__ button](../uploads/Main/AnimationEditorMatchesInspector.png) 

When in __Animation Mode__, a red vertical line will show which frame of the __Animation Clip__ is currently previewed. The __Inspector__ and __Scene View__ will show the Game Object at that frame of the Animation Clip. The values of the animated properties at that frame are also shown in a column to the right of the property names.

In Animation Mode a red vertical line shows the currently previewed frame.

![Current frame](../uploads/Main/AnimationEditorPreviewFrame.png) 

###Time Line
You can click anywhere on the __Time Line__ to preview or modify that frame in the Animation Clip. The numbers in the __Time Line__ are shown as seconds and frames, so 1:30 means 1 second and 30 frames.

![Time Line](../uploads/Main/AnimationEditorTimeLine.png) 


###Animation Mode

In __Animation Mode__ you can move, rotate, or scale the __Game Object__ in the __Scene View__. This will automatically create __Animation Curves__ for the position, rotation, and scale properties of the __Animation Clip__ if they didn't already exist, and keys on those Animation Curves will automatically be created at the currently previewed frame to store the respective __Transform__ values you changed.

You can also use the __Inspector__ to modify any of the other animatable properties of the __Game Object__. This too will create __Animation Curves__ as needed, and create __keys__ on those Animation Curves at the currently previewed frame to store your changed values.


###Keyframe Creation

You can manually create a __keyframe__ using the __Add Keyframe button__. This will create a key for all the properties that are currently selected in the __Animation View__. This is useful for selectively adding keys to specific properties only.

![The Add Keyframe Button](../uploads/Main/AnimationEditorKeyframeButton.png) 

