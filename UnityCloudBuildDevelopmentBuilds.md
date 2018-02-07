# Development builds

Unity Cloud Build builds your projects for release by default. To create a development build, go to the build target’s __Advanced Options__. (See documentation on accessing and editing [Advanced Options](UnityCloudBuildAdvancedOptions).)



![The Edit Advanced Options screen](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsEdit.png)

Check the __Development Builds__ box. When enabled, this sets two flags in the `BuildOptions` API:

* `Development`: A development build includes debug symbols and enables the Profiler.

* `AllowDebugging`: Allow script debuggers to attach to the player remotely.

Note that to profile a web player build, you need to have the development version of the web player installed. You can only profile the .unity3d file when the development web player build is active. See documentation on the [Profiler window](Profiler) for more information on profiling your development build.