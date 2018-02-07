# Script Serialization

Serialization is the automatic process of transforming data structures or object states into a format that Unity can store and reconstruct later. Some of Unity’s built-in features use serialization; features such as saving and loading, the Inspector window, instantiation, and Prefabs. See documentation on [Built-in serialization use](script-Serialization-BuiltInUse) for background details on all of these.

How you organise data in your Unity project affects how Unity serializes that data and can have a significant impact on the performance of your project. Below is some guidance on serialization in Unity and how to optimize your project for it.

See also documentation on: [Serialization Errors](script-Serialization-Errors), [Custom Serlialization](script-Serialization-Custom), and [Built-in Serialization](script-Serialization-BuiltInUse).

## Understanding hot reloading

### Hot reloading

Hot reloading is the process of creating or editing scripts while the Editor is open and applying the script behaviors immediately. You do not have to restart the game or Editor for changes to take effect.

When you change and save a script, Unity hot reloads all the currently loaded script data. It first stores all serializable variables in all loaded scripts and, after loading the scripts, it restores them. All data that is not serializable is lost after a hot reload.

### Saving and loading 

Unity uses serialization to  load and save [Scenes](CreatingScenes), [Assets](AssetWorkflow), and [AssetBundles](AssetBundlesIntro) to and from your computer’s hard drive. This includes data saved in your own scripting API objects such as [MonoBehaviour](ScriptRef:MonoBehaviour.html) components and [ScriptableObjects](class-ScriptableObject).

Many of the features in the Unity Editor build on top of the core serialization system. Two things to be particularly aware of with serialization are the [Inspector window](UsingTheInspector), and hot reloading.

### The Inspector window

When you view or change the value of a GameObject’s component field in the [Inspector window](UsingTheInspector), Unity serializes this data and then displays it in the Inspector window. The Inspector window does not communicate with the Unity Scripting API when it displays the values of a field. 

If you use properties in your script, any of the property getters and setters are never called when you view or change values in the Inspector windows as Unity serializes the Inspector window fields directly. This means that: While the values of a field in the Inspector window represent script properties, changes to values in the Inspector window do not call any property getters and setters in your script

## Serialization rules

Serializers in Unity run in a real-time game environment. This has a significant impact on performance. As such, serialization in Unity behaves differently to serialization in other programming environments. Outlined below are a number of tips on how to use serialization in Unity.

<a name="FieldSerliaized1"></a>
#### How to ensure a field in a script is serialized

Ensure it:

* Is `public`, or has a [SerializeField](ScriptRef:SerializeField.html) attribute

* Is not  `static`

* Is not  `const`

* Is not  `readonly`

