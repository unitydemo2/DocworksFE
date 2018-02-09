Animation
=========

This is the **Legacy** Animation component, which was used on Game Objects for animation purposes prior to the introduction of Unity's current animation system.

This component is retain in Unity for backwards-compatibility only. For new projects, please use the [Animator component](class-Animator).

![The Animation Inspector](../uploads/Main/AnimationInspector35.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Animation__ |The default animation that will be played when Play Automatically is enabled. |
|__Animations__ |A list of animations that can be accessed from scripts. |
|__Play Automatically__ |Should the animation be played automatically when starting the game? |
|__Animate Physics__ |Should the animation interact with physics? |
|__Culling Type__|Determines when the animation will not be played.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Always Animate__|Always animate.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based on Renderers__|Cull based on the default animation pose.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based on Clip Bounds__|Cull based on clip bounds (calculated during import), if the clip bounds are out of view, the animation will not be played.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based on User Bounds__|Cull based on bounds defined by the user, if the user-defined bounds are out of view, the animation will not be played.|

See the [Animation View Guide](AnimationEditorGuide) for more information on how to create animations inside Unity. See the [Animation Import](AssetPreparationandImport) page on how to import animated characters.
