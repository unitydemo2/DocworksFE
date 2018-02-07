#Mobile Keyboard

In most cases, Unity will handle keyboard input automatically for GUI elements but it is also easy to show the keyboard on demand from a script.


##GUI Elements
The keyboard will appear automatically when a user taps on editable GUI elements. Currently, [GUI.TextField](ScriptRef:GUI.TextField.html), [GUI.TextArea](ScriptRef:GUI.TextArea.html) and [GUI.PasswordField](ScriptRef:GUI.PasswordField.html) will display the keyboard; see the [GUI class](ScriptRef:GUI.html) documentation for further details.

##Manual Keyboard Handling
Use the __[TouchScreenKeyboard.Open()](ScriptRef:TouchScreenKeyboard.Open.html)__ function to open the keyboard. Please see the [TouchScreenKeyboard](ScriptRef:TouchScreenKeyboard.html) scripting reference for the parameters that this function takes.

##Keyboard Layout Options

The Keyboard supports the following options:-

|**_Property:_** |**_Function:_** |
|:---|:---|
|__[TouchScreenKeyboardType.Default](ScriptRef:TouchScreenKeyboardType.Default.html)__ |Letters. Can be switched to keyboard with numbers and punctuation.|
|__[TouchScreenKeyboardType.ASCIICapable](ScriptRef:TouchScreenKeyboardType.ASCIICapable.html)__ |Letters. Can be switched to keyboard with numbers and punctuation.|
|__[TouchScreenKeyboardType.NumbersAndPunctuation](ScriptRef:TouchScreenKeyboardType.NumbersAndPunctuation.html)__ |Numbers and punctuation. Can be switched to keyboard with letters.|
|__[TouchScreenKeyboardType.URL](ScriptRef:TouchScreenKeyboardType.URL.html)__ |Letters with slash and .com buttons. Can be switched to keyboard with numbers and punctuation.|
|__[TouchScreenKeyboardType.NumberPad](ScriptRef:TouchScreenKeyboardType.NumberPad.html)__ |Only numbers from 0 to 9.|
|__[TouchScreenKeyboardType.PhonePad](ScriptRef:TouchScreenKeyboardType.PhonePad.html)__ |Keyboard used to enter phone numbers.|
|__[TouchScreenKeyboardType.NamePhonePad](ScriptRef:TouchScreenKeyboardType.NamePhonePad.html)__ |Letters. Can be switched to phone keyboard.|
|__[TouchScreenKeyboardType.EmailAddress](ScriptRef:TouchScreenKeyboardType.EmailAddress.html)__ |Letters with @ sign. Can be switched to keyboard with numbers and punctuation.|



##Text Preview

By default, an edit box will be created and placed on top of the keyboard after it appears. This works as preview of the text that user is typing, so the text is always visible for the user. However, you can disable text preview by setting __TouchScreenKeyboard.hideInput__ to true. Note that this works only for certain keyboard types and input modes. For example, it will not work for phone keypads and multi-line text input. In such cases, the edit box will always appear. __TouchScreenKeyboard.hideInput__ is a global variable and will affect all keyboards.



##Visibility and Keyboard Size

There are three keyboard properties in [TouchScreenKeyboard](ScriptRef:TouchScreenKeyboard.html) that determine keyboard visibility status and size on the screen.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__visible__ |Returns __true__ if the keyboard is fully visible on the screen and can be used to enter characters.|
|__area__ |Returns the position and dimensions of the keyboard.|
|__active__ |Returns __true__ if the keyboard is activated. This property is not static property. You must have a keyboard instance to use this property.|

Note that __TouchScreenKeyboard.area__ will return a Rect with position and size set to 0 until the keyboard is fully visible on the screen. You should not query this value immediately after __TouchScreenKeyboard.Open()__. The sequence of keyboard events is as follows:


* __TouchScreenKeyboard.Open()__ is called. __TouchScreenKeyboard.active__ returns true. __TouchScreenKeyboard.visible__ returns false. __TouchScreenKeyboard.area__ returns (0, 0, 0, 0).
* Keyboard slides out into the screen. All properties remain the same.
* Keyboard stops sliding. __TouchScreenKeyboard.active__ returns true. __TouchScreenKeyboard.visible__ returns true. __TouchScreenKeyboard.area__ returns real position and size of the keyboard.



##Secure Text Input

It is possible to configure the keyboard to hide symbols when typing. This is useful when users are required to enter sensitive information (such as passwords). To manually open keyboard with secure text input enabled, use the following code:


````
TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true);


````


![Hiding text while typing](../uploads/Main/KeyboardSecure.png) 



##Alert keyboard

To display the keyboard with a black semi-transparent background instead of the classic opaque, call __TouchScreenKeyboard.Open()__ as follows:


````
TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true, true);


````

![Alert keyboard](../uploads/Main/KeyboardAlert.png) 
