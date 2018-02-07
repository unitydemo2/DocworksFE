# Built-in serialization 

Some of the built-in features of Unity automatically use serialization. These are outlined below. 

See the documentation on [Script Serialization](script-Serialization) for further information.

#### Saving and loading

Unity uses serialization to load and save [Scenes](CreatingScenes), [Assets](AssetWorkflow), and [AssetBundles](AssetBundlesIntro) to and from your computer’s hard drive. This includes data saved in your own scripting API objects such as [MonoBehaviour](ScriptRef:MonoBehaviour.html) components and [ScriptableObjects](class-ScriptableObject).

This happens in the Editor’s Play Mode and Edit Mode.

#### Inspector window

When you view or change the value of a GameObject’s component field in the [Inspector window](UsingTheInspector), Unity serializes this data and then displays it in the Inspector window. The Inspector window does not communicate with the Unity Scripting API when it displays the values of a field. If you use properties in your script, any of the property getters and setters are never called when you view or change values in the Inspector windows as Unity serializes the Inspector window fields directly.

#### Reloading scripts in the Unity Editor

When you change and save a script, Unity reloads all the currently loaded script data. It first stores all serializable variables in all loaded scripts, and after loading the scripts restores them. All data that is not serializable is lost after the script is reloaded.

This affects all Editor windows, as well as all MonoBehaviours in the project. Unlike other cases of serialization in Unity, private fields are serialized by default when reloading, even if they don't have the 'SerializeField' attribute.

#### Prefabs

In the context of serialization, a [Prefab](Prefabs) is the serialized data of one or more [GameObjects](GameObjects) and [components](Components). A Prefab instance contains a reference to both the Prefab source and a list of modifications to it. The modifications are what Unity needs to do to the Prefab source to create that particular Prefab instance.

The Prefab instance only exists while you edit your project in the Unity Editor. During the project build, the Unity Editor instantiates a GameObject from its two sets of serialization data: the Prefab source and the Prefab instance’s modifications.

#### Instantiation 

When you call [Instantiate](ScriptRef:Object.Instantiate.html) on anything that exists in a [Scene](CreatingScenes), such as a [Prefab](Prefabs) or a [GameObjects](GameObjects), Unity serializes it. This happens both at runtime and in the Editor. Everything that derives from [UnityEngine.Object](ScriptRef:Object.html) can be serialized.

Unity then creates a new GameObject and deserializes the data onto the new GameObject. Next, Unity runs the same serialization code in a different variant to report which other `UnityEngine.Objects` are being referenced. It checks all referenced `UnityEngine.Objects` to see if they are part of the data being instantiated.  If the reference points to something "external", such as a Texture, Unity keeps that reference as it is. If the reference points to something "internal", such as a child GameObject, Unity patches the reference to the corresponding copy.

#### Unloading unused assets

`Resource.GarbageCollectSharedAssets()` is the native Unity garbage collector and performs a different function to the standard C# garbage collector. It runs after you load a Scene and checks for objects (like textures) that are no longer referenced and unloads them safely. The native Unity garbage collector runs the serializer in a variation in which objects report all references to external `UnityEngine.Objects`.  This is how Textures that were used by one scene are unloaded in the next.
<br/><br/>

----

<span class="page-edit">• 2017-05-15  <!-- include IncludeTextNewPageYesEdit --></span><br/>
