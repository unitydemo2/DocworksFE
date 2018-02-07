#JSON Serialization

The JSON Serialization feature converts objects to and from [JSON](http://www.json.org) format.  This can be useful when interacting with web services, or just for packing and unpacking data to a text-based format easily.

For information on the JsonUtility class, please see the Unity ScriptRef [JsonUtility](ScriptRef:JsonUtility) page. 

## Simple usage

The JSON Serialization feature is built around a notion of 'structured' JSON, which means that you describe what variables are going to be stored in your JSON data by creating a class or structure. For example:

````
[Serializable]
public class MyClass
{
	public int level;
	public float timeElapsed;
	public string playerName;
}
````

This defines a plain C# class containing three variables - __level__, __timeElapsed__, and __playerName__ - and marks it as Serializable, which is necessary for it to work with the JSON serializer. You could then create an instance of it like this:

````
MyClass myObject = new MyClass();
myObject.level = 1;
myObject.timeElapsed = 47.5f;
myObject.playerName = "Dr Charles Francis";
````

And serialize it to JSON format by using ``JsonUtility.ToJson``:

````
string json = JsonUtility.ToJson(myObject);
````

This would result in the ``json`` variable containing the string:

````
{"level":1,"timeElapsed":47.5,"playerName":"Dr Charles Francis"}
````

To convert the JSON back into an object, use ``JsonUtility.FromJson``:

````
myObject = JsonUtility.FromJson<MyClass>(json);
````

This will create a new instance of ``MyClass`` and set the values on it using the JSON data. If the JSON data contains values that do not map to fields in ``MyClass`` then those values will simply be ignored, and if the JSON data is missing values for fields in ``MyClass``, then those fields will be left at their constructed values in the returned object.

The JSON Serializer does not currently support working with 'unstructured' JSON (i.e. navigating and editing the JSON as an arbitrary tree of key-value pairs). If you need to do this, you should look for a more fully-featured JSON library.

## Overwriting objects with JSON

It is also possible to take JSON data and deserialize it 'over' an already-created object, overwriting data that is already present:

````
JsonUtility.FromJsonOverwrite(json, myObject);
````

Any fields on the object for which the JSON does not contain a value will be left unchanged. This method allows you to keep allocations to a minimum by reusing objects that you created previously, and also to 'patch' objects by deliberately overwriting them with JSON that only contains a small subset of fields.

Note that the JSON Serializer API supports ``MonoBehaviour`` and ``ScriptableObject`` subclasses as well as plain structs/classes. However, when deserializing JSON into subclasses of ``MonoBehaviour`` or ``ScriptableObject``, you _must_ use FromJsonOverwrite; FromJson is not supported and will throw an exception.

##Supported Types
The API supports any ``MonoBehaviour``-subclass, ``ScriptableObject``-subclass, or plain class/struct with the ``[Serializable]`` attribute. The object you pass in is fed to the standard Unity serializer for processing, so the same rules and limitations apply as they do in the Inspector; only fields are serialized, and types like ``Dictionary&lt;&gt;`` are not supported.

Passing other types directly to the API, for example primitive types or arrays, is not currently supported. For now you will need to wrap such types in a ``class`` or ``struct`` of some sort.

In the Editor only, there is a parallel API - ``EditorJsonUtility`` - which allows you to serialize any ``UnityEngine.Object``-derived type both to and from JSON. This will produce JSON that contains the same data as the YAML representation of the object.

##Performance
Benchmark tests have shown ``JsonUtility`` to be significantly faster than popular .NET JSON solutions (albeit with fewer features than some of them).

GC Memory usage is at a minimum:

* ``ToJson()`` allocates GC memory only for the returned string.
* ``FromJson()`` allocates GC memory only for the returned object, as well as any subobjects needed (e.g. if you deserialize an object that contains an array, then GC memory will be allocated for the array).
* ``FromJsonOverwrite()`` allocates GC memory only as necessary for written fields (for example strings and arrays). If all fields being overwritten by the JSON are value-typed, it should not allocate any GC memory.

Using the JsonUtility API from a background thread is **permitted.** As with any multithreaded code, you should be careful not to access or alter an object on one thread while it is being serialized/deserialized on another.

##Controlling the output of ToJson()

``ToJson`` supports pretty-printing the JSON output. It is off by default but you can turn it on by passing ``true`` as the second parameter.

Fields can be omitted from the output by using the ``[NonSerialized]`` attribute.

##Using FromJson() when the type is not known ahead of time
Deserialize the JSON into a class or struct that contains 'common' fields, and then use the values of those fields to work out what actual type you want. Then deserialize a second time into that type.
