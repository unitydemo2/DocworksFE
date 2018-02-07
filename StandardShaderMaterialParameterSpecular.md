#Specular mode: Specular parameter

![](../uploads/Main/StandardShaderSpecularMode.png)

###Specular parameter
The __Specular__ parameter is only visible when using the __Specular setup__, as shown in the __Shader__ field in the image above. Specular effects are essentially the direct reflections of light sources in your Scene, which typically show up as bright highlights and shine on the surface of objects (although specular highlights can be subtle or diffuse too).

![](../uploads/Main/StandardShaderParameterSpecularSmoothness.png)

Both the __Specular setup__ and __Metallic setup__ produce specular highlights, so the choice of which to use is more a matter of setup and your artistic preference. In the __Specular setup__ you have direct control over the brightness and tint colour of specular highlights, while in the __Metallic setup__ you control other parameters and the intensity and colour of the specular highlights emerge as a natural result of the other parameter settings.

When working in Specular mode, the RGB colour in the __Specular__ parameter controls the strength and colour tint of the specular reflectivity. This includes shine from light sources and reflections from the environment. The [Smoothness](StandardShaderMaterialParameterSmoothness) parameter controls the clarity of the specular effect. With a low smoothness value, even strong specular reflections appear blurred and diffuse. With a high smoothness value, specular reflections are crisper and clearer.

![The Specular Smoothness values from 0 to 1](../uploads/Main/StandardShaderReflectivityGraduationTable.svg)

You might want to vary the __Specular__ values across the surface of your material - for example, if your Texture contains a character's coat that has some shiny buttons. You would want the buttons to have a higher specular value than the fabric of the clothes. To achieve this, assign a Texture map instead of using a single slider value. This allows greater control over the the strength and colour of the specular light reflections across the surface of the material, according to the pixel colours of your specular map.

When a Texture is assigned to the __Specular__ parameter, both the __Specular__ parameter and __Smoothness__ slider disappear. Instead, the specular levels for the material are controlled by the values in the __Red__, __Green__ and __Blue__ channels of the Texture itself, and the [Smoothness](StandardShaderMaterialParameterSmoothness) levels for the material are controlled by the Alpha channel of the same Texture. This provides a single Texture which defines areas as being rough or smooth, and have varying levels and colors of specularity. This is very useful when working Texture maps that cover many areas of a model with varying requirements; for example, a single character Texture map often includes multiple surface requirements such as leather shoes, fabric of the clothes, skin for the hands and face, and metal buckles.

![An example of a 1000kg weight with a strong specular reflection from a directional light.](../uploads/Main/StandardShaderSpecularCol1000kgWeight.png)

Here, the specular reflection and smoothness are defined by a colour and the __Smoothness__ slider. No Texture has been assigned, so the specular and smoothness level is constant across the whole surface. This is not always desirable, particularly in the case where your Albedo Texture maps to a variety of different areas on your model (also known as a Texture atlas).

![The same model, but with a specular map assigned, instead of using a constant value.](../uploads/Main/StandardShaderSpecularMap1000kgWeight.png)

Here, a Texture map controls the specularity and smoothness. This allows the specularity to vary across the surface of the model. Notice the edges have a higher specular effect than the centre, there are some subtle colour responses to the light, and the area inside the lettering no longer has specular highlights. Pictured to the right are the RGB channels controlling the specular colour and strength, and the Alpha channel controlling the smoothness.

**Note**: A black specular color (0,0,0) results in nulling out the specular effect.