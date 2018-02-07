#Universal Windows Platform: Plugins on IL2CPP Scripting Backend

At this point in time, the plugin model for Universal Windows Platform with IL2CPP scripting backend is much more similar to other Unity platforms (such as Windows standalone), rather than Universal Windows Platform with .NET scripting backend.

## Managed plugins

By default, IL2CPP targets .NET 2.0 API compatiblity level. That means unlike .NET scripting backend, it does not support managed plugins targeting .NET 4.5 or consuming any of Windows Runtime APIs. All managed plugins must be targeting .NET 3.5 or equivalent API when using this compatiblity level. You can switch to .NET 4.6 API compatibilty level in player settings if you wish to lift these restrictions.

Another difference compared to .NET scripting backend is that IL2CPP scripting backend exposes the exact same .NET API surface as Unity editor or standalone player, so it's possible to use the same plugins without the need to compile separate versions target different .NET API for Universal Windows Platform.

## Native plugins

IL2CPP scripting backend supports using native plugins through P/Invoke mechanism. It means that you can call into native plugins directly from your C# code by specifying the native function prototype and then calling it. For example:

    [DllImport("MyPlugin.dll")]
    private static extern int CountLettersInString([MarshalAs(UnmanagedType.LPWSTR)]string str);
    
    private void Start()
    {
        Debug.Log(CountLettersInString("Hello, native plugin!"));
    }
    
The implementation of such function inside MyPlugin.dll would look like this:

    extern "C" __declspec(dllexport)
    int __stdcall CountLettersInString(wchar_t* str)
    {
        int length = 0;
        while (*str++ != nullptr)
            length++;
        return length;
    }

P/Invoke marshaling rules match that of official .NET marshaling, with exception of few unsupported types:

* AnsiBStr
* BStr
* Currency
* SAFEARRAY
* IDispatch
* IUnknown
* TBStr
* VBByRefStr

The default calling convention for P/Invoke functions on x86 is ``__stdcall``.

Native plugins can be authored in two ways: precompiled DLL or C++ source code.

### Precompiled native plugins

P/Invoking into precompiled native plugins works by loading the DLL at runtime, finding the function entry point and then calling it. These DLLs must be compiled against appropriate Windows SDK for the target CPU architecture. The DLLs must also be configured in Plugin Inspector when added to Unity project.

### C++ source code native plugins

It is possible to add C++ (.cpp) code files directly into Unity project, which will act as a plugin in Plugin Inspector. If configured to be compatible with Universal Windows Platform and IL2CPP scriping backend, these C++ files will be compiled together with C++ code that gets generated from managed assemblies:

![](../uploads/Main/NativeFunctions.png)

Since the functions are linked together with generated C++ code, there is no separate DLL to P/Invoke into. Due to this, it's possible to use "__Internal" keyword in place of DLL name, which will make it C++ Linker responsibility to resolve the functions, rather than loading them at runtime:

    [DllImport("__Internal")]
    private static extern int CountLettersInString([MarshalAs(UnmanagedType.LPWSTR)]string str);

Since the call is resolved by the linker, making an error in function declaration on managed side will produce a linker error, rather an error at runtime. This also means that no dynamic loading needs to take place at runtime, and function is called directly. This significantly decreases the overhead of a P/Invoke call.

### P/Invoke limitations

On Universal Windows Platform you cannot P/Invoke into specific system libraries by specifying the dll name (like "kernelbase.dll") when using IL2CPP scripting backend. Attempting to P/Invoke into any DLL that exists outside of the project will result in DllNotFoundException at runtime.

However, it's still possible to P/Invoke into these system functions by specifying "**Internal" keyword instead of the DLL name, which results in linker resolving the functions at build time.

## See also

[Plugin Inspector](PluginInspector.html "Plugin Inspector")

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>