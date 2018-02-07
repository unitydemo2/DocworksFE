# Practical guide to optimization for mobiles

This guide is for developers new to mobile game development, who are probably feeling overwhelmed and are either planning and prototyping a new mobile game or porting an existing project to run smoothly on a mobile device. This guide should also be useful as a reference for anyone making mobile games or browser games that target old PCs and netbooks.

Optimization is a broad topic, and how you do it depends a lot on your game. Because of this, this guide is best read as an introduction or reference rather than a step-by-step guide that guarantees a smooth product.

##All mobile devices are not created equal

The information here assumes hardware around the level of the Apple A4 chipset, which is used on the original iPad, the iPhone 3GS, and the third generation iPod Touch. On the Android side, that would mean an Android phone such as the Nexus One, or most phones that run Android 2.3 Gingerbread. Most of these devices were released around early 2010. Out of the app-hungry market, these devices are the older, slower portion, but they should be supported because they represent a large portion of the market. 

For an overview of Apple mobile device tech specs, see documentation on [iPhone hardware](iphone-Hardware). The very low-end Apple mobile devices (such as the iPhone 3G) and the first and second generation iPod Touches are extremely limited, and even more care must be taken to optimize for them. However, there is some question as to whether consumers who have not upgraded their device will be buying apps at all. So, unless you are making a free app, it might not be worthwhile to support the old hardware.

There are much slower and much faster phones out there, and the computational capability of mobile devices is increasing at an extraordinary rate. It's not unheard of for a new generation of a mobile GPU to be five times faster than its predecessor. That's incredibly fast when compared to the PC industry.

##Make optimization a design consideration, not a final step

British computer scientist Michael A. Jackson is often quoted for his rules of program optimization:

_"The first rule of program optimization: don't do it. The second rule of program optimization (for experts only!): don't do it yet."_

His rationale was that, considering how fast computers are and how quickly their speed is increasing, there is a good chance that, if you program something, it will run fast enough. Additionally, if you try to optimize too heavily, you might over-complicate things, limit yourself, or create bugs.

However, if you are developing mobile games, there is another consideration: The hardware that is on the market right now is very limited compared to the computers we are used to working with, so the risk of creating something that simply won't run on the device balances out the risk of over-complication that comes with optimizing from the start.

Throughout this guide, we will try to point out situations where an optimization would help a lot, versus situations where it would just be frivolous.

###Optimization: not just for programmers

Artists also need to know the limitations of the platform, and the methods that are used to get around them, so they can make creative choices that pay off without having to re-produce work.

* More responsibility can fall on the artist if the game design calls for atmosphere and lighting to be drawn into Textures instead of being baked.
* Whenever anything can be baked, artists can produce content for baking instead of real-time rendering. This allows them to ignore technical limitations and work freely.

###Design your game for a smooth runtime

These two pages detail general trends in game performance, and explain how you can best design your game to be optimized or how you can intuitively figure out which things need to be optimized if you've already gone into production.

* [Practical Methods for Optimized Rendering](MobileOptimizationPracticalRenderingOptimizations)
* [Practical Methods for Optimized Scripting and Gameplay](MobileOptimizationPracticalScriptingOptimizations)

##Profile early and often

Profiling is important because it helps you discern which optimizations will pay off with big performance increases and which ones are a waste of your time. Because of the way that rendering is handled on a separate chip (GPU), the time it takes to render a frame is not the time that the CPU takes plus the time that the GPU takes. Instead, it is the longer of the two.

That means that if the CPU is slowing things down, optimizing your Shaders won't increase the frame rate at all, and if the GPU is slowing things down, optimizing physics and scripts won't help at all.

Often, different parts of the game and different situations perform differently as well. This means one part of the game might cause 100 millisecond frames entirely due to a script, and another part of the game might cause the same slowdown but because of something that is being rendered. At the very least, you need to know where all the bottlenecks are if you're going to optimize your game.

###Unity Profiler

You can use the main Profiler in Unity when targeting iOS, Android or Tizen. See documentation on the [Profiler](Profiler) for basic instructions on how to use it.

###Internal profilers

Andriod and iOS both have a built-in internal profiler, which spews out text every 30 frames. It can help you figure out which aspects of your game are slowing things down (such as physics, scripts, or rendering), but it doesn't go into much detail (for example, it can't tell you which script or renderer is the culprit).

* If the profiler indicates that most of your processing time is spent in rendering, see documentation on [Rendering Optimizations](MobileOptimizationPracticalRenderingOptimizations)
* If the profiler indicates that most of your processing time is spent outside of rendering, see documentation on [Scripting Optimizations](MobileOptimizationPracticalScriptingOptimizations)

See documentation on [Internal profilers](iphone-InternalProfiler) for information on how they work and how to turn them on.

###Table of contents

* [Practical Guide to Optimization for Mobiles - Graphics Methods](MobileOptimizationGraphicsMethods)
* [Practical Guide to Optimization for Mobiles - Scripting and Gameplay Methods](MobileOptimizationScriptingMethods)
* [Practical Guide to Optimization for Mobiles - Rendering Optimizations](MobileOptimizationPracticalRenderingOptimizations)
* [Practical Guide to Optimization for Mobiles - Optimizing Scripts](MobileOptimizationPracticalScriptingOptimizations)
