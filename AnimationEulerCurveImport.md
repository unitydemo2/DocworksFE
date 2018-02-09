#Euler Curve Import

Rotations in 3D applications are usually represented in one of two ways, Quaternions or Euler angles. For the most part, Unity uses Quaternions as its internal representation of rotations, however it's important to have a basic understanding of [rotation and orientation in Unity](QuaternionAndEulerRotationsInUnity).

When importing animation from external sources, these files usually contain keyframe animation in Euler format. Unity's default behavior is to resample these animations as Quaternion values and generate a new Quaternion keyframe for every frame in the animation, in an attempt to minimise any perceivable difference between the source animation and how it appears in Unity. 

There are still some situations where - even with resampling - the quaternion representation of the imported animation may not match the original closely enough, For this reason, in Unity 5.3 and onwards there is the option to turn off animation resampling, so that you can instead use the original Euler animation keyframes at runtime.

## Using Euler Curve Support on Imported Animations

To enable support for using the original Euler Curve values in an animation file, you must turn ***off** the "Resample Curves" option in the Animations Import Inspector:

![The Resample Curves option in the Animations Import Inspector](../uploads/Main/AnimationImportResampleRotations.png)

With this option enabled, rotations will be resampled to quaternions. This is the default behavior.
When disabled, rotation curves will not be resampled, and the rotation curve will be imported with its original keyframes, in Euler or quaternion mode as appropriate for the curve type. **Note: Any rotation curve on a joint that has pre- or post-rotations will be automatically resampled by the FBX SDK, and will automatically be imported as quaternion curves.**

To support a maximum variety of imported files, and for maximum fidelity, Unity supports all normal (non-repeating) euler rotation orders, and curves will be imported in their original rotation orders.

*The primary reason for disabling rotation resampling and using the original euler curves is when the default quaternion interpolation between frames gives faulty results, and causes issues.*

## The Results During Animation Playback
When using non-resampled rotations, there should be very little visual difference in the playback of animations. Under the hood though, rotation curves that have been imported in Euler representation will always be kept so, even at runtime. 

Since the engine functions with quaternions, rotation values have to be converted to quaternion at some point. Before Unity 5.3, this conversion always happened at import. In 5.3, when the Resample Curves option is switched off in the Animation Import inspector, the rotation values are kept as euler values up until they are applied to a Gameobject. This means that the end result should be as good as - or better than - before. 

Memory wise, for rotation curves that have not been baked in the authoring software, there should be a net gain for rotation curves.

## Non-Default Euler Orders in the Transform Inspector

The Euler angles used in Unity's transform inspector are applied in the default order of Z,X,Y. 

When playing back or editing imported animations that feature Euler curves with a rotation order different from Unity’s default, an indication of the current rotation order will be shown next to the rotation fields.

![The inspector showing that a non-default rotation order is being used for the rotation animation on this object](../uploads/Main/AnimationEulerAlternateRotationOrderInInspector.png)

When editing multiple transforms with differing rotation orders, a warning will be shown to the users to warn them that the same Euler rotation applied will give different results on curves with different rotation orders.

![The inspector showing that a mixture of rotation orders are being used for the rotation animation on the selected group of objects](../uploads/Main/AnimationEulerMixedRotationOrderInInspector.png)

