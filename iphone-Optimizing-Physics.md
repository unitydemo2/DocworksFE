Optimizing Physics Performance
==============================

The NVIDIA PhysX physics engine used by Unity is available on iOS but the performance limits of the hardware will be reached more easily on mobile platforms than desktops.

Here are some tips for tuning physics to get better performance on iOS:-

* You can adjust the __Fixed Timestep__ setting (in the [Time manager](class-TimeManager)) to reduce the time spent on physics updates. Increasing the timestep will reduce the CPU overhead at the expense of the accuracy of the physics. Often, lower accuracy is an acceptable tradeoff for increased speed.
* Set the __Maximum Allowed Timestep__ in the [Time manager](class-TimeManager) in the 8-10fps range to cap the time spent on physics in the worst case scenario.
* Mesh colliders have a much higher performance overhead than primitive colliders, so use them sparingly. It is often possible to approximate the shape of a mesh by using child objects with primitive colliders. The child colliders will be controlled collectively as a single compound collider by the rigidbody on the parent.
* While wheel colliders are not strictly colliders in the sense of solid objects, they nonetheless have a high CPU overhead.

The total amount of physics calculation depends on the number of non-sleeping rigid bodies and colliders in the scene and the complexity of the colliders. You can keep track of how many physics objects there are in the scene using the [internal profiler](iphone-InternalProfiler).
