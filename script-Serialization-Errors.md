# Script serialization errors

Serialization is the automatic process of transforming data structures or object states into a format that Unity can store and reconstruct later.  (See the documentation on [Script Serialization](script-Serialization) for further information.)

In certain circumstances, Script serialization can cause errors. Fixes to some of these are listed below.

#### Calling Unity Scripting API from constructor or field initializers

Calling Scripting  API such as [GameObject.Find](ScriptRef:GameObject.Find.html) inside a [MonoBehaviour](ScriptRef:MonoBehaviour.html) constructor or field initializer triggers the error: "Find is not allowed to be called from a MonoBehaviour constructor (or instance field initializer), call in in Awake or Start instead."

Fix this by making the call to the Scripting API in [MonoBehaviour.Start](ScriptRef:MonoBehaviour.Start.html) instead of in the constructor.

#### Calling Unity Scripting API during deserialization

Calling Scripting API such as [GameObject.Find](ScriptRef:GameObject.Find.html) from within the constructor of a class marked with `System.Serializable` triggers the error: "Find is not allowed to be called during serialization, call it from Awake or Start instead."

To fix this, edit your code so that it makes no Scripting API calls in any constructors for any serialized objects.

#### Thread-safe Unity Scripting API

The majority of the Scripting API is affected by the restrictions listed above. Only select parts of the Unity scripting API are exempt and may be called from anywhere. These are:

* [Debug.Log](ScriptRef:Debug.Log.html)

* [Mathf](ScriptRef:Mathf.html) functions

* Simple self-contained structs; for example math structs like [Vector3](ScriptRef:Vector3.html) and [Quaternion](ScriptRef:Quaternion.html)

To reduce the risk of errors during serialization, only call API methods that are self-contained and do not need to get or set data in Unity itself. Only call these if there is no alternative.
<br/><br/>

----

<span class="page-edit">• 2017-05-15  <!-- include IncludeTextNewPageYesEdit --></span><br/>
