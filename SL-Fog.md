#ShaderLab: Legacy Fog

Fog parameters are controlled with Fog command.

Fogging blends the color of the generated pixels down towards a constant color based on distance from camera. Fogging does not modify a blended pixel's alpha value, only its RGB components.



##Syntax

###Fog
````
	Fog {Fog Commands}
````
Specify fog commands inside curly braces.

###Mode
````
	Mode Off | Global | Linear | Exp | Exp2
````
Defines fog mode. Default is global, which translates to Off or Exp2 depending whether fog is turned on in Render Settings.

###Color
````
	Color ColorValue
````
Sets fog color.

###Density
````
	Density FloatValue
````
Sets density for exponential fog.

###Range
````
	Range FloatValue, FloatValue
````
Sets near & far range for linear fog.



##Details

Default fog settings are based on settings in the [Lighting Window](GlobalIllumination): fog mode is either __Exp2__ or __Off__; density & color taken from settings as well.

Note that if you use [fragment programs](SL-ShaderPrograms), Fog settings of the shader will still be applied. On platforms where there is no fixed function Fog functionality, Unity will patch shaders at runtime to support the requested Fog mode.
