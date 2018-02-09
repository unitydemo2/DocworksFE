# Understanding the managed heap

Another common problem faced by many Unity developers is the unexpected expansion of the managed heap. In Unity, the managed heap expands much more readily than it shrinks. Furthermore, Unity’s garbage collection strategy tends to fragment memory, which can prevent a large heap from shrinking.

## Technical details: how the managed heap operates and why it expands

The "managed heap" is a section of memory that is automatically managed by the memory manager of a Project’s scripting runtime (Mono or IL2CPP). All objects created in managed code must be allocated on the managed heap(2) (__Note:__ Strictly speaking, all non-null reference-typed objects and all boxed value-typed objects must be allocated on the managed heap).

![](../uploads/Main/Understanding%20Performance%20in%20Unity%20-%20Asset%20Auditing%20Section_image_0.png)

In the above diagram, the white box represents a quantity of memory apportioned to the managed heap, and the colored boxes within it represent data values stored within the managed heap’s memory space. When additional values are needed, more space is allocated from within the managed heap.

The garbage collector runs periodically(3) (__Note:__ The exact timing is platform-dependent). This sweeps through all objects on the heap, marking for deletion any objects that are no longer referenced. Unreferenced objects are then deleted, freeing up memory.

Crucially, Unity’s garbage collection – which uses the [Boehm GC algorithm](https://en.wikipedia.org/wiki/Boehm_garbage_collector) – is non-generational and non-compacting. "Non-generational" means that the GC must sweep through the entire heap when performing a collection pass, and its performance therefore degrades as the heap expands. “Non-compacting” means that objects in memory are not relocated in order to close gaps between objects.

![](../uploads/Main/Understanding%20Performance%20in%20Unity%20-%20Asset%20Auditing%20Section_image_1.png)

The above diagram shows an example of memory fragmentation. When an object is released, its memory is freed. However, the freed space does **not** become part of a single large pool of "free memory". The objects on either side of the freed object may still be in use. Because of this, the freed space is a “gap” between other segments of memory (this gap is indicated by the red circle in the diagram). The newly-freed space can therefore only be used to store data of identical or lesser size than the freed object.

When allocating an object, remember that the object must always occupy a contiguous block of space in memory.

This leads to the core problem of memory fragmentation: while the overall amount of space available in the heap may be substantial, it is possible that some or all of that space is in small "gaps" between allocated objects. In this case, even though there may be enough total space to accommodate a certain allocation, the managed heap cannot find a large enough block of contiguous memory in which to fit the allocation.

![](../uploads/Main/Understanding%20Performance%20in%20Unity%20-%20Asset%20Auditing%20Section_image_2.png)

However, if a large object is allocated and there is insufficient contiguous free space to accommodate the object, as illustrated above, the Unity memory manager performs two operations.

First, if it has not already done so, the garbage collector runs. This attempts to free up enough space to fulfill the allocation request.

If, after the GC runs, there is still not enough contiguous space to fit the requested amount of memory, the heap must expand. The specific amount that the heap expands is platform-dependent; however, most Unity platforms double the size of the managed heap.

## Key problems with the heap

The core issues with managed heap expansion are twofold:

* Unity does not often release the memory pages allocated to the managed heap when it expands; it optimistically retains the expanded heap, even if a large portion of it is empty. This is to prevent the need to re-expand the heap should further large allocations occur.

* On most platforms, Unity eventually releases the pages used by empty portions of the managed heap back to the operating system. The interval at which this occurs is not guaranteed and should not be relied upon.

* The address space used by the managed heap is never returned to the operating system.

* For 32-bit programs, this can lead to address space exhaustion if the managed heap expands and contracts many times. If a program’s available memory address space is exhausted, the operating system will terminate the program.

* For 64-bit programs, the address space is sufficiently large that this is extremely unlikely to occur for programs whose running time does not exceed the average human lifespan.

## Temporary allocations

Many Unity projects are found to operate with several tens or hundreds of kilobytes of temporary data being allocated to the managed heap each frame. This is often extremely detrimental to a project’s performance. Consider the following math:

If a program allocates one kilobyte (1kb) of temporary memory each frame, and is running at 60 frames per second, then it must allocate 60 kilobytes of temporary memory per second. Over the course of a minute, this adds up to 3.6 megabytes of garbage in memory. Invoking the garbage collector once per second is likely to be detrimental to performance, but allocating 3.6 megabytes per minute is problematic when attempting to run on low-memory devices.

Further, consider loading operations. If a large number of temporary objects are generated during a heavy Asset-loading operation, and those objects are referenced until the operation completes, then the garbage collector is unable to release those temporary objects and the managed heap needs to expand – even though many of the objects it contains will be released a short time later.

![](../uploads/Main/Understanding%20Performance%20in%20Unity%20-%20Asset%20Auditing%20Section_image_3.png)

Keeping track of managed memory allocations is relatively simple. In Unity’s CPU Profiler, the Overview has a "GC Alloc" column. This column displays the number of bytes allocated on the managed heap in a specific frame (4) (__Note:__ Note that this is not identical to the number of bytes temporarily allocated during a given frame. The profile displays the number of bytes allocated in a specific frame, even if some/all of the allocated memory is reused in subsequent frames). With the “Deep Profiling” option enabled, it’s possible to track down the method in which these allocations occur.

Note that some script methods cause allocations when running in the Editor, but do not produce allocations after the project has been built. `GetComponent` is the most common example; this method always allocates when executed in the Editor, but not in a built project.

In general, it is strongly recommended that all developers minimize managed heap allocations whenever the project is in an interactive state. Allocations during non-interactive operations, such as Scene loading, are less problematic.

## Basic memory conservation
There are a handful of relatively simple techniques that can be employed to reduce managed heap allocations.

### Collection and array reuse

When using C#’s Collection classes or Arrays, consider reusing or pooling the allocated Collection or Array whenever possible. The Collection classes expose a *Clear* method which eliminates the Collection’s values but does not release the memory allocated to the Collection.

```

void Update() {

	List<float> nearestNeighbors = new List<float>();

	findDistancesToNearestNeighbors(nearestNeighbors);

	nearestNeighbors.Sort();

	// … use the sorted list somehow …

}

```

This is particularly useful when allocating temporary "helper" Collections for complex computations. A very simple example might be the following code:

In this example, the `nearestNeighbors` List is allocated once per frame in order to collect a set of data points. It’s very simple to hoist this List out of the method and into the containing class, which avoids allocating a new List each frame:

```

List<float> m_NearestNeighbors = new List<float>();

void Update() {

	m_NearestNeighbors.Clear();

	findDistancesToNearestNeighbors(NearestNeighbors);

	m_NearestNeighbors.Sort();

	// … use the sorted list somehow …

}

```


In this version, the List’s memory is retained and reused across multiple frames. New memory is only allocated when the List needs to expand.

## Closures and anonymous methods

There are two points to consider when using closures and anonymous methods.

First, all method references in C# are reference types, and are therefore allocated on the heap. Temporary allocations can be easily created by passing a method reference as an argument. This allocation occurs regardless of whether the method being passed is an anonymous method or a predefined one.

Second, converting an anonymous method to a closure significantly increases the amount of memory required to pass the closure to method receiving it.


Consider the following code:

```

List<float> listOfNumbers = createListOfRandomNumbers();

listOfNumbers.Sort( (x, y) =>

(int)x.CompareTo((int)(y/2)) 

);

```

This snippet uses a simple anonymous method to control the sorting order of the list of numbers created on the first line. However, if a programmer wished to make this snippet reusable, it is tempting to substitute the constant `2` for a variable in local scope, like so:

```

List<float> listOfNumbers = createListOfRandomNumbers();

int desiredDivisor = getDesiredDivisor();

listOfNumbers.Sort( (x, y) =>

(int)x.CompareTo((int)(y/desiredDivisor))

);

```

The anonymous method now requires the method to be able to access the state of a variable outside of the method’s scope, and so has become a closure. The `desiredDivisor` variable must be passed into the closure somehow so that it can be used by the actual code of the closure.

To do this, C# generates an anonymous class that can retain the externally-scoped variables needed by the closure. A copy of this class is instantiated when the closure is passed to the `Sort` method, and the copy is initialized with the value of the `desiredDivisor` integer.

Because executing the closure requires instantiation of a copy of its generated class, and all classes are reference types in C#, then executing the closure requires allocation of an object on the managed heap.

In general, it is best to avoid closures in C# whenever possible. Anonymous methods and method references should be minimized in performance-sensitive code, and especially in code that executes on a per-frame basis.

### Anonymous methods under IL2CPP

Currently, inspection of code generated by IL2CPP reveals that the simple declaration and assignment of a variable of type `System.Function` allocates a new object. This is true whether the variable is explicit (declared in a method/class) or implicit (declared as an argument to another method).

As such, any use of anonymous methods under the IL2CPP scripting backend allocates managed memory. This is not the case under the Mono scripting backend.

Furthermore, IL2CPP displays dramatically different levels of managed memory allocation depending on the way in which a method argument is declared. Closures, as expected, allocate the most memory per call.

Unintuitively, predefined methods allocate __nearly as much memory as closures__ when passed as arguments under the IL2CPP scripting backend. Anonymous methods generate the least amount of transient garbage on the heap, by one or more orders of magnitude.

Therefore, if a project is intended to ship on the IL2CPP scripting backend, there are three key recommendations:

* Prefer coding styles that do not require passing methods as arguments.

* When unavoidable, prefer anonymous methods over predefined methods.

* Avoid closures, regardless of scripting backend.

## Boxing

Boxing is one of the most common sources of unintended temporary memory allocations found in Unity projects. It occurs whenever a value-typed value is utilized as a reference type; this most often occurs when passing primitive value-typed variables (such as `int` and `float`) to object-typed methods.

In this extremely simple example, the integer in *x* is boxed in order to be passed to the `object.Equals` method, because the `Equals` method on `object` requires that an `object` be passed to it.

```

int x = 1;

object y = new object();

y.Equals(x);

```

C# IDEs and compilers generally do not issue warnings about boxing, even though it leads to unintended memory allocations. This is because the C# language was developed with the assumption that small temporary allocations would be efficiently handled by generational garbage collectors and allocation-size-sensitive memory pools.

While Unity’s allocator does use different memory pools for small and large allocations, Unity’s garbage collector is `not` generational and therefore cannot efficiently sweep out the small, frequent temporary allocations generated by boxing.

Boxing should be avoided wherever possible when writing C# code for Unity runtimes.

### Identifying boxing

Boxing shows up in CPU traces as calls to one of a few methods, depending on the scripting backend in use. These generally take one of the following forms, where `<some class>` is the name of some other class or struct, and `…` is some number of arguments:

* `<some class>::Box(…)`

* `Box(…)`

* `<some class>_Box(…)`

It can also be located by searching the output of a decompiler or IL viewer, such as the IL viewer tool built into ReSharper or the dotPeek decompiler. The IL instruction is "box".

### Dictionaries and enums

One common cause of boxing is the use of `enum` types as keys for Dictionaries. Declaring an `enum` creates a new value type that is treated like an integer behind the scenes, but enforces type-safety rules at compile time.

By default, a call to `Dictionary.add(key, value)` results in a call to `Object.getHashCode(Object)`. This method is used to obtain the appropriate hash code for the Dictionary’s key, and is used in all methods that accept a key: `Dictionary.tryGetValue, Dictionary.remove`, etc.

The `Object.getHashCode` method is reference-typed, but `enum` values are always value types. Therefore, for enum-keyed Dictionaries, every method call results in the key being boxed at least once.


The following code snippet illustrates a simple example that demonstrates this boxing problem:

```

enum MyEnum { a, b, c };

var myDictionary = 

new Dictionary<MyEnum, object>();

myDictionary.Add(MyEnum.a, new object());

```

To solve this problem, it is necessary to write a custom class that implements the `IEqualityComparer` interface and assign an instance of that class as the Dictionary’s comparer (__Note:__ This object is usually stateless, and therefore can be reused with different Dictionary instances to save memory). 
	 
The following is a simple example of an IEqualityComparer for the above code snippet.

```

public class MyEnumComparer : IEqualityComparer<MyEnum> {

	public bool Equals(MyEnum x, MyEnum y) {

		return x == y;

	}

	public int GetHashCode(MyEnum x) {

		return (int)x;

	}

}

```

An instance of the above class could be passed to the Dictionary’s constructor. 

### Foreach loops

In Unity’s version of the Mono C# compiler, use of the `foreach` loop forces Unity to box a value each time the loop terminates (__Note:__ The value is boxed once each time the loop as a whole finishes executing. It does not box once per iteration of the loop, so memory usage remains the same regardless of whether the loop runs two times or 200 times). This is because the IL generated by Unity’s C# compiler constructs a generic value-type Enumerator in order to iterate over the value collection. 

This Enumerator implements the `IDisposable` interface, which must be called when the loop terminates. However, calling interface methods on value-typed objects (such as structs and Enumerators) requires boxing them.


Examine the following very simple example code:

```

int accum = 0;

foreach(int x in myList) {

	accum += x;

}

```

The above, when run through Unity’s C# compiler, produces the following Intermediate Language:

```

   .method private hidebysig instance void 

    ILForeach() cil managed 

  {

    .maxstack 8

    .locals init (

      [0] int32 num,

      [1] int32 current,

      [2] valuetype [mscorlib]System.Collections.Generic.List`1/Enumerator<int32> V_2

    )

    // [67 5 - 67 16]

    IL_0000: ldc.i4.0     

    IL_0001: stloc.0      // num

    // [68 5 - 68 74]

    IL_0002: ldarg.0      // this

    IL_0003: ldfld        class [mscorlib]System.Collections.Generic.List`1<int32> test::myList

    IL_0008: callvirt     instance valuetype [mscorlib]System.Collections.Generic.List`1/Enumerator<!0/*int32*/> class [mscorlib]System.Collections.Generic.List`1<int32>::GetEnumerator()

    IL_000d: stloc.2      // V_2

    .try

    {

      IL_000e: br           IL_001f

    // [72 9 - 72 41]

      IL_0013: ldloca.s     V_2

      IL_0015: call         instance !0/*int32*/ valuetype [mscorlib]System.Collections.Generic.List`1/Enumerator<int32>::get_Current()

      IL_001a: stloc.1      // current

    // [73 9 - 73 23]

      IL_001b: ldloc.0      // num

      IL_001c: ldloc.1      // current

      IL_001d: add          

      IL_001e: stloc.0      // num

    // [70 7 - 70 36]

      IL_001f: ldloca.s     V_2

      IL_0021: call         instance bool valuetype [mscorlib]System.Collections.Generic.List`1/Enumerator<int32>::MoveNext()

      IL_0026: brtrue       IL_0013

      IL_002b: leave        IL_003c

    } // end of .try

    finally

    {

      IL_0030: ldloc.2      // V_2

      IL_0031: box          valuetype [mscorlib]System.Collections.Generic.List`1/Enumerator<int32>

      IL_0036: callvirt     instance void [mscorlib]System.IDisposable::Dispose()

      IL_003b: endfinally   

    } // end of finally

    IL_003c: ret          

  } // end of method test::ILForeach

} // end of class test

