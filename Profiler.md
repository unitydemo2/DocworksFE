Profiler overview
========


The Unity Profiler Window helps you to optimize your game. It reports for you how much time is spent in the various areas of your game. For example, it can report the percentage of time spent rendering, animating or in your game logic.

You can analyze the performance of the GPU, CPU, memory, rendering, and audio.

To see the profiling data, you play your game in the Editor with Profiling on, and it records performance data. The Profiler window then displays the data in a timeline, so you can see the frames or areas that spike (take more time) than others. By clicking anywhere in the timeline, the bottom section of the Profiler window will display detailed information for the selected frame.

Note that profiling has to instrument your code (that is; add some instructions to facilitate the check). While this  has a small impact on the performance of your game, the overhead is small enough to not affect the game framerate. 

##Tips on using the Tool
When using the profiling tool, focus on those parts of the game that consume the most time. Compare profiling results before and after code changes and determine the improvements you measure. Sometimes changes you make to improve performance might have a negative effect on frame rate; there may be unexpected consequences of your code optimization. 

See  [Profiler window](ProfilerWindow) documentation for details of the Profiler window.

See also: [Optimizing Graphics Performance](OptimizingGraphicsPerformance).


