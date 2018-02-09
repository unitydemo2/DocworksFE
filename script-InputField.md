#Input Field

An __Input Field__ is a way to make the text of a [Text Control](script-Text) editable. Like the other interaction controls, it's not a visible UI element in itself and must be combined with one or more visual UI elements in order to be visible.

![An empty Input Field.](../uploads/Main/UI_InputFieldExample.png)

![Text entered into the Input Field.](../uploads/Main/UI_InputFieldExample2.png)

![](../uploads/Main/UI_InputFieldInspector.png)

##Properties

|**_Property:_**||**_Function:_** |
|:---|:---|:---|
|__**Interactable**__ ||A boolean that determines if the Input Field can be interacted with or not.|

|__**Transition**__ ||[Transitions](script-SelectableTransition) are used to set how the input field transitions when ***Normal***, ***Highlighted***, ***Pressed*** or ***Disabled***. |
|__**Navigation**__ || Properties that determine the sequence of controls. See [Navigation Options](script-SelectableNavigation).|

|__**TextComponent**__ ||A reference to the [Text](script-Text) element used as the contents of the _*Input Field*_|

|__**Text**__ ||Starting Value. The initial text placed in the field before editing begins. |

|__**Character Limit**__ ||The value of the maximum number of characters that can be entered into the input field.|

|__**Content Type**__ ||Define the type(s) of characters that your input field accepts|
| |__Standard__ |Any charcter can be entered.|
| |__Autocorrected__ |The autocorrection determines whether the input tracks unknown words and suggests a more suitable replacement candidate to the user, replacing the typed text automatically unless the user explicitly overrides the action.|
| |__Integer Number__ |Allow only whole numbers to be entered.|
| |__Decimal Number__ |Allow only numbers and a single decimal point to be entered.|
| |__Alphanumeric__ |Allow both letters and numbers. Symbols cannot be entered.|
| |__Name__ |Automatically capitalizes the first letter of each word. Note that the user can circumvent the capitalization rules using the __Delete__ key.|
| |__Email Address__ |Allows you to enter an Alphanumeric string consisting of a maximum of one @ sign. periods/baseline dots cannot be entered next to each other. |
| |__Password*__ |Conceals the characters inputed with an asterisk. Allows symbols.|
| |__Pin__ |Conceals the characters inputed with an asterisk. Only allows only whole numbers to be entered.|
| |__Custom__ |Allows you to customise the Line Type, Input Type, Keyboard Type and Character Validation.|

|__**Line Type**__ ||Defines how test is formatted inside the text field.|
| |__Single Line__ |Only allows text to be on a single line.|
| |__Multi Line Submit__ |Allows text to use multiple lines. Only uses a new line when needed.|
| |__Multi Line Newline__ |Allows text to use multiple lines. User can use a newline by pressing the return key.|

|__**Placeholder**__ ||This is an optional ‘empty’ [Graphic](ScriptRef:UI.Graphic.html) to show that  the _*Input Field*_ is empty of text. Note that this ‘empty' graphic still displays even when the _*Input Field*_ is selected (that is; when there is focus on it). eg; "Enter text...".|

|__**Caret Blink Rate**__ ||Defines the blink rate for the mark placed on the line to indicate a proposed insertion of text.|

|__**Selection Color**__ ||The background color of the selected portion of text.|

|__**Hide Mobile Input** (iOS only)__ ||Hides the native input field attached to the onscreen keyboard on mobile devices. Note that this only works on iOS devices.|
| | | |

##Events

|**_Property:_** |**_Function:_** |
|:---|:---|
|__On Value Change__ | A [UnityEvent](UnityEvents) that is invoked when the text content of the Input Field changes. The event can send the current text content as a `string` type dynamic argument. |
|__End Edit__ | A [UnityEvent](UnityEvents) that is invoked when the user finishes editing the text content either by submitting or by clicking somewhere that removes the focus from the Input Field. The event can send the current text content as a `string` type dynamic argument. |


##Details

The Input Field script can be added to any existing Text control object from the menu (__Component &gt; UI &gt; Input Field__). Having done this, you should also drag the object to the Input Field's _Text_ property to enable editing.

The _Text_ property of the Text control itself will change as the user types and the value can be retrieved from a script after editing. Note that Rich Text is intentionally not supported for editable Text controls; the field will apply any Rich Text markup instantly when typed but the markup essentially "disappears" and there is no subsequent way to change or remove the styling.


##Hints

* To obtains the text of the Input Field, use the text property on the InputField component itself, not the text property of the Text component that displays the text. The text property of the Text component may be cropped or may consist of asterisks for passwords.
