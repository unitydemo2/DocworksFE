#Character Controllers

The character in a first- or third-person game will often need some collision-based physics so that it doesn't fall through the floor or walk through walls. Usually, though, the character's acceleration and movement will not be physically realistic, so it may be able to accelerate, brake and change direction almost instantly without being affected by momentum.

In 3D physics, this type of behaviour can be created using a __Character Controller__. This component gives the character a simple, capsule-shaped collider that is always upright. The controller has its own special functions to set the object's speed and direction but unlike true colliders, a rigidbody is not needed and the momentum effects are not realistic.

A character controller cannot walk through static colliders in a scene, and so will follow floors and be obstructed by walls. It can push rigidbody objects aside while moving but will not be accelerated by incoming collisions. This means that you can use the standard 3D colliders to create a scene around which the controller will walk but you are not limited by realistic physical behaviour on the character itself.

You can find out more about character controllers on the [reference page](class-CharacterController).