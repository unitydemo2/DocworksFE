GUI Style (IMGUI System)
=========


__GUI Styles__ are a collection of custom attributes for use with __UnityGUI__. A single GUI Style defines the appearance of a single UnityGUI __Control__.


![A GUI Style in the Inspector](../uploads/Main/GuiStyleInspector.png) 

If you want to add style to more than one control, use a [GUI Skin](class-GUISkin) instead of a GUI Style. For more information about UnityGUI, please read the [GUI Scripting Guide](GUIScriptingGuide).

**Please Note**: This page refers to part of the [IMGUI](GUIScriptingGuide) system, which is a *scripting-only* UI system. Unity has a full GameObject-based UI system which you may prefer to use. It allows you to design and edit user interface elements as visible objects in the scene view. See the [UI System Manual](UISystem) for more information.


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Name__ |The text string that can be used to refer to this specific Style |
|__Normal__ |Background image & Text Color of the Control in default state |
|__Hover__ |Background image & Text Color when the mouse is positioned over the Control |
|__Active__ |Background image & Text Color when the mouse is actively clicking the Control |
|__Focused__ |Background image & Text Color when the Control has keyboard focus |
|__On Normal__ |Background image & Text Color of the Control in enabled state |
|__On Hover__ |Background image & Text Color when the mouse is positioned over the enabled Control |
|__On Active__ |Properties when the mouse is actively clicking the enabled Control |
|__On Focused__ |Background image & Text Color when the enabled Control has keyboard focus |
|__Border__ |Number of pixels on each side of the __Background__ image that are not affected by the scale of the Control' shape |
|__Padding__ |Space in pixels from each edge of the Control to the start of its contents. |
|__Margin__ |The margins between elements rendered in this style and any other GUI Controls. |
|__Overflow__ |Extra space to be added to the background image. |
|__Font__ |The Font used for all text in this style |
|__Image Position__ |The way the background image and text are combined. |
|__Alignment__ |Standard text alignment options. |
|__Word Wrap__ |If enabled, text that reaches the boundaries of the Control will wrap around to the next line |
|__Text Clipping__ |If __Word Wrap__ is enabled, choose how to handle text that exceeds the boundaries of the Control |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Overflow__ |Any text that exceeds the Control boundaries will continue beyond the boundaries |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Clip__ |Any text that exceeds the Control boundaries will be hidden |
|__Content Offset__ |Number of pixels along X and Y axes that the Content will be displaced in addition to all other properties |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__X__ |Left/Right Offset |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Y__ |Up/Down Offset |
|__Fixed Width__ |Number of pixels for the width of the Control, which will override any provided __Rect()__ value |
|__Fixed Height__ |Number of pixels for the height of the Control, which will override any provided __Rect()__ value |
|__Stretch Width__ |If enabled, Controls using this style can be stretched horizontally for a better layout. |
|__Stretch Height__ |If enabled, Controls using this style can be stretched vertically for a better layout. |


Details
-------


GUIStyles are declared from scripts and modified on a per-instance basis. If you want to use a single or few Controls with a custom Style, you can declare this custom Style in the script and provide the Style as an argument of the Control function. This will make these Controls appear with the Style that you define.

First, you must declare a GUI Style from within a script.



````
/* Declare a GUI Style */
var customGuiStyle : GUIStyle;

...


````

When you attach this script to a GameObject, you will see the custom Style available to modify in the __Inspector__.


![A Style declared in a script can be modified in each instance of the script](../uploads/Main/ModifyingStyleInInspector.png) 

Now, when you want to tell a particular Control to use this Style, you provide the name of the Style as the last argument in the Control function.



````
...

function OnGUI () {
	// Provide the name of the Style as the final argument to use it
	GUILayout.Button ("I am a custom-styled Button", customGuiStyle);

	// If you do not want to apply the Style, do not provide the name
	GUILayout.Button ("I am a normal UnityGUI Button without custom style");
}


````


![Two Buttons, one with Style, as created by the code example](../uploads/Main/guiStyle-TwoButtonsOneIsStyled.png) 

For more information about using UnityGUI, please read the [GUI Scripting Guide](GUIScriptingGuide).
