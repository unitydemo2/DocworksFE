#Getting started with WebGL development

##What is Unity WebGL?

The WebGL build option allows Unity to publish content as JavaScript programs which use HTML5 technologies and the WebGL rendering API to run Unity content in a web browser. To build and test your content for WebGL, choose the WebGL build target in the __Build Player__ window, and click __Build & Run__.

##Technical overview

To run in WebGL, all code needs to be JavaScript. We use the emscripten compiler toolchain to cross-compile the Unity runtime code (written in C and C++) into asm.js JavaScript. asm.js is a very optimizable subset of JavaScript which allows JavaScript engines to AOT-compile asm.js code into very efficient native code.

To convert the .NET game code (your C# and UnityScript scripts) into JavaScript, we use a technology called [IL2CPP](IL2CPP). IL2CPP takes .NET bytecode and converts it to corresponding C++ source files, which is then compiled using emscripten to convert your scripts to JavaScript.

##Platform support

Unity WebGL content is supported in the current versions of most major browsers on the desktop, however there are [differences in the level of support](webgl-browsercompatibility) offered by the different browsers. Mobile devices are not supported by Unity WebGL.

Not all features of Unity are available in WebGL builds, mostly due to constraints of the platform. Specifically:

* Threads are not supported due to the lack of threading supporting in JavaScript. This applies to both Unity's internal use of threads to speed up performance, and to the use of threads in script code and managed dlls. Essentially, anything in the `System.Threading` namespace is not supported.

* WebGL builds cannot be debugged in MonoDevelop or Visual Studio. See: [Debugging and trouble shooting WebGL builds](webgl-debugging).

* Browsers do not allow direct access to IP sockets for networking, due to security concerns. See: [WebGL Networking](webgl-networking).

* The WebGL graphics API is equivalent to OpenGL ES 2.0 and 3.0, which has some limitations. See: [WebGL Graphics](webgl-graphics).

* WebGL builds use a custom backend for Audio, based on the __Web Audio__ API. This supports only basic audio functionality. See: [Using Audio in WebGL](webgl-audio).

* WebGL is an AOT platform, so it does not allow dynamic generation of code using `System.Reflection.Emit`. This is the same on all other IL2CPP platforms, iOS, and most consoles.
