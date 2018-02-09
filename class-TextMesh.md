Text Mesh
=========


The __Text Mesh__ generates 3D geometry that displays text strings.


![](../uploads/Main/Inspector-TextMesh.png) 

You can create a new Text Mesh from __Component &gt; Mesh &gt; Text Mesh__.


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Text__ |The text that will be rendered |
|__Offset Z__ |How far should the text be offset from the transform.position.z when drawing |
|__Character Size__ |The size of each character (This scales the whole text.) |
|__Line Spacing__ |How much space will be in-between lines of text. |
|__Anchor__ |Which point of the text shares the position of the Transform. |
|__Alignment__ |How lines of text are aligned (Left, Right, Center). |
|__Tab Size__ |How much space will be inserted for a tab '&#92;t' character. This is a multiplum of the 'spacebar' character offset. |
|__Font Size__ |The size of the font. This can override the size of a dynamic font.|
|__Font Style__ |The rendering style of the font. The font needs to be marked as dynamic.|
|__Rich Text__ |When selected this will enable tag processing when the text is rendered.|
|__Font__ |The [TrueType Font](class-Font) to use when rendering the text. |
|__Color__ |The global color to use when rendering the text. |


Details
-------


Text Meshes can be used for rendering road signs, graffiti etc. The Text Mesh places text in the 3D scene. To make generic 2D text for GUIs, use a [GUI Text](class-GUIText) component instead.

Follow these steps to create a Text Mesh with a custom Font:

1. Import a font by dragging a TrueType Font - a **.ttf** file - from the Explorer (Windows) or Finder (OS X) into the __Project View__.
1. Select the imported font in the Project View.
1. Choose __GameObject &gt; Create Other &gt; 3D Text__.
You have now created a text mesh with your custom TrueType Font. You can scale the text and move it around using the __Scene View's__ __Transform__ controls.

**Note:** If you want to change the font for a Text Mesh, need to set the component's font property and also set the texture of the font material to the correct font texture. This texture can be located using the font asset's foldout. If you forget to set the texture then the text in the mesh will appear blocky and misaligned. 

Hints
-----


* You can download free TrueType Fonts from [1001freefonts.com](http://www.1001freefonts.com/fonts/afonts.htm) (download the Windows fonts since they contain TrueType Fonts).
* If you are scripting the __Text__ property, you can add line breaks by inserting the escape character "&#92;n" in your strings.
* Text meshes can be styled using simple mark-up. See the [Styled Text](StyledText) page for more details.
* Fonts in Unity are rendered by first rendering the font glyphs to a texture map.  If the font size is set too small, these font textures will appear blocky.  Since TextMesh assets are rendered using quads, it's possible that if the size of the TextMesh and font texture differ the TextMesh will look wrong.
