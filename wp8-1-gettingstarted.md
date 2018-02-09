Windows Phone 8.1: Getting Started
================================

Windows Phone 8.1 brings many changes to Unity for Windows Phone. Due to the convergence effort, Windows Phone 8.1 is considered to be a part of Windows Store Apps family, rather than being an extension to Windows Phone 8. As such, it behaves much  more like Windows Store Apps behave on Unity.

Here are some of the bigger changes that Windows Phone 8.1 brought to Unity:

  * As in Windows Store applications, scripts may now be compiled with Microsoft C# compiler, which means one can access phone specific APIs in scripts. For more info, check FAQ.
  
  * For Windows Phone 8.1 projects, preprocessor define UNITY_WP8 is not defined anymore. These preprocessor defines are present: UNITY_METRO, UNITY_WP_8_1, UNITY_WINRT, UNITY_WINRT_8_1. When compiling scripts with
  Microsoft C# compiler, additionally NETFX_CORE is defined as well.

  * Building Windows Phone 8.1 project is located under "Windows Store" platform. To build a Windows Phone 8.1 application, select "Phone 8.1" SDK.

  * In addition, UnityEngine.WSA namespace is available to Windows Phone 8.1 games, while UnityEngine.WindowsPhone is not anymore.
  
  * Unity exposes a way to build Universal Windows Store/Phone 8.1 applications, through selecting "Universal 8.1" SDK in build window. Upon building such a project, Unity creates a Universal Visual Studio project, which then can be built to both Windows and Windows Phone devices.
  

Prerequisites
-------------

In order to build applications for Windows Phone 8.1, Visual Studio 2013 installation with Windows Phone 8.1 support is required.
