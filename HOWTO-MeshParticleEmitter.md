How do I make a Mesh Particle Emitter? (Legacy Particle System)
===============================================================


__Mesh Particle Emitters__ are generally used when you need high control over where to emit particles.

For example, when you want to create a flaming sword:


1. Drag a mesh into the scene.
1. Remove the __Mesh Renderer__ by right-clicking on the __Mesh Renderer's__ __Inspector__ title bar and choose __Remove Component__.
1. Choose __Mesh Particle Emitter__ from the __Component-&gt;Effects-&gt;Legacy Particles__ menu.
1. Choose __Particle Animator__ from the __Component-&gt;Effects-&gt;Legacy Particles__ menu.
1. Choose __Particle Renderer__ from the __Component-&gt;Effects-&gt;Legacy Particles__ menu.

You should now see particles emitting from the mesh.

Play around with the values in the [Mesh Particle Emitter](class-MeshParticleEmitter).

Especially enable __Interpolate Triangles__ in the Mesh Particle Emitter Inspector and set __Min Normal Velocity__ and __Max Normal Velocity__ to 1.

To customize the look of the particles that are emitted:


1. Choose __Assets-&gt;Create-&gt;Material__ from the menu bar.
1. In the Material Inspector, select __Particles-&gt;Additive__ from the shader drop-down.
1. Drag & drop a texture from the __Project view__ onto the texture slot in the Material Inspector.
1. Drag the Material from the Project View onto the Particle System in the __Scene View__.

You should now see textured particles emitting from the mesh.

See Also
--------


* [Mesh Particle Emitter Component Reference page](class-MeshParticleEmitter)