* Has a  `fieldtype` that can be serialized <br/> (See [Simple field types that can be serialized](#FieldSerliaized2), below.)


<a name="FieldSerliaized2"></a>
#### Simple field types that can be serialized

* Custom non-abstract, non-generic classes with the `Serializable` attribute <br/>(See [How to ensure a custom class can be serialized](#ClassSerialized), below.)

* Custom structs with the `Serializable` attribute

* References to objects that derive from [UnityEngine.Object](ScriptRef:Object.html)

* Primitive data types (`int`, `float`, `double`, `bool`, `string`, etc.)

* Enum types

* Certain Unity built-in types: `Vector2`, `Vector3`, `Vector4`, `Rect`, `Quaternion`, `Matrix4x4`, `Color`, `Color32`, `LayerMask`, `AnimationCurve`, `Gradient`, `RectOffset`, `GUIStyle`

#### Container field types that can be serialized

* An array of a simple field type that can be serialized

* A `List<T>` of a simple field type that can be serialized

**Note**: Unity does not support serialization of multilevel types (multidimensional arrays, jagged arrays, and nested container types). <br/>If you want to serialize these, you have two options: wrap the nested type in a class or struct, or use serialization callbacks [ISerializationCallbackReceiver](ScriptRef:ISerializationCallbackReceiver.html) to perform custom serialization. For more information, see documentation on [Custom Serialization](script-Serialization-Custom).

<a name="ClassSerialized"></a>
#### How to ensure a custom class can be serialized

Ensure it:

* Has the [Serializable](ScriptRef:Serializable.html) attribute

* Is not abstract

* Is not static

* Is not generic, though it may inherit from a generic class

To ensure the fields of a custom class or struct are serialized, see [How to ensure a field in a script is serialized](#FieldSerliaized1), above.
<br/><br/>
### When might the serializer behave unexpectedly?

#### Custom classes behave like structs

With custom classes that are not derived from [UnityEngine.Object](ScriptRef:Object.html) Unity serializes them inline by value, similar to the way it serializes structs. If you store a reference to an instance of a custom class in several different fields, they become separate objects when serialized. Then, when Unity deserializes the fields, they contain different distinct objects with identical data.

When you need to serialize a complex object graph with references, do not let Unity automatically serialize the objects. Instead, use `ISerializationCallbackReceiver` to serialize them manually. This prevents Unity from creating multiple objects from object references. For more information, see documentation on [ISerializationCallbackReceiver](ScriptRef:ISerializationCallbackReceiver.html).

This is only true for custom classes. Unity serializes custom classes "inline" because their data becomes part of the complete serialization data for the [MonoBehaviour](ScriptRef:MonoBehaviour.html) or [ScriptableObject](ScriptRef:ScriptableObject.html) they are used in. When fields reference something that is a [UnityEngine.Object](ScriptRef:Object.html)-derived class, such as `public Camera myCamera`, Unity serializes an actual reference to the camera `UnityEngine.Object`. The same occurs in instances of scripts if they are derived from `MonoBehaviour` or `ScriptableObject`, which are both derived from `UnityEngine.Object`.

#### No support for `null` for custom classes

Consider how many allocations are made when deserializing a `MonoBehaviour` that uses the following script.

````
class Test : MonoBehaviour
{
    public Trouble t;
}
[Serializable]
class Trouble
{
   public Trouble t1;
   public Trouble t2;
   public Trouble t3;
}
````

It wouldn’t be strange to expect one allocation: That of the `Test` object. It also wouldn’t be strange to expect two allocations: One for the `Test` object and one for a `Trouble` object. 

However, Unity actually makes more than a thousand allocations. The serializer does not support null. If it serializes an object, and a field is null, Unity instantiates a new object of that type, and serializes that. Obviously this could lead to infinite cycles, so there is a depth limit of seven levels. At that point Unity stops serializing fields that have types of custom classes, structs, lists, or arrays.

Since so many of Unity's subsystems build on top of the serialization system, this unexpectedly large serialization stream for the `Test MonoBehaviour` causes all these subsystems to perform more slowly than necessary.  

#### No support for polymorphism

If you have a `public Animal[] animals` and you put in an instance of a `Dog`, a `Cat` and a `Giraffe`, after serialization, you have three instances of `Animal`.

One way to deal with this limitation is to realize that it only applies to custom classes, which get serialized inline. References to other `UnityEngine.Objects` get serialized as actual references, and for those, polymorphism does actually work.  You would make a `ScriptableObject` derived class or another `MonoBehaviour` derived class, and reference that. The downside of this is that you need to store that `Monobehaviour` or scriptable object somewhere, and that you cannot serialize it inline efficiently.

The reason for these limitations is that one of the core foundations of the serialization system is that the layout of the datastream for an object is known ahead of time; it depends on the types of the fields of the class, rather than what happens to be stored inside the fields.

### Tips 

#### Optimal use of serialization

You can organise your data to ensure you get optimal use from Unity’s serialization.

* Organise your data with the aim to have Unity serialize the smallest possible set of data. The primary purpose of this is not to save space on your computer’s hard drive, but to make sure that you can maintain backwards compatibility with previous versions of the project. Backwards compatibility can become more difficult later on in development if you work with large sets of serialized data.

* Organise your data to never have Unity serialize duplicate data or cached data. This causes significant problems for backwards compatibility: It carries a high risk of error because it is too easy for data to get out of sync.

* Avoid nested, recursive structures where you reference other classes.The layout of a serialized structure always needs to be the same; independent of the data and only dependent on what is exposed in the script. The only way to reference other objects is through classes derived from [UnityEngine.Object](ScriptRef:Object.html). These classes are completely separate; they only reference each other and they don't embed the contents.

#### Making Editor code hot reloadable

When reloading scripts, Unity serializes and stores all variables in all loaded scripts. After reloading the scripts, Unity then restores them to their original, pre-serialization values.

When reloading scripts, Unity restores all variables - including private variables - that fulfill the requirements for serialization, even if a variable has no [SerializeField](ScriptRef:SerializeField.html) attribute. In some cases, you specifically need to prevent private variables from being restored: For example, if you want a reference to be null after reloading from scripts. In this case, use the [NonSerializable](ScriptRef:NonSerializable.html) attribute.

Unity never restores static variables, so do not use static variables for states that you need to keep after reloading a script.
<br/><br/>

----

<span class="page-edit">• 2017-05-15  <!-- include IncludeTextAmendPageYesEdit --></span><br/>