```

The most relevant code is the `__finally { … }__` block near the bottom. The `callvirt` instruction discovers the location of the `IDisposable.Dispose` method in memory before invoking the method, and requires that the Enumerator be boxed.

In general, `foreach` loops should be avoided in Unity. Not only do they box, but the method-call cost of iterating over collections via Enumerators is generally much slower than manual iteration via a `for` or `while` loop.

Note that the C# compiler upgrade in Unity 5.5 significantly improves Unity’s ability to generate IL. In particular, the boxing operations has been eliminated from `foreach` loops. This eliminates the memory overhead associated with `foreach` loops. However, the CPU performance difference compared to equivalent Array-based code remains, due to method-call overhead.

### Array-valued Unity APIs

A more pernicious and less-visible cause of spurious array allocation is the repeated accessing of Unity APIs that return arrays. All Unity APIs that return arrays create a new copy of the array each time they are accessed. It is extremely non-optimal to access an array-valued Unity API more often than necessary.

As an example, the following code spuriously creates four copies of the `vertices` array per loop iteration. The allocations are occur each time the `.vertices` property is accessed.

```

for(int i = 0; i < mesh.vertices.Length; i++)

{

	float x, y, z;

	x = mesh.vertices[i].x;

	y = mesh.vertices[i].y;

	z = mesh.vertices[i].z;

	// ...

	DoSomething(x, y, z);	

}

