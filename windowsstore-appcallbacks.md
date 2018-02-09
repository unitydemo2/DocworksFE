AppCallbacks class
==================


You could call it a bridge between your main application and Unity engine. Here, we'll try to explain what every call to AppCallbacks exactly does. Let's build solution and explore App.xaml.cs file, which gets created if you use .NET Scripting Backend.

````
sealed partial class App : Application
{
	private WinRTBridge.WinRTBridge _bridge;
	private AppCallbacks appCallbacks;
	public App()
	{
		this.InitializeComponent();
		appCallbacks = new AppCallbacks(false);
	}

	protected override void OnLaunched(LaunchActivatedEventArgs args)
	{
		Frame rootFrame = Window.Current.Content as Frame;
		if (rootFrame == null)
		{
			var mainPage = new MainPage();
			Window.Current.Content = mainPage;
			Window.Current.Activate();

			_bridge = new WinRTBridge.WinRTBridge();
			appCallbacks.SetBridge(_bridge);

			appCallbacks.SetSwapChainBackgroundPanel(mainPage.GetSwapChainBackgroundPanel());

			appCallbacks.SetCoreWindowEvents(Window.Current.CoreWindow);

			appCallbacks.InitializeD3DXAML();
		}

		Window.Current.Activate();
	}
}
````

**private WinRTBridge.WinRTBridge \_bridge;**

So first of all, what is WinRTBridge, it's used internally by Unity, to perform some of native-to-managed, managed-to-native operations, it's not intended to be used by developers. Due some WinRT platform restrictions, it cannot be created from Unity engine code, that's why WinRTBridge is being created here and is passed to Unity engine via appCallbacks.SetBridge(_bridge) instead.

**appCallbacks = new AppCallbacks(false);**

Now, let's take a closer look at AppCallbacks class. When you create it, you specify that your game will run on different thread, for backward compatibility reasons you can also specify that your application can run on UI thread, but that's not recommended, because there's a restriction from Microsoft - if your application won't become responsive after 5 seconds you'll fail to pass WACK (Windows Application Certification), read more here - [http://msdn.microsoft.com/en-us/library/windowsphone/develop/hh184840(v=vs.105).aspx](http://msdn.microsoft.com/en-us/library/windowsphone/develop/hh184840(v=vs.105).aspx), imagine if your first level is pretty big, it might take significant amount of time to load it, because your application is running on UI thread, UI will be unresponsive until your level is fully loaded. That's why it's recommend to always run your game on different thread.

Read more on UI thread here - [http://msdn.microsoft.com/en-us/library/windows/apps/hh994635.aspx](http://msdn.microsoft.com/en-us/library/windows/apps/hh994635.aspx)

**Note:** Code located in App.xaml.cs, MainPage.xaml.cs is always running on UI thread, unless called from InvokeOnAppThread function.

**appCallbacks.SetSwapChainBackgroundPanel(mainPage.GetSwapChainBackgroundPanel());**

This simply passes a XAML control to Unity which will be used as a render target for DirectX 11.

**appCallbacks.SetCoreWindowEvents(Window.Current.CoreWindow);**

Sets the core window for Unity, Unity subscribes to the following events (there may be more, depending on when this information was updated) :

* VisibilityChanged
* Closed
* PointerCursor
* SizeChanged
* Activated
* CharacterReceived
* PointerPressed
* PointerReleased
* PointerMoved
* PointerCaptureLost
* PointerWheelChanged
* AcceleratorKeyActivated

**appCallbacks.InitializeD3DXAML();**

This is main initialization function for Unity, it does following things:

* Parse command line arguments, set by AppCallbacks.AddCommandLineArg()
* Initialize DirectX 11 device
* Load first level

At this point, when Unity finishes loading first level, it enters main loop.

Other functions
-----

* **void InvokeOnAppThread(AppCallbackItem item, bool waitUntilDone)**

  Invokes a delegate on application thread, useful when you want to call your script function from UI thread.

* **void InvokeOnUIThread(AppCallbackItem item, bool waitUntilDone)**

  Invokes a delegate on UI thread, useful when you want to invoke something XAML specific API from your scripts.

* **bool RunningOnAppThread()**
  
  Returns true, if you're currently running in application thread.

* **bool RunningOnUIThread()**
  
  Returns true, if you're currently running in UI thread.

* **void InitializeD3DWindow()**
  
  Initialization function for D3D application.

* **void Run()**
  
  Function used by D3D application, for entering main loop.

* **bool IsInitialized()**

  Returns true, when first level is fully loaded.

* **void AddCommandLineArg(string arg)**

  Sets a command line argument for application, must be called before InitializeD3DWindow, InitializeD3DXAML.

* **void SetAppArguments(string arg)** / **string GetAppArguments()**

  Sets application arguments, which can be later accessed from Unity API - **UnityEngine.WSA.Application.arguments**.

* **void LoadGfxNativePlugin(string pluginFileName)**

  This function is obsolete and does nothing.  In previous versions of Unity, this was needed to register native plugins for callbacks such as UnityRenderEvent.  All plugins are now registered automatically.  This function will be removed in a future update.


* **void ParseCommandLineArgsFromFiles(string fileName)**
  
  Parses command line arguments from a file, arguments must be separated by white spaces.

* **bool UnityPause(int pause)**

  Pauses Unity if you pass 1, unpauses if you pass 0, useful if you want to temporary freeze your game, for ex., when your game is snapped.

* **void UnitySetInput(bool enabled)**
  
  Enables/Disables input.

* **bool UnityGetInput()**
  
  Returns true, if Unity will process incoming input.

* **void SetKeyboardTriggerControl(Windows.UI.Xaml.Controls.Control ctrl)**

  Sets the control to be used for triggering on screen keyboard. This control will simply receive focus, when on screen keyboard is requested in scripts. Should be called with control, that does open keyboard on focus.

* **Windows.UI.Xaml.Controls.Control GetKeyboardTriggerControl()**

  Returns control, currently used control for triggering keyboard input. See SetKeyboardTriggerControl.

* **void SetCursor(Windows.UI.Core.CoreCursor cursor)**

  Sets system cursor. The given curosr is set for both CoreWindow and independent input source (if used).

* **void SetCustomCursor(unsigned int id)**

  Sets system cursor to custom. Parameter is cursor resource ID. Cursor is set for both CoreWindow and independent input source (if used).
