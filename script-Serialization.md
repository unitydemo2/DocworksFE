Script Serialization
=================

Serialization is a central feature in Unity.

In the Unity Engine, serialization is used to load Scenes, Assets, and AssetBundles from disk. This includes data saved in your own script objects such as `MonoBehaviour` components and `ScriptableObjects`.

Additionally, many of the features in the Unity Editor build on top of the core serialization system.

##Built-in features that use serialization
To give you an understanding of how serialization works in Unity, the following sections provide a list of the built-in features of Unity that use serialization.

####MonoBehaviour and ScriptableObject
Data saved in script objects in the form of `MonoBehaviour` components and `ScriptableObjects` are saved and loaded using serialization. This happen at runtime when running your game, but also at many other points in time, as is detailed below.

####Inspector window
The Inspector window doesn’t communicate with the C# API to know the values of a property that it is inspecting. It asks the object to serialize itself, and then displays this serialized data.

####Prefabs
Internally, a Prefab is the serialized data stream of one (or more) GameObjects and components. A Prefab instance is a list of modifications that should be made on the serialized data for this instance. The concept Prefab only exists during project editing in the Unity Editor; the Prefab modifications get backed into a normal serialization stream when the Unity Editor makes a build, and when GameObjects are instantiated in the build, there is no reference to these GameObjects being Prefabs.

####Instantiation 
When you call `Instantiate()` on anything that exists in a Scene, such as a Prefab or a GameObject, Unity serializes the object. This happens both at runtime and in the Editor. Note that everything that derives from `UnityEngine.Object` can be serialized.

Unity then creates a new GameObject and deserializes (that is, loads) the data onto the new GameObject. Next, Unity runs the same serialization code in a different variant to report which other `UnityEngine.Objects` are being referenced. It checks all referenced `UnityEngine.Objects` to see if they are part of the data being `Instantiated()`.  If the reference points to something "external", such as a Texture, Unity keeps that reference as it is. If the reference points to something "internal", such as a child GameObject, Unity patches the reference to the corresponding copy.