```

This can be trivially refactored into a single array allocation, regardless of the number of loop iterations, by capturing the `vertices` array before entering the loop:

```

var vertices = mesh.vertices;

for(int i = 0; i < vertices.Length; i++)

{

	float x, y, z;

	x = vertices[i].x;

	y = vertices[i].y;

	z = vertices[i].z;

	// ...

	DoSomething(x, y, z);	

}

```


While the CPU cost of accessing a property once is not very high, repeated accesses within tight loops create CPU performance hotspots. Further, repeated accesses unnecessarily expand the managed heap.

This problem is extremely common on mobile, because the `Input.touches` API behaves similarly to the above. It is extremely common for projects to contain code similar to the following, where an allocation occurs each time the `.touches` property is accessed.

```

for ( int i = 0; i < Input.touches.Length; i++ )

{

   Touch touch = Input.touches[i];

    // …

}

```


This can, of course, be trivially improved by hoisting the array allocation out of the loop condition:

```

Touch[] touches = Input.touches;

for ( int i = 0; i < touches.Length; i++ )

{

   Touch touch = touches[i];

   // …

}

```


However, there are now versions of many Unity APIs that do not cause memory allocations. These should generally be favored, when they’re available. 

```

int touchCount = Input.touchCount;

for ( int i = 0; i < touchCount; i++ )

