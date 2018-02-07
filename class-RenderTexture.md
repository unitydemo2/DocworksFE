Render Texture
==============

__Render Textures__ are special types of __Textures__ that are created and updated at runtime. To use them, you first create a new Render Texture and designate one of your [Cameras](class-Camera) to render into it. Then you can use the Render Texture in a __Material__ just like a regular Texture. The [Water](HOWTO-Water) prefabs in Unity Standard Assets are an example of real-world use of Render Textures for making real-time reflections and refractions.


Properties
----------


The Render Texture __Inspector__ is different from most Inspectors, but very similar to the [Texture Inspector](class-TextureImporter).


![The Render Texture Inspector is almost identical to the Texture Inspector](../uploads/Main/Inspector-RenderTexture.png) 

The Render Texture inspector displays the current contents of Render Texture in realtime and can be an invaluable debugging tool for effects that use render textures.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Size__ |The size of the Render Texture in pixels. Observe that only power-of-two values sizes can be chosen. |
|__Anti-Aliasing__ |The amount of anti-aliasing to be applied. None, two, four or eight samples.|
|__Depth Buffer__ |The type of the depth buffer. None, 16 bit or 24 bit. |
|__Wrap Mode__ |Selects how the Texture behaves when tiled: |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Repeat__ |The Texture repeats (tiles) itself |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Clamp__ |The Texture's edges get stretched |
|__Filter Mode__ |Selects how the Texture is filtered when it gets stretched by 3D transformations: |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__No Filtering__ |The Texture becomes blocky up close |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bilinear__ |The Texture becomes blurry up close |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Trilinear__ |Like Bilinear, but the Texture also blurs between the different mip levels |
|__Aniso Level__ |Increases Texture quality when viewing the texture at a steep angle. Good for floor and ground textures |


Example
-------


A very quick way to make a live arena-camera in your game:

1. Create a new Render Texture asset using __Assets &gt;Create &gt;Render Texture__.
1. Create a new Camera using __GameObject &gt; Camera__.
1. Assign the Render Texture to the __Target Texture__ of the new Camera.
1. Create a wide, tall and thin box
1. Drag the Render Texture onto it to create a Material that uses the render texture.
1. Enter Play Mode, and observe that the box's texture is updated in real-time based on the new Camera's output.


![Render Textures are set up as demonstrated above](../uploads/Main/RenderTextureLiveCam.png) 

---

* <span class="page-edit">2017-09-19  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">GameObject menu changed in Unity 4.6</span>
