Vertex Lit Rendering Path Details
=================================


This page describes details of __Vertex Lit__ [rendering path](RenderingPaths).

Vertex Lit path generally renders each object in one pass, with lighting from all lights calculated for each vertex.

It's the fastest rendering path and has the widest hardware support.

Since all lighting is calculated at the vertex level, this rendering path does not support most per-pixel effects: shadows, normal mapping, light cookies, and highly detailed specular highlights are not supported.
