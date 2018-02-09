#ShaderLab: CustomEditor



A CustomEditor can be defined for your shader. When you do this Unity will look for a class that extends ShaderGUI with this name. If one is found any material that uses this shader will use this ShaderGUI. See [Custom Shader GUI](SL-CustomShaderGUI) for examples.



##Syntax

````
	CustomEditor "name"
````
Use the ShaderGUI with a given _name_.


##Details

A CustomEditor statement effects all materials that use this Shader


##Example

````
Shader "example" {
    // properties and subshaders here...
    CustomEditor "MyCustomEditor"
}
````
