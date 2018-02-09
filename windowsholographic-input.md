#Input types

Input on HoloLens is different from other platforms. Unlike other platforms, the primary means of interaction are three non-traditional systems:

1. __Gaze__: Where the user is looking in the world.
1. __Gesture__: Hand signals used to signify commands to the system.
1. __Voice__: Short, spoken commands, and longer free-form dictation.

##Gaze

The __Gaze__ refers to where the user is looking. On HoloLens, this is fairly precise and can be used to select GameObjects in the world. This can be used to direct commands at specific GameObjects rather than every GameObject in the Scene.

Microsoft provides useful documentation on [Gaze indicator](https://dev.windows.com/en-us/holographic/gaze_indicator) and [Gaze targeting](https://dev.windows.com/en-us/holographic/gaze_targeting) pages.

##Gesture

A __Gesture__ is a hand signal interpreted by the system. These can be used to represent commands. There are several built-in Gestures you can use in your application, as well as a generic API to recognize custom Gestures. Both built-in Gestures and custom Gestures (via API) are functional in Unity.

Built-in Gestures:

* __Tap__:  With a closed hand and extended thumb and forefinger, press thumb and forefinger together. This is commonly used as a select command on the HoloLens.
* __Double Tap__:  Two Tap Gestures in rapid succession.
* __Hold__:  A Tap Gesture, keeping the forefinger and thumb together for one second or more.
* __Manipulation__: A Hold Gesture, followed by a translation in space. Distances from the Hold position are reported in the Gesture.
* __Navigation__: A Hold gesture, followed by a translation in space. This may be constrained to one or more of the x, y, and z planes, and reports a value from -1 to 1 for each axis.

For more information about gestures, refer to Microsoft's documentation on [Gesture design](https://dev.windows.com/en-us/holographic/Gesture_design).

##Voice

__Voice__ input on HoloLens is provided by the Windows 10 API. Unity supports three styles of input:

* __Keywords__: Simple commands or phrases set up in code which generate events. This allows you to quickly add voice commands to an application where localization is not an issue. This functionality is provided by the [KeywordRecognizer](ScriptRef:Windows.Speech.KeywordRecognizer.html).
* __Grammars__: A table of commands with semantic meaning which you can localize. Grammars are configured from an xml grammar file (.grxml). See Microsoft's documentation on [Creating Grammar Files](https://msdn.microsoft.com/en-us/library/ms873278.aspx) for more information on the file format. Grammar recognition functionality is provided by the [GrammarRecognizer](ScriptRef:Windows.Speech.GrammarRecognizer.html).
* __Dictation__: A more free-form text-to-speech system that translates longer spoken input into text. Dictation recognition on the HoloLens is only active for short periods of time to prolong battery life. Dictation requires a working Internet connection and is provided by the [DictationRecognizer](ScriptRef:Windows.Speech.DictationRecognizer.html).

For more information about voice input, refer to Microsoft's documentation on [Voice design](https://dev.windows.com/en-us/holographic/Voice_design).
