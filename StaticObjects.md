#Static GameObjects

Many optimisations need to know if an object can move during gameplay. Information about a **Static** (ie, non-moving) object can often be precomputed in the editor in the knowledge that it will not be invalidated by a change in the object's position. For example, rendering can be optimised by combining several static objects into a single, large object known as a _batch_.

The inspector for a GameObject has a _Static_ checkbox and menu in the extreme top-right, which is used to inform various different systems in Unity that the object will not move. The object can be marked as static for each of these systems individually, so you can choose not to calculate static optimisations for an object when it isn't advantageous.


![The Static checkbox and drop-down menu, as seen when viewing a GameObject in the Inspector](../uploads/Main/GameObjectStaticDropDownMenu.png)


##Static Settings

The _Everything_ and _Nothing_ enable or disable static status simultaneously for all systems that make use of it. These systems are:

* [Lightmapping](GIIntro): advanced lighting for a scene;
* [Occluder and Occludee](OcclusionCulling): rendering optimization based on the visibility of objects from specific camera positions;
* [Batching](DrawCallBatching): rendering optimization that combines several objects into one larger object;
* [Navigation](Navigation): the system that enables characters to negotiate obstacles in the scene;
* [Off-mesh Links](class-OffMeshLink): connections made by the Navigation system between discontinuous areas of the scene.
* [Reflection Probe](class-ReflectionProbe): captures a spherical view of its surroundings in all directions.

See the pages about these topics for further details on how the static setting affects performance.