####Saving 
If you open a `.unity` Scene file with a text editor, and have set the Unity Editor to __force text serialization__, it runs the serializer with a yaml backend. See  [www.yaml.org ](http://www.yaml.org) for further information.

####Loading
Backwards-compatible loading is built on top of serialization. In-Editor yaml loading, as well as the run-time loading of Scenes, Assets, and AssetBundles, all use the serialization system.

####Hot reloading in the Unity Editor
When you change and save a Unity script, Unity serializes all managed representations of objects that derive from `UnityEngine.Object`. This includes (among other things) all Editor windows, as well as all MonoBehaviours in the project. Unity then destroys all these objects, unloads the old C# code, loads the new C# code, recreates the objects, and then deserializes the data streams of the objects back onto the new objects.

If a hot reload happens while the Editor is in Play mode, all states that are not serializable are lost. Note that unlike other cases of serialization in Unity, private fields are serialized by default when hot reloading, even if they don't have the 'SerializeField' attribute.

####Resource.GarbageCollectSharedAssets()
`Resource.GarbageCollectSharedAssets()` is the native Unity garbage collector. Note that it has a different function to the C# garbage collector. It runs after you load a Scene, to ensure that objects from the previous Scene are no longer referenced, and so can be unloaded. The native Unity garbage collector runs the serializer in a variation in which objects report all references to external `UnityEngine.Objects`.  This is how Textures that were used by Scene1 are unloaded in Scene2.

The serialization system is written in C++. It is used for all internal object types, such as Textures, AnimationClips, and Cameras, among others. Serialization happens at the `UnityEngine.Object` level. Each `UnityEngine.Object` is always serialized as a whole. They can contain references to other `UnityEngine.Objects`, and these references get serialized properly.



##Serialization rules
Because of the very high performance requirements that the serializer has, it does not always behave exactly like a C# developer would expect from a serializer. Below is some guidance on how to make best use of serialization.

####How to ensure a field in a script is serialized
Ensure it:

* is `public`, or has a [SerializeField](ScriptRef:SerializeField.html) attribute (doesn't need to be serialized for hot reloading)
* is not  `static`
* is not  `const`
* is not  `readonly`
* has  `fieldtype` that is of a type that can be serialized (See below.)

####Fieldtypes that can be serialized
* Custom non-abstract classes with `[Serializable]` attribute.
* Custom structs with `[Serializable]` attribute (added in Unity 4.5).
* References to objects that derive from `UnityEngine.Object`.
* Primitive data types (`int`, `float`, `double`, `bool`, `string`, etc.).
* Enum types.
* Certain Unity built-in types: `Vector2`, `Vector3`, `Vector4`, `Rect`, `Quaternion`, `Matrix4x4`, `Color`, `Color32`, `LayerMask`, `AnimationCurve`, `Gradient`, `RectOffset`, `GUIStyle`.
* Array of a fieldtype that can be serialized.
* `List`&lt;`T`&gt; of a fieldtype that can be serialized.

####In what situations does serializer behave unexpectedly?

**Custom classes behave like structs**

````
[Serializable]
class Animal
{
   public string name;
}

class MyScript : MonoBehaviour
{
      public Animal[] animals;
}
````

If you populate the `animals` array with three references to a single Animal object, in the serialization stream, you find 3 objects.  When it’s deserialized, there are now three different objects. If you need to serialize a complex object graph with references, you cannot rely on Unity’s serializer doing that all automatically for you; you have to do some work to get that object graph serialized yourself. See the example below on how to serialize things Unity doesn't serialize by itself.

Note that this is only true for custom classes; they are serialized "inline" because their data becomes part of the complete serialization data for the `MonoBehaviour` they are used in.  When you have fields that have a reference to something that is a `UnityEngine.Object` derived class, such as a `public Camera myCamera`,  the data from that camera is not serialized inline. Instead an actual reference to the camera `UnityEngine.Object` is serialized.

**No support for `null` for custom classes**

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

It wouldn’t be strange to expect 1 allocation: That of the `Test` object. It also wouldn’t be strange to expect 2 allocations: One for the `Test` object and one for a `Trouble` object. 

However, the correct answer is 729. The serializer does not support null. If it serializes an object, and a field is null, Unity instantiates a new object of that type, and serializes that. Obviously this could lead to infinite cycles, so there is a depth limit of 7 levels. At that point Unity stops serializing fields that have types of custom classes, structs, lists, or arrays.

Since so many of Unity's subsystems build on top of the serialization system, this unexpectedly large serialization stream for the `Test MonoBehaviour` causes all these subsystems to perform more slowly than necessary.  

**NOTE:** This causes so significant a performance problem in many projects that  it carries a warning message (since Unity 4.5).

**No support for polymorphism**
 
if you have a `public Animal[] animals` and you put in an instance of a dog, a cat and a giraffe, after serialization, you have three instances of Animal.

One way to deal with this limitation is to realize that it only applies to custom classes, which get serialized inline. References to other `UnityEngine.Objects` get serialized as actual references, and for those, polymorphism does actually work.  You would make a `ScriptableObject` derived class or another `MonoBehaviour` derived class, and reference that. The downside of this is that you need to store that `Monobehaviour` or scriptable object somewhere, and that you cannot serialize it inline efficiently.

The reason for these limitations is that one of the core foundations of the serialization system is that the layout of the datastream for a object is known ahead of time; it depends on the types of the fields of the class, rather than what happens to be stored inside the fields.

**Serializing someting that that Unity's serializer doesn't support**

In many cases the best approach is to use serialization callbacks. These allow you to be notified before the serializer reads data from your fields and after it has finished writing to them. You can use serialization callbacks to have a different representation of your hard-to-serialize data at run time to its representation when you actually serialize.

Transform your data into something Unity understands right before Unity wants to serialize it.  Then, right after Unity has written the data to your fields you can transform the serialized form back into the form you want to have your data in at run time 

For example: Suppose you want to have a tree data structure. If you let Unity directly serialize the data structure, the "no support for null" limitation would cause your data stream to become very big, leading to performance degradations in many systems:

````
using UnityEngine;
using System.Collections.Generic;
using System;

public class VerySlowBehaviourDoNotDoThis : MonoBehaviour
{
[Serializable]
public class Node
{
public string interestingValue = "value";

//The field below is what makes the serialization data become huge because
//it introduces a 'class cycle'.
public List<Node> children = new List<Node>();
}
//this gets serialized
public Node root = new Node();

void OnGUI()
{
Display (root);
}

void Display(Node node)
{
GUILayout.Label ("Value: ");
node.interestingValue = GUILayout.TextField(node.interestingValue, GUILayout.Width(200));

GUILayout.BeginHorizontal ();
GUILayout.Space (20);
GUILayout.BeginVertical ();

foreach (var child in node.children)
Display (child);
if (GUILayout.Button ("Add child"))
node.children.Add (new Node ());

GUILayout.EndVertical ();
GUILayout.EndHorizontal ();
}
}
````

Instead, you tell Unity not to serialize the tree directly, and you make a seperate field to store the tree in a serialized format, suited to Unity’s serializer:

````
using System.Collections.Generic;
using System;

public class BehaviourWithTree : MonoBehaviour, ISerializationCallbackReceiver
{
// Node class that is used at runtime.
// This is internal to the BehaviourWithTree class and is not serialized.
public class Node
{
public string interestingValue = "value";
public List<Node> children = new List<Node>();
}

// Node class that we will use for serialization.
[Serializable]
public struct SerializableNode
{
public string interestingValue;
public int childCount;
public int indexOfFirstChild;
}

// The root node used for runtime tree representation. Not serialized.
Node root = new Node(); 

// This is the field we give Unity to serialize.
public List<SerializableNode> serializedNodes;

public void OnBeforeSerialize()
{
// Unity is about to read the serializedNodes field's contents.
// The correct data must now be written into that field "just in time".
if (serializedNodes == null) serializedNodes = new List<SerializableNode>();
if (root == null) root = new Node ();
serializedNodes.Clear();
AddNodeToSerializedNodes(root);
// Now Unity is free to serialize this field, and we should get back the expected 
// data when it is deserialized later.
}

void AddNodeToSerializedNodes(Node n)
{
var serializedNode = new SerializableNode () {
interestingValue = n.interestingValue,
childCount = n.children.Count,
indexOfFirstChild = serializedNodes.Count+1
};
serializedNodes.Add (serializedNode);
foreach (var child in n.children)
AddNodeToSerializedNodes (child);
}

public void OnAfterDeserialize()
{
//Unity has just written new data into the serializedNodes field.
//let's populate our actual runtime data with those new values.
if (serializedNodes.Count > 0) {
ReadNodeFromSerializedNodes (0, out root);
}
else
root = new Node ();
}

int ReadNodeFromSerializedNodes(int index, out Node node)
{
var serializedNode = serializedNodes [index];
// Transfer the deserialized data into the internal Node class
Node newNode = new Node() {
interestingValue = serializedNode.interestingValue,
children = new List<Node> ()
};
// The tree needs to be read in depth-first, since that's how we wrote it out.
for (int i = 0; i != serializedNode.childCount; i++) {
Node childNode;
index = ReadNodeFromSerializedNodes (++index, out childNode);
newNode.children.Add (childNode);
}
node = newNode;
return index;
}

// This OnGUI draws out the node tree in the Game View, with buttons to add new nodes as children.
void OnGUI()
{
if (root != null)
Display (root);
}

void Display(Node node)
{
GUILayout.Label ("Value: ");
// Allow modification of the node's "interesting value".
node.interestingValue = GUILayout.TextField(node.interestingValue, GUILayout.Width(200));

GUILayout.BeginHorizontal ();
GUILayout.Space (20);
GUILayout.BeginVertical ();

foreach (var child in node.children)
Display (child);
if (GUILayout.Button ("Add child"))
node.children.Add (new Node ());

GUILayout.EndVertical ();
GUILayout.EndHorizontal ();
}
}
````

Beware that the serializer, including these callbacks coming from the serializer, usually happen not on the main thread, so you are very limited in what you can do in terms of invoking Unity API. You can, however, do the necessary data transformations to get your data from a non-Unity-serializer-friendly format to a Unity-serializer-friendly-format.

## Script serialization errors
When scripts call the Unity API from constructors or field initializers, or during deserialization (loading), they can trigger errors. This section demonstrates the poor practise that causes these errors.

You should call the majority of the Unity API from the main thread; for example, from `Start` or `Update` on MonoBehaviour. 

You should only call a subset of the Unity API from script constructors or field initializers;  `Debug.Log` or `Mathf` for example. This is because constructors are invoked when constructing an instance of a class during deserialization, and these should only run on a main thread but might end up running on a non-main thread. So, you get errors if you call all the Unity API from script constructors or field initializers.  

###Calling Unity API from constructor or field initializers

When Unity creates an instance of a MonoBehaviour or ScriptableObject derived class, it calls the default constructor to create the managed object. This happens before entering the main loop, and before the Scene has been fully loaded. Field initializers are also called from the default constructor of a managed object. In general, do not call the Unity API from a constructor, as this is unsafe for the majority of the Unity API.

Examples of **poor practice**:

````
//NOTE: THIS IS A BAD EXAMPLE TO DEMONSTRATE POOR PRACTISE  - DO NOT REUSE

public class FieldAPICallBehaviour : MonoBehaviour
{
   public GameObject foo = GameObject.Find("foo");   // This line generates an error 
                        // message as it should not be called from within a constructor

}
````
````
//NOTE: THIS IS A BAD EXAMPLE TO DEMONSTRATE POOR PRACTISE - DO NOT REUSE

public class ConstructorAPICallBehaviour : MonoBehaviour
{
   ConstructorAPICallBehaviour()
   {
       GameObject.Find("foo");   // This line generates an error message
                                // as it should not be called from within a constructor
   }
}
````

Both these cases generate the error message: *Find is not allowed to be called from a MonoBehaviour constructor (or instance field initializer), call in in Awake or Start instead.*

Fix this by making the the call to the Unity API in `MonoBehaviour.Start`.

###Calling Unity API during deserialization

When Unity loads a Scene, it recreates the managed objects from the saved Scene and populates them with the saved values (deserializing). In order to create the managed objects, call the default constructor for the objects. If a field referencing a object is saved (serialized) and the object default constructor calls the Unity API, you get an error when loading the Scene. As with the previous error, it is not yet in the main loop and the Scene is not fully loaded. This is considered unsafe for the majority of the Unity API.

Example of **poor practice**:

````
//NOTE: THIS IS A BAD EXAMPLE TO DEMONSTRATE POOR PRACTISE  - DO NOT REUSE

public class SerializationAPICallBehaviour : MonoBehaviour
{
   [System.Serializable]
   public class CallAPI
   {
       public CallAPI()
       {
           GameObject.Find("foo"); // This line generates an error message 
                                                 // as it should not be called during serialization

       }
   }

   CallAPI callAPI;
}
````

This generates the error: *Find is not allowed to be called during serialization, call it from Awake or Start instead.*

To fix this, refactor your code so that no Unity API calls are made in any constructors for any serialized objects. If you need to call the Unity API for a object, do this in the main thread from one of the MonoBehaviour callbacks, such as `Start`, `Awake` or `Update`.
