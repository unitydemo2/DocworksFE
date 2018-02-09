# Scripting restrictions

We strive to provide a common scripting API and experience across all platforms Unity supports. However, some platforms have inherent restrictions. To help you understand these restrictions and support cross-platform code, the following table describes which restrictions apply to each platform and scripting backend:

| **_Platform_** | **_Scripting Backend_** | **_Restrictions_** | 
|:---|:---|:---| 
| Standalone | Mono | None | 
| WebGL | IL2CPP | [Ahead-of-time compile](#AOT), [No threads](#threads)| 
| iOS | IL2CPP | [Ahead-of-time compile](#AOT) | 
| Android | Mono | None | 
| Android | IL2CPP | [Ahead-of-time compile](#AOT) | 
| Samsung TV | Mono | [Ahead-of-time compile](#AOT) | 
| Tizen | Mono | [Ahead-of-time compile](#AOT) | 
| XBox One | Mono | [Ahead-of-time compile](#AOT) | 
| XBox One | IL2CPP | [Ahead-of-time compile](#AOT) | 
| WiiU | Mono | [Ahead-of-time compile](#AOT) | 
| PS Vita | Mono | [Ahead-of-time compile](#AOT) | 
| PS Vita | IL2CPP | [Ahead-of-time compile](#AOT) | 
| PS4 | Mono | [Ahead-of-time compile](#AOT) | 
| PS4 | IL2CPP | [Ahead-of-time compile](#AOT) | 
| Windows Store | .NET | Uses .NET Core class libraries subset | 
| Windows Store | IL2CPP | [Ahead-of-time compile](#AOT) | 

<a name="AOT"></a>
## Ahead-of-time compile

Some platforms do not allow runtime code generation. Therefore, any managed code which depends upon just-in-time (JIT) compilation on the target device will fail. Instead, we need to compile all of the managed code ahead-of-time (AOT). Often, this distinction doesn't matter, but in a few specific cases, AOT platforms require additional consideration.

### System.Reflection.Emit

An AOT platform cannot implement any of the methods in the **System.Reflection.Emit** namespace. Note that the rest of **System.Reflection** is acceptable, as long as the compiler can infer that the code used via reflection needs to exist at runtime.

### Serialization

AOT platforms may encounter issues with serialization and deserlization due to the use of reflection. If a type or method is only used via reflection as part of serialization or deserialization, the AOT compiler cannot detect that code needs to be generated for the type or method.

### Generic virtual methods

Generic methods require the compiler to do some additional work to expand the code written by the developer to the code actually executed on the device. For example, we need different code for **List** with an **int** or a **double**. In the presence of virtual methods, where behavior is determined at runtime rather than compile time, the compiler can easily require runtime code generation in places where it is not entirely obvious from the source code.

Suppose we have the following code, which works exactly as expected on a JIT platform (it prints "Message value: Zero" to the console once):

```
using UnityEngine;
using System;

public class AOTProblemExample : MonoBehaviour, IReceiver {
	public enum AnyEnum {
		Zero,
		One,
	}

	void Start() {
		// Subtle trigger: The type of manager *must* be
		// IManager, not Manager, to trigger the AOT problem.
		IManager manager = new Manager();
		manager.SendMessage(this, AnyEnum.Zero);
	}

	public void OnMessage<T>(T value) {
		Debug.LogFormat("Message value: {0}", value);
	}
}

public class Manager : IManager {
	public void SendMessage<T>(IReceiver target, T value) {
		target.OnMessage(value);
	}
}

public interface IReceiver {
	void OnMessage<T>(T value);
}

public interface IManager {
	void SendMessage<T>(IReceiver target, T value);
}
```

When this code is executed on an AOT platform with the IL2CPP scripting backend, this exception occurs:

```
ExecutionEngineException: Attempting to call method 'AOTProblemExample::OnMessage<AOTProblemExample+AnyEnum>' for which no ahead of time (AOT) code was generated.
  at Manager.SendMessage[T] (IReceiver target, .T value) [0x00000] in <filename unknown>:0 
  at AOTProblemExample.Start () [0x00000] in <filename unknown>:0 
```

Likewise, the Mono scripting backend provides this similar exception:

```
  ExecutionEngineException: Attempting to JIT compile method 'Manager:SendMessage<AOTProblemExample/AnyEnum> (IReceiver,AOTProblemExample/AnyEnum)' while running with --aot-only.
  at AOTProblemExample.Start () [0x00000] in <filename unknown>:0 
```

The AOT compiler does not realize that it should generate code for the generic method **OnMessage** with a **T** of **AnyEnum**, so it blissfully continues, skipping this method. When that method is called, and the runtime can't find the proper code to execute, it gives up with this error message.

To work around an AOT issue like this, we can often force the compiler to generate the proper code for us. If we add a method like this to the **AOTProblemExample** class:

```
public void UsedOnlyForAOTCodeGeneration() {
	// IL2CPP needs only this line.
	OnMessage(AnyEnum.Zero);

	// Mono also needs this line. Note that we are
	// calling directly on the Manager, not the IManager interface.
	new Manager().SendMessage(null, AnyEnum.Zero);

	// Include an exception so we can be sure to know if this method is ever called.
	throw new InvalidOperationException("This method is used for AOT code generation only. Do not call it at runtime.");
}
```

When the compiler encounters the explicit call to **OnMessage** with a **T** of **AnyEnum**, it generates the proper code for the runtime to execute. The method **UsedOnlyForAOTCodeGeneration** does not ever need to be called; it just needs to exist for the compiler to see it.

<a name="threads"></a>
## No threads

Some platforms do not support the use of threads, so any managed code that uses the **System.Threading** namespace will fail at runtime. Also, some parts of the .NET class libraries implicitly depend upon threads. An often-used example is the **System.Timers.Timer** class, which depends on support for threads.
