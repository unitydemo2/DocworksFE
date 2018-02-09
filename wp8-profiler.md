Windows Phone 8: Profiler
=========================


One of the simplest ways to profile Windows Phone 8 app is over WiFi. Build your app with Development Build enabled in Build Settings (or choose Debug or Release configuration if you're building from Visual Studio). Deploy and run the app. Open Profiler window in Unity and select WP8Player from Active Profiler menu. Incoming data will appear on the screen. Please keep in mind that GPU profiling is not yet support on Windows Phone 8 platform.

Troubleshooting
---------------


If WP8Player option doesn't appear in Active Profiler menu you can try connecting directly to the phone by manually specifying IP address. Also make sure that Unity Editor is not blocked by the firewall. Profiler might also not work if connected to the public network.
