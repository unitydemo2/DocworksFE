#Universal Windows Platform: Command line arguments

Universal Windows Apps don't accept command line arguments by default, so to pass them you have to call a special function from App.xaml.cs/cpp or App.cs/cpp. For ex., **appCallbacks.AddCommandLineArg("-nolog");**
You have to call it before **appCallbacks.Initialize()** function.

## Arguments

* **-nolog** - Don't produce UnityPlayer.log.

* **-force-driver-type-warp** - Force DirectX 11.0 WARP device (More info [http://msdn.microsoft.com/en-us/library/gg615082.aspx](http://msdn.microsoft.com/en-us/library/gg615082.aspx))

* **-force-gfx-direct** - Force single threaded rendering.

* **-force-d3d11-no-singlethreaded** - Force DirectX 11.0 to be created without D3D11_CREATE_DEVICE_SINGLETHREADED flag.

* **-dontConnectAcceleratorEvent** - Disable connecting to `AcceleratorKeyEvent`. This may help if you have issues with input in XAML elements. The downside is that Unity cannot handle some keys (for example, the keyboard keys __F10__, __Ctrl__, __Alt__, __Tab__ may have issues in Unity).

* **-forceTextBoxBasedKeyboard** - Use TextBox-based implementation for `TouchScreenKeyboard`. Only has an effect on UWP XAML applications. Allows switching to different implementations, in case there are issues with the default one.

## DirectX feature levels

For further information about DirectX feature levels, see  [http://msdn.microsoft.com/en-us/library/windows/desktop/ff476876(v=vs.85).aspx](http://msdn.microsoft.com/en-us/library/windows/desktop/ff476876(v=vs.85).aspx))

* **-force-feature-level-9-1** - Force DirectX 11.0 feature level 9.1.

* **-force-feature-level-9-3** - Force DirectX 11.0 feature level 9.3.

* **-force-feature-level-10-0** - Force DirectX 11.0 feature level 10.0.

* **-force-feature-level-10-1** - Force DirectX 11.0 feature level 10.1.

* **-force-feature-level-11-0** - Force DirectX 11.0 feature level 11.0.

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>