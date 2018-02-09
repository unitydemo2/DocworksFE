#Text

The __Text__ control displays a non-interactive piece of text to the user. This can be used to provide captions or labels for other GUI controls or to display instructions or other text.

##Properties

![](../uploads/Main/UI_TextInspector.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Text__ |The text displayed by the control. |
| **Character** |
| __Font__ | The [Font](class-Font) used to display the text. |
|__Font Style__ | The style applied to the text. The options are _Normal_, _Bold_, _Italic_ and _Bold And Italic_. |
|__Font Size__ | The size of the displayed text. |
|__Line Spacing__ | The vertical separation between lines of text. |
|__Rich Text__ | Should markup elements in the text be interpreted as [Rich Text](StyledText) styling? |
|**Paragraph**|
|__Alignment__ | The horizontal and vertical alignment of the text. |
|__Align by Geometry__ | Use the extents of glyph geometry to perform horizontal alignment rather than glyph metrics. |
|__Horizontal Overflow__ | The method used to handle the situation where the text is too wide to fit in the rectangle. The options are _Wrap_ and _Overflow_. |
|__Vertical Overflow__ | The method used to handle the situation where wrapped text is too tall to fit in the rectangle. The options are _Truncate_ and _Overflow_. |
|__Best Fit__ | Should Unity ignore the size properties and simply try to fit the text to the control's rectangle? |
| | |
|__Color__ | The color used to render the text. |
|__Material__ | The [Material](class-Material) used to render the text. |

A default text element looks like this:

![A Text element.](../uploads/Main/UI_TextExample.png)

##Details

Some controls (such as [Buttons](script-Button) and [Toggles](script-Toggle) have textual descriptions built-in. For controls that have no implicit text (such as [Sliders](script-Slider), you can indicate the purpose using a label created with a Text control. Text is also useful for lists of instructions, story text, conversations and legal disclaimers.

The Text control offers the usual parameters for font size, style, etc, and text alignment. When the _Rich Text_ option is enabled, markup elements within the text will be treated as styling information, so you can have just a single word or short section in boldface or in a different color, say (see the page about [Rich Text](StyledText) for details of the markup scheme).


##Hints

* See the [Effects](comp-UIEffects) page for how to apply a simple shadow or outline effect to the text.

 