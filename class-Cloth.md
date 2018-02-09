Cloth
==============

The __Cloth__ component provides a physics-based solution for the simulation of fabrics and works in conjunction with the Skinned Mesh Renderer. While it has been specifically designed for character clothing it is still possible to use arbitrary, non-skinned meshes.

![](../uploads/Main/Inspector-Cloth.png) 

Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Stretching Stiffness__ |Stretching stiffness of the cloth. |
|__Bending Stiffness__ |Bending stiffness of the cloth. |
|__Use Tethers__ |Apply constraints that help to prevent the moving cloth particles from going too far away from the fixed ones. This helps to reduce excess stretchiness. |
|__Use Gravity__ |Should gravitational acceleration be applied to the cloth? |
|__Damping__ |Motion damping coefficient. |
|__External Acceleration__ |A constant, external acceleration applied to the cloth. |
|__Random Acceleration__ |A random, external acceleration applied to the cloth. |
|__World Velocity Scale__ |How much world-space movement of the character will affect cloth vertices. |
|__World Acceleration Scale__ |How much world-space acceleration of the character will affect cloth vertices. |
|__Friction__ |The friction of the cloth when colliding with the character. |
|__Collision Mass Scale__ |How much to increase mass of colliding particles. |
|__Use Continuous Collision__ |Enable continuous collision to improve collision stability. |
|__Use Virtual Particles__ |Add one virtual particle per triangle to improve collision stability. |
|__Solver Frequency__ |Number of solver iterations per second. |
|__Sleep Threshold__ |Cloth's sleep threshold. |
|__Capsule Colliders__ |An array of CapsuleColliders which this Cloth instance should collide with. |
|__Sphere Colliders__ |An array of ClothSphereColliderPairs which this Cloth instance should collide with. |

Details
-------

Cloth does not react to all colliders in a scene, nor does it apply forces back to the world. When it has been added the Cloth component will not react to or influence any other bodies at all. Thus Cloth and the world do not recognise or see each other until you manually add colliders from the world to the Cloth component. Even after that, the simulation is still one-way: cloth reacts to those bodies but doesn’t apply forces back.

Additionally, you can only use three types of colliders with cloth: a sphere, a capsule, and conical capsule colliders, constructed using two sphere colliders. These restrictions all exist to help boost performance.

###Edit Constraints Tool

Selecting Edit Constraints will enter the editor into a mode to edit the constraints applied to each of the vertices in the cloth mesh. All vertices will be coloured based on the current Visualization mode to display the difference between their respective values.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Visualization__ |Changes the visual appearance of the tool in the Scene view between Max Distance and Surface Penetration Values. A toggle for Manipulate Backfaces is also available. |
|__Max Distance__ |The maximum distance a cloth particle can travel from its vertex position. |
|__Surface Penetration__ |How deep the cloth particle can penetrate the mesh. |

![The Cloth Constraints Tool being used on a Skinned Mesh Renderer.](../uploads/Main/Inspector-Cloth2.png) 

There are two modes that can be used for changing the values for each vertex, in Select mode a group of vertices can be selected using the mouse cursor to either draw a selection box or else by individually clicking on vertices one at a time. Once any number of cloth vertices have been selected they can then have either Max Distance or Surface Penetration constraints enabled and a value assigned.

Paint mode allows you to directly adjust each individual vertex by clicking on it, again with options to adjust the Max Distance, Surface Penetration, or both. As before a value can be assigned and the visual representation in the scene view will be updated.

###Collisions

Cloth is unable to simply collide with arbitrary world geometry, and now will only interact with the colliders specified in either the [Capsule Colliders](ScriptRef:Cloth-capsuleColliders.html) or [Sphere Colliders](ScriptRef:Cloth-sphereColliders.html) arrays.

The sphere colliders array can contain either a single valid [SphereCollider](ScriptRef:SphereCollider.html) instance (with the second one being null), or a pair. In the former cases the [ClothSphereColliderPair](ScriptRef:ClothSphereColliderPair.html) just represents a single sphere collider for the cloth to collide against. In the latter case, it represents a conic capsule shape defined by the two spheres, and the cone connecting the two. Conic capsule shapes are useful for modelling limbs of a character.