{

   Touch touch = Input.GetTouch(i);

   // …

}

```



Converting the above example to the allocation-less Touch API is simple:

Note that the property access (`Input.touchCount`) is still kept outside the loop condition in order to save the CPU cost of invoking the property’s `get` method.

### Empty array reuse

Some teams prefer to return empty arrays instead of `null` when an array-valued method needs to return an empty set. This coding pattern is common in many managed languages, particularly C# and Java.

In general, when returning a zero-length array from a method, it is considerably more efficient to return a pre-allocated singleton instance of the zero-length array than to repeatedly create empty arrays(5) (__Note:__ Naturally, an exception should be made when the array is resized after being returned).

__Footnotes__

* __(1)__ This is because, on most platforms, readback from GPU memory is extremely slow. Reading a Texture from GPU memory into a temporary buffer for use by CPU code (e.g. `Texture.GetPixel`) would be very nonperformant.

* __(2)__ Strictly speaking, all non-null reference-typed objects and all boxed value-typed objects must be allocated on the managed heap.

* __(3)__ The exact timing is platform-dependent.

* __(4)__ Note that this is **not** identical to the number of bytes temporarily allocated during a given frame. The profile displays the number of bytes allocated in a specific frame, even if some/all of the allocated memory is reused in subsequent frames.

* __(5)__ Naturally, an exception should be made when the array is resized after being returned.
