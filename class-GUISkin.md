GUI Skin (IMGUI System)
========


__GUISkins__ are a collection of __GUIStyles__ that can be applied to your GUI. Each __Control__ type has its own Style definition. Skins are intended to allow you to apply style to an entire UI, instead of a single Control by itself.


![A GUI Skin as seen in the Inspector](../uploads/Main/Inspector-GUISkin.png) 

To create a GUISkin, select __Assets-&gt;Create-&gt;GUI Skin__ from the menubar.

**Please Note**: This page refers to part of the [IMGUI](GUIScriptingGuide) system, which is a *scripting-only* UI system. Unity has a full GameObject-based UI system which you may prefer to use. It allows you to design and edit user interface elements as visible objects in the scene view. See the [UI System Manual](UISystem) for more information.


Properties
----------


All of the properties within a GUI Skin are an individual [GUIStyle](class-GUIStyle). Please read the [GUIStyle](class-GUIStyle) page for more information about how to use Styles.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Font__ |The global Font to use for every Control in the GUI |
|__Box__ |The [Style](class-GUIStyle) to use for all Boxes |
|__Button__ |The [Style](class-GUIStyle) to use for all Buttons |
|__Toggle__ |The [Style](class-GUIStyle) to use for all Toggles |
|__Label__ |The [Style](class-GUIStyle) to use for all Labels |
|__Text Field__ |The [Style](class-GUIStyle) to use for all Text Fields |
|__Text Area__ |The [Style](class-GUIStyle) to use for all Text Areas |
|__Window__ |The [Style](class-GUIStyle) to use for all Windows |
|__Horizontal Slider__ |The [Style](class-GUIStyle) to use for all Horizontal Slider bars |
|__Horizontal Slider Thumb__ |The [Style](class-GUIStyle) to use for all Horizontal Slider Thumb Buttons |
|__Vertical Slider__ |The [Style](class-GUIStyle) to use for all Vertical Slider bars |
|__Vertical Slider Thumb__ |The [Style](class-GUIStyle) to use for all Vertical Slider Thumb Buttons |
|__Horizontal Scrollbar__ |The [Style](class-GUIStyle) to use for all Horizontal Scrollbars |
|__Horizontal Scrollbar Thumb__ |The [Style](class-GUIStyle) to use for all Horizontal Scrollbar Thumb Buttons |
|__Horizontal Scrollbar Left Button__ |The [Style](class-GUIStyle) to use for all Horizontal Scrollbar scroll Left Buttons |
|__Horizontal Scrollbar Right Button__ |The [Style](class-GUIStyle) to use for all Horizontal Scrollbar scroll Right Buttons |
|__Vertical Scrollbar__ |The [Style](class-GUIStyle) to use for all Vertical Scrollbars |
|__Vertical Scrollbar Thumb__ |The [Style](class-GUIStyle) to use for all Vertical Scrollbar Thumb Buttons |
|__Vertical Scrollbar Up Button__ |The [Style](class-GUIStyle) to use for all Vertical Scrollbar scroll Up Buttons |
|__Vertical Scrollbar Down Button__ |The [Style](class-GUIStyle) to use for all Vertical Scrollbar scroll Down Buttons |
|__Custom 1-20__ |Additional custom Styles that can be applied to any Control |
|__Custom Styles__ |An array of additional custom Styles that can be applied to any Control |
|__Settings__ |Additional Settings for the entire GUI |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Double Click Selects Word__ |If enabled, double-clicking a word will select it |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Triple Click Selects Line__ |If enabled, triple-clicking a word will select the entire line |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Cursor Color__ |Color of the keyboard cursor |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Cursor Flash Speed__ |The speed at which the text cursor will flash when editing any Text Control |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Selection Color__ |Color of the selected area of Text |


Details
-------


When you are creating an entire GUI for your game, you will likely need to do a lot of customization for every different Control type. In many different game genres, like real-time strategy or role-playing, there is a need for practically every single Control type.

Because each individual Control uses a particular Style, it does not make sense to create a dozen-plus individual Styles and assign them all manually. GUI Skins take care of this problem for you. By creating a GUI Skin, you have a pre-defined collection of Styles for every individual Control. You then apply the Skin with a single line of code, which eliminates the need to manually specify the Style of each individual Control.


###Creating GUISkins

GUISkins are asset files. To create a GUI Skin, select __Assets-&gt;Create-&gt;GUI Skin__ from the menubar. This will put a new GUISkin in your __Project View__.


![A new GUISkin file in the Project View](../uploads/Main/GUISkin-ProjectView.png) 


###Editing GUISkins

After you have created a GUISkin, you can edit all of the [Styles](class-GUIStyle) it contains in the Inspector. For example, the __Text Field__ [Style](class-GUIStyle) will be applied to all Text Field Controls.


![Editing the Text Field Style in a GUISkin](../uploads/Main/GUISkin-EditingTextField.png) 

No matter how many Text Fields you create in your script, they will all use this [Style](class-GUIStyle). Of course, you have control over changing the styles of one Text Field over the other if you wish. We'll discuss how that is done next.


###Applying GUISkins

To apply a GUISkin to your GUI, you must use a simple script to read and apply the Skin to your Controls.


````

	// Create a public variable where we can assign the GUISkin
	var customSkin : GUISkin;

	// Apply the Skin in our OnGUI() function
	function OnGUI () {
		GUI.skin = customSkin;

		// Now create any Controls you like, and they will be displayed with the custom Skin
		GUILayout.Button ("I am a re-Skinned Button");

		// You can change or remove the skin for some Controls but not others
		GUI.skin = null;

		// Any Controls created here will use the default Skin and not the custom Skin
		GUILayout.Button ("This Button uses the default UnityGUI Skin");
	}


````


In some cases you want to have two of the same Control with different Styles. For this, it does not make sense to create a new Skin and re-assign it. Instead, you use one of the __Custom__ Styles in the skin. Provide a __Name__ for the custom Style, and you can use that name as the last argument of the individual Control.



````
	// One of the custom Styles in this Skin has the name "MyCustomControl"
	var customSkin : GUISkin;

	function OnGUI () {
		GUI.skin = customSkin;

		// We provide the name of the Style we want to use as the last argument of the Control function
		GUILayout.Button ("I am a custom styled Button", "MyCustomControl");

		// We can also ignore the Custom Style, and use the Skin's default Button Style
		GUILayout.Button ("I am the Skin's Button Style");
	}

````

For more information about working with GUIStyles, please read the [GUIStyle](class-GUIStyle) page. For more information about using UnityGUI, please read the [GUI Scripting Guide](GUIScriptingGuide).
