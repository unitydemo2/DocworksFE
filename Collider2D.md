# Collider 2D

__Collider 2D__ components define the shape of a 2D GameObject for the purposes of physical collisions. A Collider, which is invisible, need not be the exact same shape as the GameObject's Mesh;  in fact, a rough approximation is often more efficient and indistinguishable in gameplay.

Colliders for 2D GameObjects all have names ending "2D". A Collider that does not have "2D" in the name is intended for use on a 3D GameObject. Note that you can’t mix 3D GameObjects and 2D Colliders, or 2D GameObjects and 3D Colliders.

The Collider 2D types that can be used with Rigidbody 2D are:

* [Circle Collider 2D](class-CircleCollider2D) for circular collision areas.
* [Box Collider 2D](class-BoxCollider2D) for square and rectangle collision areas.
* [Polygon Collider 2D](class-PolygonCollider2D) for freeform collision areas.
* [Edge Collider 2D](class-EdgeCollider2D) for freeform collision areas and areas which aren't completely enclosed (such as rounded convex corners).
* [Capsule Collider 2D](class-CapsuleCollider2D) for circular or lozenge-shaped collision areas.
* [Composite Collider 2D](class-CompositeCollider2D) for merging Box Collider 2Ds and Polygon Collider 2Ds.
 

## Use Auto Mass

On the Rigidbody 2D component, tick the __Use Auto Mass__ checkbox to automatically set the Rigidbody 2D's mass to the same value as the Collider 2D's mass. This is particularly useful in conjunction with the [Buoyancy Effector 2D](class-BuoyancyEffector2D).
