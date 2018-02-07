# Universal Windows Platform: WinRT API in C# scripts

It is possible to use WinRT API directly in Unity scripts. However there are limitations and requirements for this:

* Scripts must be written in C#, it's not possible to use WinRT API from UnityScript
* Scripts must be compiled using Microsoft's compiler, not Mono. This requires to set compilation overrides to **Use .NET Core** or **Use .NET Core Partially**, in the later case scripts must **not** be under **Plugins** or **Standard Assets** folders
* Because the same script code is also used by Unity Editor (which always uses Mono), all code that uses WinRT API must be under **ENABLE_WINMD_SUPPORT** define

Below is an example for getting advertising using WinRT API directly:

```C#
using UnityEngine;
public class WinRTAPI : MonoBehaviour {
	void Update() {
		auto adId = GetAdvertisingId();
		// ...
	}

	string GetAdvertisingId() {
		#if ENABLE_WINMD_SUPPORT
			return Windows.System.UserProfile.AdvertisingManager.AdvertisingId;
		#else
			return "";
		#endif
	}
}
```

Note: when using IL2CPP scripting backend, this is only supported when using .NET 4.6 compatiblity profile.