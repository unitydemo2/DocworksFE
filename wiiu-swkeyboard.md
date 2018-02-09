Software Keyboard
==================

Wii U uses the common interface for on screen keyboard [TouchScreenKeyboard](ScriptRef:TouchScreenKeyboard.html) with additional option *targetDisplay* to specify which display it will be rendered onto. Use ```UnityEngine.WiiU.DisplayIndex.TV``` or ```UnityEngine.WiiU.DisplayIndex.GamePad``` (*default*) to specify the displays.

An example:

	TouchScreenKeyboard keyboard = TouchScreenKeyboard.Open("Enter a name", TouchScreenKeyboardType.Default);
	keyboard.targetDisplay = UnityEngine.WiiU.DisplayIndex.TV; // appear on TV

