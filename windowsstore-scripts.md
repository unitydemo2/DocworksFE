# Windows Store Apps: WinRT API in C# scripts

It is possible to use WinRT API directly in Unity scripts. However there are limitations and requirements for this:

* Scripts must be written in C#, it's not possible to use WinRT API from UnityScript
* Scripts must be compiled using Microsoft's compiler, not Mono. This requires to set compilation overrides to **Use .NET Core** or **Use .NET Core Partially**, in the later case scripts must **not** be under **Plugins** or **Standard Assets** folders
* Because the same script code is also used by Unity Editor (which always uses Mono), all code that uses WinRT API must be under **NETFX_CORE** define
* If you want to use Universal Windows 10 API, use **WINDOWS_UWP** define.

Note, that **NETFX_CORE** or **WINDOWS_UWP** is defined by Visual Studio when compiling code for Windows Store Apps, so it can be used in any C# code, not just Unity scripts.

Below is an example for getting advertising using WinRT API directly:

```C#
using UnityEngine;
public class WinRTAPI : MonoBehaviour {
	void Update() {
		auto adId = GetAdvertisingId();
		// ...
	}

	string GetAdvertisingId() {
		#if NETFX_CORE
			return Windows.System.UserProfile.AdvertisingManager.AdvertisingId;
		#else
			return "";
		#endif
	}
}
```

Note: this is currently supported only on .NET scripting backend.