GUI Text (Legacy UI Component)
========


__GUI Text__ displays text of any font you import in screen coordinates.


![](../uploads/Main/Inspector-GUIText.png) 

**Please Note:** *This component relates to legacy methods for drawing UI textures and images to the screen. You should use Unity's up-to-date [UI system](UISystem) instead. This is also unrelated to the [IMGUI system](GUIScriptingGuide).*


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Text__ |The string to display. |
|__Anchor__ |The point at which the __Text__ shares the position of the __Transform__. |
|__Alignment__ |How multiple lines are aligned within the __GUIText__. |
|__Pixel Offset__ |Offset of the text relative to the position of the GUIText in the screen.|
|__Line Spacing__ |How much space will be in-between lines of __Text__. |
|__Tab Size__ |How much space will be inserted for a tab ('&#92;t') character. As a multiplum of the space character offset. |
|__Font__ |The [Font](class-Font) to use when rendering the text. |
|__Material__ |Reference to the __Material__ containing the characters to be drawn. If set, this property overrides the one in the [Font](class-Font) asset. |
|__Font Size__ |The font size to use. Set to 0 to use the default font size. Only applicable for dynamic fonts. |
|__Font Style__ |The font style to use. (Normal, Bold, Italic or Bold and Italic). Only applicable for dynamic fonts. |
|__Pixel Correct__ |If enabled, all __Text__ characters will be drawn in the size of the imported font texture. If disabled, the characters will be resized based on the Transform's __Scale__. |
|__Rich Text__ |If enabled, allows HTML-style tags for text formatting. |


Details
-------


GUI Texts are used to print text onto the screen in 2D. The __Camera__ has to have a [GUI Layer](class-GUILayer) attached in order to render the text. Cameras include a GUI Layer by default, so don't remove it if you want to display a GUI Text. GUI Texts are positioned using only the X and Y axes. Rather than being positioned in World Coordinates, GUI Texts are positioned in Screen Coordinates, where (0,0) is the bottom-left and (1,1) is the top-right corner of the screen.  To add a GUIText component in Unity 5.0, first use __GameObject->Create Empty__ to create an empty game object, then use the __Component->Rendering->GUIText__ option to add the GUIText component to the newly created game object.  If the text isn't visible when you press Play, check that the transform has suitable position, typically (0.5, 0.5, 0.0).

To import a font see the [Font page](class-Font).

To use Rich Text see the [Rich Text page](StyledText).


###Pixel Correct

By default, GUI Texts are rendered with __Pixel Correct__ enabled. This makes them look crisp and they will stay the same size in pixels independent of the screen resolution.

Hints
-----


* When entering text into the __Text__ property, you can create a line break by holding __Alt__ and pressing __Return__.
* If you are scripting the __Text__ property, you can add line breaks by inserting the escape character "&#92;n" in your strings.
* You can download free true type fonts from [1001freefonts.com](http://www.1001freefonts.com/fonts/afonts.htm) (download the Windows fonts since they contain TrueType fonts).
