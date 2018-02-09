##Physics in Unity 5.0

Unity 5.0 features an upgrade to PhysX3.3 SDK. Please give this blogpost a quick look before taking any action on your 4.x projects. It should give you a taste of what to expect from the new codebase: [High Performance Physics in Unity 5](http://blogs.unity3d.com/2014/07/08/high-performance-physics-in-unity-5/).
Please be warned that PhysX3 is not 100% compatible with PhysX2 and requires some actions from the user when upgrading.

###General overview of updates

Unity 5.0 physics could be expected to work up to 2x faster than in previous versions. Most of the components you were familiar with are still there, and you will find them working as before. Of course, some behaviours were impossible to get the same and some were just weird behaviours caused by limitations of the pre-existed codebase, so we had to take changes. The two areas that got the most significant change are Cloth component and WheelCollider component. We're including a section about each of them below. Then, there are smaller changes all over the physics code that cause incompatibility. 

###Changes that are likely to affect projects:

####Adaptive force is now switched off by default
Adaptive force was introduced to help with the simulation of large stacks, but it turned out to be great only for demos. In real games it happened to cause wrong behaviour. You can switch it on in the editor physics properties: Edit -> Project settings -> Physics -> Enable adaptive force.

####Smooth sphere collisions are removed both from terrain and meshes.
PhysX3 has the feature that addresses the same issue and it's no longer switchable as it's considered to be a solution without major drawbacks.

####Springs expose larger amplitudes with PhysX3.
you may want to tune spring parameters after upgrading.

####Setting Terrain Physics Material has changed
Use TerrainCollider.sharedMaterial and TerrainCollider.material to specify physics material for terrain. The older way of setting physics material through the TerrainData will no longer work. As a bonus, you can now specify terrain physics materials on a per collider basis.

####Shape casting and sweeping has changed:
- Shape sweeps report all shapes they hit (i.e CapsuleCast and SphereCast would return all shapes they hit, even the ones that fully contain the primitive)
- Raycasts filter out shapes that contain the raycast origin

####Compound Collider events:
When using compound colliders, OnCollisionEnter is now called once per each contact pair

####Triggers must be convex:
From now on, you can have triggers only on convex shapes (a PhysX restriction):

- TerrainCollider no longer supports IsTrigger flag
- MeshCollider can have IsTrigger only if it's convex

####Dynamic bodies must be convex:
Dynamic bodies (i.e. those having Rigidbody attached with Kinematic = false) can no longer have concave mesh colliders (a PhysX limitation).

If you want to have collisions with concave meshes, you can only have them on static colliders and kinematic bodies

####Ragdoll joints:
Joint setups for ragdolls will likely need tweaking. 

These suggestions apply to joints in general as well.

See the [Joint And Ragdoll Stability](RagdollStability) page for most recent version of this guide.

- Avoid small angles of "Angular Y Limit" and "Angular Z Limit". Depending on your setup the minimum angles should be around 5 to 15 degrees in order to be stable. Instead of using a small angle try setting the angle to zero. This will lock the axis and provide a stable simulation.

- Set "Enable Preprocessing" to false (unchecked). Disabling the preprocessing can help against joints "blowing up". Joints can "blow up" if they are forced into situations where there is no possible way to satisfy the joint constraints. This can occur if jointed rigid bodies are pulled apart by static collision geometry, like spawning a ragdoll partially inside a wall.

- Ragdoll stability or stretching: If ragdolls are given extreme circumstances, such as spawning partially inside a wall or pushed with a large force, the joint solver will be unable to keep the rigid bodies together. This can result in stretching or a "cloud of body parts". Please enable projection on the joints, using either "ConfigurableJoint.projectionMode" or "CharacterJoint.enableProjection".

- If bodies connected with joints are jittering try increase Edit->Project Settings->Physics->"Solver Iteration Count". Try between 10 or 20.

- Never use direct transform access with kinematic bodies jointed to other bodies. Doing so skips the step where PhysX computes internal velocities of corresponding bodies and thus makes solver provide unpleasant results. We've seen some 2D projects using direct transform access to flip characters via altering transform.direction on the root boon of the rig. This behaves much better if you use MovePosition / MoveRotation / Move instead.

####Rigidbody's constraints are applied in local space.

The locking mechanism we used in Unity 4 was basically discarding changes to locked rotations & was resetting the angular speeds as a post-solver step. This was working mostly fine except that there were issues with bodies failing to go asleep as the solver wanted to adjust the rotations every frame; and a few related cases were noticed over the years. When working on PhysX3 integration we utilised this new cool feature of PhysX 3.3 where we can set the infinite inertia tensor components for locked rotational degrees of freedom. This is now supported in the solver so the body would now go to sleep appropriately, but since this is inertia, it is applied in local coordinates.

####WheelCollider

 The new WheelCollider is powered by the PhysX3 Vehicles SDK that is basically a completely new vehicle simulation library when compared to the code we had with PhysX2. 
 
[Read more about the new WheelCollider here](WheelColliderTutorial).

####Cloth

Unity 5 uses the completely rewritten cloth solver provided by the new PhysX SDK. This cloth solver has been designed with character clothing in mind, and is a great improvement compared to the old version in terms of performance and stability. Unity 5 replaces the SkinnedCloth and InteractiveCloth components in Unity 4 with a single Cloth component, which works in conjunction with a SkinnedMeshRenderer. The functionality is similar to the previous SkinnedCloth component, but it is now possible to assign arbitrary, non-skinned meshes to the SkinnedMeshRenderer, so you can still handle cloth simulation on any random mesh.

However, some functionality which was available on the old InteractiveCloth is now no longer supported by the new version of PhysX as it is difficult to implement these with good performance. Specifically:

 - you can no longer use cloth to collide with arbitrary world geometry
 - tearing is no longer supported
 - you can no longer apply pressure on cloth
 - you can no longer attach cloth to colliders or have cloth apply forces to rigidbodies in the scene.



