##Animation in Unity 5.0

These are notes to be aware of when upgrading projects from Unity 4 to Unity 5, if your project uses animation features.

###Asset Creation API

In 5.0 we introduced an API that allows you to build and edit Mecanim assets in the editor. For users that have previously used the unsupported API (in UnityEditorInternal namespace) you will need to manually update your scripts to use the new API.

Here is a short list of the most encountered type changes : 

|**_Previous:_** |**_New:_** |
|:---|:---|:---|
|UnityEditorInternal.BlendTree |UnityEditor.Animations.BlendTree |
|UnityEditorInternal.AnimatorController |UnityEditor.Animations.AnimatorController |
|UnityEditorInternal.StateMachine |UnityEditor.Animations.AnimatorStateMachine |
|UnityEditorInternal.State |UnityEditor.Animations.AnimatorState |
|UnityEditorInternal.AnimatorControllerLayer |UnityEditor.Animations.AnimatorControllerLayer |
|UnityEditorInternal.AnimatorControllerParameter |UnityEditor.Animations.AnimatorControllerParameter |

Also note that most accessor functions have been changed to arrays:

````
UnityEditorInternal.AnimatorControllerLayer layer = animatorController.GetLayer(index);
````
becomes:

````
UnityEditor.Animations.AnimatorControllerLayer layer = animatorController.layers[index];
````

 

A basic example of API usage is given at the end of this blog post: [http://blogs.unity3d.com/2014/06/26/shiny-new-animation-features-in-unity-5-0/](http://blogs.unity3d.com/2014/06/26/shiny-new-animation-features-in-unity-5-0/
)

For more details refer the the Scripting API documentation.