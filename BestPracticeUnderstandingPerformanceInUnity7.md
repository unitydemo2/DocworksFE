# General Optimizations

There are as many different ways to optimize code as there are reasons for performance problems. In general, it is strongly recommended that developers closely profile their applications before attempting to apply CPU optimizations. However, there are several simple CPU optimizations that are universally applicable.

## Address Properties by ID

Unity does not use string names to address Animator, Material and Shader properties internally. For speed, all property names are hashed into property IDs, and it is these IDs that are actually used to address the properties.

Therefore, whenever using a *Set* or *Get* method on an Animator, Material or Shader, use the integer-valued method instead of the string-valued methods. The string methods simply perform string hashing and then forward the hashed ID to the integer-valued methods.

The property IDs created from string hashes are deterministic over the course of a single run. The simplest way to use them is to declare a static read-only integer variable for each property name, and use the integer variable in place of the string. These are automatically initialized during startup with no further initialization code needed.

The appropriate APIs are [Animator.StringToHash](ScriptRef:Animator.StringToHash.html) for Animator property names, and [Shader.PropertyToID](ScriptRef:Shader.PropertyToID.html) for Material & Shader property names.

## Use non-allocating physics APIs

In Unity 5.3 and onwards, non-allocating versions of all Physics query APIs have been introduced. Replace [RaycastAll](ScriptRef:Physics.RaycastAll.html) calls with [RaycastNonAlloc](ScriptRef:Physics.RaycastNonAlloc.html), [SphereCastAll](ScriptRef:Physics.SphereCastAll.html) calls with [SphereCastNonAlloc](ScriptRef:Physics.SphereCastNonAlloc.html), and so on. For 2D applications, there are also non-allocating versions of all Physics2D query APIs.

## Transform manipulation

Whenever a Transform’s position or rotation is changed, an `OnTransformChanged` message is dispatched to all components on the same GameObject as the Transform, as well as all child GameObjects. For this reason, it is best practice to attempt to alter a Transform’s position and rotation as few times as possible during a given frame. Instead, batch all possible changes that need to be applied to the Transform, and apply them once. This minimizes the number of `OnTransformChanged` messages that must propagate through the Transform hierarchy, and is especially important when moving deep/large Transform hierarchies, such as animated characters.

### Vector and quaternion math and order of operations

For vector and quaternion math that is located in tight loops, remember that integer math is faster than floating-point math, and floating-point math is faster than vector, matrix or quaternion math.


Therefore, whenever commutative or associative arithmetic allows, attempt to minimize the cost of individual mathematical operations:

```

Vector3 x;

int a, b;

// Less efficient: results in two vector multiplications

Vector3 slow = a * x * b;

// More efficient: one integer mult, one vector mult

Vector3 fast = a * b * x;

```

## Built-In ColorUtility

It is common for applications that must convert between HTML-formatted color strings (`#RRGGBBAA`) and Unity’s native `Color` and `Color32` structures to use a script from the Unify Community. This script was both slow and caused extensive memory allocation due to string manipulation.

As of Unity 5, there is a built-in [ColorUtility](ScriptRef:ColorUtility.html) API that performs these conversions efficiently. Usage of the built-in API should be preferred.

## Find and FindObjectOfType

It is a general best practice to eliminate all usage of `Object.Find` and `Object.FindObjectOfType` in production code. As these APIs require Unity to iterate over all GameObjects and Components in memory, they rapidly become non-performant as the scope of a project grows.

An exception to the above rule can be made in accessors for singleton objects. A global manager object often exposes an "instance" property, and often has a `FindObjectOfType` call in the getter to detect pre-existing instances of the singleton:

```

class SomeSingleton {

	private SomeSingleton _instance;

	public SomeSingleton Instance {

		get {

			if(_instance == null) { 

				_instance =

					FindObjectOfType<SomeSingleton>(); 

			}

			if(_instnace == null) { 

				_instance = CreateSomeSingleton();

			}

			return _instance;

		}

	}

}

```

While this pattern is generally acceptable, it is important to examine the code and ensure that the accessor is be called in Scenes where the singleton object does not exist. If the getter does not automatically create an instance of a missing singleton, it is very common to discover that code looking for the singleton results in repeated calls to `FindObjectOfType` (often multiple times per frame) and creates an undesirable drain on performance.

### Camera locators

Internally, Unity’s `Camera.main` property calls `Object.FindObjectWithTag`, a specialized variant of `Object.FindObject`. Accessing this property is no more efficient than a call to `Object.FindObjectOfType`. If code must address the main camera, it is strongly recommended to do one of two things:

* Access `Camera.main` in a `Start` or` OnEnable` callback and cache the resulting reference.

* Construct a `Camera Manager` class that can provide or inject a reference to the active camera.

## Debug code & the [conditional] attribute

The `UnityEngine.Debug` logging APIs are not stripped from non-development builds, and do write to log files if called. As most developers do not intend to write debug information in non-development builds, it is recommended to wrap development-only logging calls in custom methods, like so:

```

    public static class Logger {

        [Conditional("ENABLE_LOGS")]

        public static void Debug(string logMsg) {

		    UnityEngine.Debug.Log(logMsg);

        }

    }

```

By decorating these methods with the [Conditional] attribute, the define or defines used by the Conditional attribute determine whether the decorated method is included in the compiled source.

If none of the defines passed to the Conditional attribute are defined, then the decorated method *and* all calls to the decorated method are compiled out. The effect is identical to what would happen if the method and all calls to the method were wrapped in `#if … #endif` preprocessor blocks.

For more information on the `Conditional` attribute, see the MSDN website: [msdn.microsoft.com](https://msdn.microsoft.com/en-us/library/4xssyw96(v=vs.90).aspx).

