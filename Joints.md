#Joints

You can attach one rigidbody object to another or to a fixed point in space using a __Joint__ component. Generally, you want a joint to allow at least _some_ freedom of motion and so Unity provides different Joint components that enforce different restrictions. 

For example, a [Hinge Joint](class-HingeJoint) allows rotation around a specific point and axis while a [Spring Joint](class-SpringJoint) keeps the objects apart but lets the distance between them stretch slightly. 

2D joint components have **2D** at the end of the name, eg, [Hinge Joint 2D](class-HingeJoint2D). See [Joints 2D](Joints2D) for a summary of the 2D joints and useful background information.

Joints also have other options that can enabled for specific effects. For example, you can set a joint to break when the force applied to it exceeds a certain threshold. Some joints also allow a __drive force__ to occur between the connected objects to set them in motion automatically.

See each  joint reference page for the Joint classes  and for further information about their properties.