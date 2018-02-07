#Memory Considerations when targeting WebGL

Memory in Unity WebGL can be a constraining factor restricting the complexity of the content you can run, so we would like to provide some explanation on how memory is used in WebGL. 

Your WebGL content will run inside a browser, so any memory has to be allocated by the browser within the browser's memory space. The amount of available memory can vary a lot depending on the browser, OS and device used. Determining factors include whether the browser is a 32 or 64 bit process, whether the browser uses separate processes for each tab or has your content share a memory space with all other open tabs, and how much memory the browser's JavaScript engine requires to parse your code.

There are multiple areas where Unity WebGL content will require the browser to allocate significant amounts of memory:

Unity Heap
----------

This is the memory Unity uses to store all it's state, managed and native objects and currently loaded assets and scenes. This is similar to the memory used by Unity players on any other platform. You can configure the size of this in the Unity WebGL player settings (But for faster iteration, you can also edit the TOTAL_MEMORY value written to the generated html file). You can use the Unity Profiler to profile and sample the contents of this memory. This memory will be created as a TypedArray of bytes in JavaScript code, and requires the browser be able to allocate a consecutive block of memory of this size. You will want this space to be as small as possible (so that the browser will be able to allocate it even if memory is fragmented), but large enough to fit all the data required to play any scene of your content.

Asset Data
----------

When you create a Unity WebGL build, Unity will write out a .data file containing all the scenes and assets needed for your content. Since WebGL does not have a real file system, this file will be downloaded before your content can start, and the uncompressed data will be kept in a consecutive block of browser memory for the whole time your content is run. So, to keep both download times and memory usage low, you should try to keep this data as small as possible. See the documentation page on [Reducing File size](ReducingFilesize) for information on how to optimize the build size of your assets.

Another thing you can do to reduce load times and the amount of memory used for assets is to pack your asset data into [AssetBundles](AssetBundlesIntro). By doing so, you get full control of when your assets need to be downloaded, and you can unload them when you no longer need them, which will free any memory used by them. Note that AssetBundles will be loaded directly into the Unity heap and will not result in additional allocations by the browser (unless you use Asset Bundle Caching using __[WWW.LoadFromCacheOrDownload](ScriptRef:WWW.LoadFromCacheOrDownload.html)__, which is using a memory-mapped Virtual File System, backed by the browser's IndexedDB).

Memory needed to parse the code
-------------------------------

Another issue related to memory is the memory required by the browser's JavaScript engine. Unity will emit very large files of millions of lines of generated JavaScript code, which is an order of magnitude larger than common uses of JavaScript code in browsers. Some JavaScript engines may allocate some rather large data structures to parse and optimize this code, which may results in memory spikes of up to several Gigabytes of memory when loading the content in some cases. We expect that future technologies like WebAssembly will eventually eliminate this problem, but until then, the best advise we can give is to do what you can to keep the size of the emitted code low. See the comments on distribution size [here](webgl-building) for more information on how to do that.

Dealing with memory issues
--------------------------

When you see an error related to memory in a Unity WebGL build, it is important to understand whether it is the browser which is failing to allocate memory or if the Unity WebGL runtime is failing to allocate a free block of memory within the pre-allocated block of the Unity heap. If the browser is failing to allocate memory, then it may help to try to reduce the size used by one or more of the memory areas above (for instance by reducing the size of the Unity heap). On the other hand, if the Unity runtime is failing to allocate a block inside the Unity heap, you may want to increase the size of that instead.

Unity will try to interpret error messages to tell which of the two it is (and provide suggestions on what to do). Since different browsers may report different messages, that is not always easy, however, and we may not be interpreting all of them. When you see a generic "Out of memory" error from the browser, it is likely to be an issue of the browser running out of memory (where you might want to use a smaller Unity heap). Also, you may sometimes see browsers simply crashing when loading Unity content without showing a human-parseable error message. This can have many reasons, but is frequently caused by JavaScript engines requiring too much memory to parse and optimize the generated code.

###Large-Allocation Http Header

Your server can emit the [Large-Allocation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Large-Allocation) http header for your content. This tells supported browsers (currently only Firefox) about your memory needs, allowing them to spawn a new process with an unfragmented memory space, or to perform other housekeeping to make sure that the large allocation succeeds. This can solve issues where the browser runs out of memory when trying to allocate the Unity heap, especially on 32-bit browsers.

Garbage Collection considerations
---------------------------------

When you allocate managed objects in Unity, they will need to be garbage collected when they are no longer used. See our documentation on [automatic memory management](UnderstandingAutomaticMemoryManagement) for more information. In WebGL, this is the same. Managed, garbage collected memory is allocated inside the Unity heap.

One distinction in WebGL, however, concerns the points in time when garbage collection (GC) can take place. To perform garbage collection, the GC would normally need to pause all running threads and inspect their stacks and registers for loaded object references. This is not currently possible in JavaScript. For this reason, the GC will only run in WebGL in situations where the stack is known to be empty (which is currently once after every frame). This is not a problem for most content which deals with managed memory conservatively and has relatively few GC allocations within each frame (you can debug this using the Unity profiler). 

However, if you had code like the following:

```
string hugeString = "";

for (int i = 0; i < 100000; i++)
{
	hugeString += "foo";
}
```

, then this code would fail running on WebGL, as it would not get a chance to run the GC between iterations of the loop, to free up memory used by all the intermediate string objects - which would eventually cause it to run out of memory in the Unity heap.


