#Albedo Color and Transparency

![A Standard Shader material with default parameters and no values or textures assigned. The Albedo Color parameter is highlighted.](../uploads/Main/StandardShaderParameterAlbedoColor.png)

The Albedo parameter controls the base color of the surface.

![A range of black to white albedo values](../uploads/Main/StandardShaderAlbedoGraduationTable.svg)

Specifying a single color for the Albedo value is sometimes useful, but it is far more common to assign a texture map for the Albedo parameter. This should represent the colors of the surface of the object. It's important to note that the Albedo texture should **not** contain any lighting, since the lighting will be added to it based on the context in which the object is seen.

![Two examples of typical Albedo texture maps. On the left is a texture map for a character model, and on the right is a wooden crate. Notice there are no shadows or lighting highlights.](../uploads/Main/StandardShaderAlbedoTextureExamples.png)

##Transparency
The alpha value of the Albedo colour controls the transparency level for the material. This only has an effect if the Rendering Mode for the material is set to one of the transparent mode, and not **Opaque**. As mentioned above, picking the correct transparency mode is important because it determines whether or not you will still see reflections and specular highlights at full value, or whether they will be faded out according to the transparency values too.

![A range of transparency values from 0 to 1, using the Transparent mode suitable for realistic transparent objects](../uploads/Main/StandardShaderTransparencyGraduationTable.png)

When using a texture assigned for the Albedo parameter, you can control the transparency of the material by ensuring your albedo texture image has an **alpha channel**. The alpha channel values are mapped to the transparency levels with white being fully opaque, and black being fully transparent. This will have the effect that your material can have areas of varying transparency.

![An imported texture with RGB channels and an Alpha Channel. You can click the RGB/A button as shown to toggle which channels of the image you are previewing.](../uploads/Main/StandardShaderTransparencyMapRGBAlphaToggle.png)

![The end result, peering through a broken window into a building. The gaps in the glass are totally transparent, while the glass shards are partially transparent and the frame is fully opaque.](../uploads/Main/StandardShaderTransparencyMapBrokenWindow.png)
