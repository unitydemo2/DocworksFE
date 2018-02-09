#WebGL performance considerations

##What kind of performance can you expect on WebGL?

This is a bit difficult to answer, as it depends on many factors. 

In general, you can assume that you will get performance close to native apps for the GPU side, as the WebGL graphics API uses your GPU for hardware accelerated rendering - there is just a little overhead for translating WebGL API calls and shaders to your OS graphics API (typically DirectX on Windows or OpenGL on Mac or Linux).

For the CPU side, all your code is translated into asm.js JavaScript. So what kind of performance you can expect depends a lot on the JavaScript engine of the web browser used, and there are some pretty significant differences there currently. At the point of this writing (November 2015), Microsoft Edge and Mozilla Firefox deliver the best performance on Unity code, as these are currently the only browsers which make use of the asm.js spec to use an optimized AOT compilation path of JavaScript code for that case, which delivers performance within a factor of less then 2x slowdown compared to native code for many programming benchmarks - and that factor also matches results we've seen from different unity content we deployed to WebGL and ran in Firefox and Edge.

There are some other considerations, though. Currently, the JavaScript language does neither support multi-threading, nor SIMD. So, any code which benefits from these features will see bigger slowdowns then other code. You cannot write threading or SIMD code in WebGL in your scripts, but some engine parts are normally multi-threaded or SIMD optimized, and will run less performant on WebGL because of this. An example is the skinning code, which is both multi-threaded and SIMD-optimized. You can use the new timeline [profiler](Profiler) in Unity to see how Unity distributes work to different threads on non-WebGL platforms. Longer term, we are hoping that these features will become available on WebGL as well.


##WebGL-specific settings which affect performance

For best performance, set the optimization level to "Fastest" in the Build Player dialog, and set "Exception support" to "None" in the player settings for WebGL.


##Profiling WebGL

The Unity profiler is supported in WebGL, see [here](Profiler) how to set it up.


##WebGL content in background tabs

If the _Run in background_ is enabled in the [WebGL Player Settings](class-PlayerSettingsWebGL), or if you enable __[Application.runInBackground](ScriptRef:Application-runInBackground.html)__, then your content will continue to run when the canvas or the browser window loses focus.

However, it should be noted that browsers may throttle content running in background tabs. If the tab with your content is not visible, your content will only be updated once a second in most browsers. Note that this will cause __[Time.time](ScriptRef:Time-time.html)__ to progress slower than usual with the default settings, as the default value of __[Time.maximumDeltaTime](ScriptRef:Time-maximumDeltaTime.html)__ is lower than one second.

##Throttling WebGL performance

You may want to run your WebGL content at a lower frame rate in some situations to reduce CPU usage. Like on other platforms, you can use the [Application.targetFrameRate](ScriptRef:Application-targetFrameRate.html) API to do so.

When you don't want to throttle performance, set this API to the default value of -1, rather then to a high value. This allows the browser to adjust the frame rate for the smoothest animation in the browser's render loop, and may produce better results than Unity trying to do its own main loop timing to match a target frame rate.
