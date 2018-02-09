#ShaderLab: Legacy BindChannels


__BindChannels__ command allows you to specify how vertex data maps to the graphics hardware.

***Note:** _BindChannels has no effect when [vertex programs](SL-ShaderPrograms) are used, as in that case bindings are controlled by vertex shader inputs. It is advisable to use programmable shaders these days instead of fixed function vertex processing.*

By default, Unity figures out the bindings for you, but in some cases you want custom ones to be used. 

For example you could map the primary UV set to be used in the first texture stage and the secondary UV set to be used in the second texture stage; or tell the hardware that vertex colors should be taken into account.

Syntax
------

````
BindChannels { Bind "source", target }
````
Specifies that vertex data _source_ maps to hardware _target_.

**Source** can be one of:

* __Vertex__: vertex position
* __Normal__: vertex normal
* __Tangent__: vertex tangent
* __Texcoord__: primary UV coordinate
* __Texcoord1__: secondary UV coordinate
* __Color__: per-vertex color

**Target** can be one of:

* __Vertex__: vertex position
* __Normal__: vertex normal
* __Tangent__: vertex tangent
* __Texcoord0__, __Texcoord1__, ...: texture coordinates for corresponding texture stage
* __Texcoord__: texture coordinates for all texture stages
* __Color__: vertex color

Details
-------


Unity places some restrictions on which sources can be mapped to which targets. Source and target must match for __Vertex__, __Normal__, __Tangent__ and __Color__. Texture coordinates from the mesh (__Texcoord__ and __Texcoord1__) can be mapped into texture coordinate targets (__Texcoord__ for all texture stages, or __TexcoordN__ for a specific stage).

There are two typical use cases for BindChannels:

* Shaders that take vertex colors into account.
* Shaders that use two UV sets.

Examples
--------


````
// Maps the first UV set to the first texture stage
// and the second UV set to the second texture stage
BindChannels {
   Bind "Vertex", vertex
   Bind "texcoord", texcoord0
   Bind "texcoord1", texcoord1
}
````


````
// Maps the first UV set to all texture stages
// and uses vertex colors
BindChannels {
   Bind "Vertex", vertex
   Bind "texcoord", texcoord
   Bind "Color", color
}
````
