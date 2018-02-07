Rigidbody
=========


__Rigidbodies__ enable your __GameObjects__ to act under the control of physics. The Rigidbody can receive forces and torque to make your objects move in a realistic way. Any GameObject must contain a Rigidbody to be influenced by gravity, act under added forces via scripting, or interact with other objects through the NVIDIA PhysX physics engine.


![](../uploads/Main/Inspector-Rigidbody.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Mass__ |The mass of the object (in kilograms by default). |
|__Drag__ |How much air resistance affects the object when moving from forces. 0 means no air resistance, and infinity makes the object stop moving immediately. |
|__Angular Drag__ |How much air resistance affects the object when rotating from torque. 0 means no air resistance. Note that you cannot make the object stop rotating just by setting its Angular Drag to infinity. |
|__Use Gravity__ |If enabled, the object is affected by gravity. |
|__Is Kinematic__ |If enabled, the object will not be driven by the physics engine, and can only be manipulated by its __Transform__. This is useful for moving platforms or if you want to animate a Rigidbody that has a __HingeJoint__ attached. |
|__Interpolate__ |Try one of the options only if you are seeing jerkiness in your Rigidbody's movement. |
|- __None__ |No Interpolation is applied. |
|- __Interpolate__ |Transform is smoothed based on the Transform of the previous frame. |
|- __Extrapolate__ |Transform is smoothed based on the estimated Transform of the next frame. | 
|__Collision Detection__ |Used to prevent fast moving objects from passing through other objects without detecting collisions. |
|- __Discrete__ |Use Discrete collision detection against all other colliders in the scene. Other colliders will use Discrete collision detection when testing for collision against it. Used for normal collisions (This is the default value). |
|- __Continuous__ |Use Discrete collision detection against dynamic colliders (with a rigidbody) and continuous collision detection against static MeshColliders (without a rigidbody). Rigidbodies set to Continuous Dynamic will use continuous collision detection when testing for collision against this rigidbody. Other rigidbodies will use Discrete Collision detection. Used for objects which the Continuous Dynamic detection needs to collide with. (This has a big impact on physics performance, leave it set to Discrete, if you don't have issues with collisions of fast objects) |
|- __Continuous Dynamic__ |Use continuous collision detection against objects set to Continuous and Continuous Dynamic Collision. It will also use continuous collision detection against static MeshColliders (without a rigidbody). For all other colliders it uses Discrete collision detection. Used for fast moving objects.|
|__Constraints__ |Restrictions on the Rigidbody's motion:-|
|- __Freeze Position__|Stops the Rigidbody moving in the world X, Y and Z axes selectively.|
|- __Freeze Rotation__|Stops the Rigidbody rotating around the local X, Y and Z axes selectively.|


Details
-------


Rigidbodies allow your GameObjects to act under control of the physics engine. This opens the gateway to realistic collisions, varied types of joints, and other very cool behaviors. Manipulating your GameObjects by adding forces to a Rigidbody creates a very different feel and look than adjusting the Transform __Component__ directly. Generally, you shouldn't manipulate the Rigidbody and the Transform of the same GameObject - only one or the other.

The biggest difference between manipulating the Transform versus the Rigidbody is the use of forces. Rigidbodies can receive forces and torque, but Transforms cannot. Transforms can be translated and rotated, but this is not the same as using physics. You'll notice the distinct difference when you try it for yourself. Adding forces/torque to the Rigidbody will actually change the object's position and rotation of the Transform component. This is why you should only be using one or the other. Changing the Transform while using physics could cause problems with collisions and other calculations.

Rigidbodies must be explicitly added to your GameObject before they will be affected by the physics engine. You can add a Rigidbody to your selected object from __Components-&gt;Physics-&gt;Rigidbody__ in the menu. Now your object is physics-ready; it will fall under gravity and can receive forces via scripting, but you may need to add a __Collider__ or a Joint to get it to behave exactly how you want.


###Parenting

When an object is under physics control, it moves semi-independently of the way its transform parents move. If you move any parents, they will pull the Rigidbody child along with them. However, the Rigidbodies will still fall down due to gravity and react to collision events.


###Scripting

To control your Rigidbodies, you will primarily use scripts to add forces or torque. You do this by calling __[AddForce()](ScriptRef:Rigidbody.AddForce.html)__ and __[AddTorque()](ScriptRef:Rigidbody.AddTorque.html)__ on the object's Rigidbody. Remember that you shouldn't be directly altering the object's Transform when you are using physics.


###Animation

For some situations, mainly creating ragdoll effects, it is neccessary to switch control of the object between animations and physics. For this purpose Rigidbodies can be marked __[isKinematic](ScriptRef:Rigidbody-isKinematic.html)__. While the Rigidbody is marked __isKinematic__, it will not be affected by collisions, forces, or any other part of the physics system. This means that you will have to control the object by manipulating the [Transform](class-Transform) component directly. Kinematic Rigidbodies will affect other objects, but they themselves will not be affected by physics. For example, Joints which are attached to Kinematic objects will constrain any other Rigidbodies attached to them and Kinematic Rigidbodies will affect other Rigidbodies through collisions.


###Colliders

Colliders are another kind of component that must be added alongside the Rigidbody in order to allow collisions to occur. If two Rigidbodies bump into each other, the physics engine will not calculate a collision unless both objects also have a Collider attached. Collider-less Rigidbodies will simply pass through each other during physics simulation.


![Colliders define the physical boundaries of a Rigidbody](../uploads/Main/RigidbodyandCollider.png) 

Add a Collider with the __Component-&gt;Physics__ menu. View the Component Reference page of any individual Collider for more specific information:

* [Box Collider](class-BoxCollider) - primitive shape of a cube
* [Sphere Collider](class-SphereCollider) - primitive shape of a sphere
* [Capsule Collider](class-CapsuleCollider) - primitive shape of a capsule
* [Mesh Collider](class-MeshCollider) - creates a collider from the object's mesh, cannot collide with another Mesh Collider
* [Wheel Collider](class-WheelCollider) - specifically for creating cars or other moving vehicles
* [Terrain Collider](class-TerrainCollider) - handles collision with Unity's terrain system

###Compound Colliders

Compound Colliders are combinations of primitive Colliders, collectively acting as a single Collider. They come in handy when you have a model that would be too complex or costly in terms of performance to simulate exactly, and want to simulate the collision of the shape in an optimal way using simple approximations. To create a Compound Collider, create child objects of your colliding object, then add a Collider component to each child object. This allows you to position, rotate, and scale each Collider easily and independently of one another. You can build your compound collider out of a number of primitive colliders and/or convex mesh colliders.


![A real-world Compound Collider setup](../uploads/Main/CompoundCollider.png) 

In the above picture, the _Gun Model_ GameObject has a Rigidbody attached, and multiple primitive Colliders as child GameObjects. When the Rigidbody parent is moved around by forces, the child Colliders move along with it. The primitive Colliders will collide with the environment's Mesh Collider, and the parent Rigidbody will alter the way it moves based on forces being applied to it and how its child Colliders interact with other Colliders in the Scene.

Mesh Colliders can't normally collide with each other. If a Mesh Collider is marked as __Convex__, then it can collide with another Mesh Collider. The typical solution is to use primitive Colliders for any objects that move, and Mesh Colliders for static background objects.


###Continuous Collision Detection

Continuous collision detection is a feature to prevent fast-moving colliders from passing each other. This may happen when using normal (__Discrete__) collision detection, when an object is one side of a collider in one frame, and already passed the collider in the next frame. To solve this, you can enable continuous collision detection on the rigidbody of the fast-moving object. Set the collision detection mode to __Continuous__ to prevent the rigidbody from passing through any static (ie, non-rigidbody) MeshColliders. Set it to __Continuous Dynamic__ to also prevent the rigidbody from passing through any other supported rigidbodies with collision detection mode set to __Continuous__ or __Continuous Dynamic__. 
Continuous collision detection is supported for Box-, Sphere- and CapsuleColliders. Note that continuous collision detection is intended as a safety net to catch collisions in cases where objects would otherwise pass through each other, but will not deliver physically accurate collision results, so you might still consider decreasing the fixed Time step value in the TimeManager inspector to make the simulation more precise, if you run into problems with fast moving objects.

Use the right size
------------------


The size of the your GameObject's mesh is much more important than the mass of the Rigidbody. If you find that your Rigidbody is not behaving exactly how you expect - it moves slowly, floats, or doesn't collide correctly - consider adjusting the scale of your mesh asset. Unity's default unit scale is 1 unit = 1 meter, so the scale of your imported mesh is maintained, and applied to physics calculations. For example, a crumbling skyscraper is going to fall apart very differently than a tower made of toy blocks, so objects of different sizes should be modeled to accurate scale.

If you are modeling a human make sure the model is around 2 meters tall in Unity. To check if your object has the right size compare it to the default cube. You can create a cube using __GameObject &gt; 3D Object &gt; Cube__. The cube's height will be exactly 1 meter, so your human should be twice as tall.

If you aren't able to adjust the mesh itself, you can change the uniform scale of a particular mesh asset by selecting it in __Project View__ and choosing __Assets-&gt;Import Settings...__ from the menu. Here, you can change the scale and re-import your mesh.

If your game requires that your GameObject needs to be instantiated at different scales, it is okay to adjust the values of your Transform's scale axes. The downside is that the physics simulation must do more work at the time the object is instantiated, and could cause a performance drop in your game. This isn't a terrible loss, but it is not as efficient as finalizing your scale with the other two options. Also keep in mind that non-uniform scales can create undesirable behaviors when Parenting is used. For these reasons it is always optimal to create your object at the correct scale in your modeling application.


Hints
-----


* The relative __Mass__ of two Rigidbodies determines how they react when they collide with each other.
* Making one Rigidbody have greater __Mass__ than another does not make it fall faster in free fall. Use __Drag__ for that.
* A low __Drag__ value makes an object seem heavy. A high one makes it seem light. Typical values for __Drag__ are between .001 (solid block of metal) and 10 (feather).
* If you are directly manipulating the Transform component of your object but still want physics, attach a Rigidbody and make it Kinematic.
* If you are moving a GameObject through its Transform component but you want to receive Collision/Trigger messages, you must attach a Rigidbody to the object that is moving.
* You cannot make an object stop rotating just by setting its Angular Drag to infinity.
