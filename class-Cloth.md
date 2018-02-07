# Cloth

The Cloth component works with the Skinned Mesh Renderer to provide a physics-based solution for simulating fabrics. It is specifically designed for character clothing, and only works with skinned meshes. If you add a Cloth component to a non-skinned Mesh, Unity removes the non-skinned Mesh and adds a skinned Mesh. 

To attach a Cloth component to a skinned Mesh, select the GameObject in the Editor, click the __Add Component__ button in the Inspector window, and select __Physics__ &gt; __Cloth__. The component appears in the Inspector.

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

Select __Edit__ &gt; __Constraints__ to edit the constraints applied to each of the vertices in the cloth mesh. All vertices have a color based on the current visualization mode, to display the difference between their respective values. You can author Cloth constraints by painting them onto the cloth with a brush.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Visualization__ |Changes the visual appearance of the tool in the Scene view between Max Distance and Surface Penetration Values. A toggle for Manipulate Backfaces is also available. |
|__Max Distance__ |The maximum distance a cloth particle can travel from its vertex position. |
|__Surface Penetration__ |How deep the cloth particle can penetrate the mesh. |
|__Brush Radius__ |Sets the radius of a brush that enables you to paint constraints onto a cloth. |

![The Cloth Constraints Tool being used on a Skinned Mesh Renderer.](../uploads/Main/Inspector-Cloth2.png) 

There are two modes for changing the values for each vertex:

* Use __Select__ mode to select a group of vertices. To do this, use the mouse cursor to draw a selection box or click on vertices one at a time. You can can then enable __Max Distance__, __Surface Penetration__, or both, and set a value.

* Use __Paint__ mode to directly adjust each individual vertex. To do this, click the vertex you want to adjust. You can can then enable __Max Distance__, __Surface Penetration__, or both, and set a value.

In both modes, the visual representation in the Scene view automatically updates when you assign values to __Max Distance__ and __Surface Penetration__.

![The Cloth Constraints Tool in Paint mode](../uploads/Main/ClothContraintsPaint.png) 

###Self collision and intercollision

Cloth collision makes character clothing and other fabrics in your game move more realistically. In Unity, a cloth has several cloth particles that handle collision. You can set up cloth particles for:

* Self-collision, which prevents cloth from penetrating itself. 
* Intercollision, which allows cloth particles to collide with each other.

To set up the collision particles for a cloth, select the __Self Collision and Intercollision__ button in the Cloth inspector:

![The Self Collision and Intercollision button in the Cloth Inspector](../uploads/Main/Inspector-Cloth-Collision-Button.png) 

The __Cloth Self Collision And Intercollision__ window appears in the Scene view:

![The Cloth Self Collision And Intercollision window](../uploads/Main/ClothSelfCollisionAndIntercollision.png)

Cloth particles appear automatically for skinned Meshes with a Cloth component. Initially, none of the cloth particles are set to use collision. These unused particles appear black:

![Unused cloth particles](../uploads/Main/ClothSelfCollisionNonSelected.png)

To apply self-collision or intercollision, you need to select a single set of particles to apply collision to. To select a set of particles for collision, click the __Select__ button:

![Select cloth particles button](../uploads/Main/ClothSelectParticles.png)

Now left-click and drag to select the particles you want to apply collision to:

![Selecting cloth particles using click and drag](../uploads/Main/SelectingClothParticles.png)

The selected particles appear in blue:

![Selected cloth particles are blue](../uploads/Main/SelectedParticlesBlue.png)

Tick the __Self Collision and Intercollision__ checkbox to apply collision to the selected particles:

![Self Collision and Intercollision tick box](../uploads/Main/SelfCollisionAndIntercollisionCheckbox.png)

The particles you specify for use in collision appear in green:

![Selected particles are green](../uploads/Main/SelectedParticlesGreen.png)

To enable the self collision behavior for a cloth, to go the __Self Collision__ section of the Cloth Inspector window and set __Distance__ and __Stiffness__ to non-zero values:

![Self Collision parameters](../uploads/Main/SelfCollisionParameters.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Distance__ |The diameter of a sphere around each particle. Unity ensures that these spheres do not overlap during simulations. __Distance__ should be smaller than the smallest distance between two particles in the configuration. If the distance is larger, self collision may violate some distance constraints and result in jittering. |
|__Stiffness__ |How strong the separating impulse between particles should be. The cloth solver calculates this and it should be enough to keep the particles separated. |

Self collision and intercollision can take a significant amount of the overall simulation time. Consider keeping the collision distance small and using self collision indices to reduce the number of particles that collide with each other.

Self collision uses vertices, not triangles, so don’t expect self collision to work perfectly for Meshes with triangles much larger than the cloth thickness.

__Paint__ and __Erase__ modes allow you to add or remove particles for use in collision by holding the left mouse button down and dragging individual cloth particles:

![Self Collision parameters](../uploads/Main/PaintEraseModes.png)

When in __Paint__ or __Erase__ mode, particles specified for collision are green, unspecified particles are black, and particles underneath the brush are blue:

![Particles being painted are blue](../uploads/Main/PaintBrushSelfCollision.png)

#### Cloth intercollision

You specify particles for intercollision in the same way as you specify particles for self collision, as described above. As with self collision, you specify one set of particles for intercollision.

To enable intercollision behavior, open the PhysicsManager inspector (__Edit__ &gt; __Project Settings__ &gt; __Physics__) and set __Distance__ and __Stiffness__ to non-zero values in the __Cloth InterCollision__ section:

![Particles being painted are blue](../uploads/Main/ClothInspectorIntercollisionSettings.png)

Cloth intercollision __Distance__ and __Stiffness__ properties have the same function as self collision Distance and Stiffness properties, which are described above.

###Collider collision

Cloth is unable to simply collide with arbitrary world geometry, and now will only interact with the colliders specified in either the [Capsule Colliders](ScriptRef:Cloth-capsuleColliders.html) or [Sphere Colliders](ScriptRef:Cloth-sphereColliders.html) arrays.

The sphere colliders array can contain either a single valid [SphereCollider](ScriptRef:SphereCollider.html) instance (with the second one being null), or a pair. In the former cases the [ClothSphereColliderPair](ScriptRef:ClothSphereColliderPair.html) just represents a single sphere collider for the cloth to collide against. In the latter case, it represents a conic capsule shape defined by the two spheres, and the cone connecting the two. Conic capsule shapes are useful for modelling limbs of a character.

---
* <span class="page-edit">2017-12-05  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">Cloth self collision and intercollision added in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>
