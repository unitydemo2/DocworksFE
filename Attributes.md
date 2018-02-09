Attributes
==========


__Attributes__ are markers that can be placed above a class, property or function in a script to indicate special behaviour. For example, the __HideInInspector__ attribute can be added above a property declaration to prevent the property being shown in the inspector, even if it is public. In JavaScript, an attribute name begins with an "@" sign, whilst in C#, it is contained within square brackets:-

````
// JS

@HideInInspector
var strength: float;


// C#

[HideInInspector]
public float strength;
````

Unity provides a number of attributes which are listed in the script reference (select the Editor or Runtime Attributes section from popup menu in the sidebar). There are also attributes defined in the .NET libraries which may sometimes be useful in Unity code.

**Note:** the [ThreadStatic](http://msdn.microsoft.com/en-us/library/system.threadstaticattribute.aspx) attribute defined in the .NET library should not be used as it will cause a crash if added to a Unity script.

