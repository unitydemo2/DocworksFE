# Terrain settings

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|

The final tool on the terrain toolbar is for settings:

![](../uploads/Main/TerrainSettingsTool.png)


##Settings Inspector

Settings are provided for a number of overall usage and rendering options as described below:

![](../uploads/Main/TerrainSettingsInsp.png)

###Base Terrain

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Draw__ |Toggle the rendering of terrain on / off. |
|__Pixel Error__ |The accuracy of the mapping between the terrain maps (heightmap, textures, etc) and the generated terrain; higher values indicate lower accuracy but lower rendering overhead. |
|__Base Map Distance__ |The maximum distance at which terrain textures will be displayed at full resolution. Beyond this distance, a lower resolution composite image will be used for efficiency. |
|__Cast Shadows__ |Does the terrain cast shadows? |
|__Material__ |The material used to render the terrain. This will affect how the color channels of a terrain texture are interpreted. See [Enabling Textures](terrain-Textures) for details. Available options are: |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Built In Standard_ |This is the PBR (Physically-Based Rendering) material introduced in Unity 5.0. For each splat layer, you can use one texture for albedo and smoothness, one texture for normal and one scalar value to tweak the metalness. For more information on PBR and the Standard shader, see [Standard Shader](shader-StandardShader). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Built In Legacy Diffuse_|This is the legacy built-in terrain material from Unity 4.x and before. It uses Lambert (diffuse term only) lighting model and has optional normal map support. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Built In Legacy Specular_|This built-in material uses BlinnPhong (diffuse and specular term) lighting model and has optional normal map support. You can specify the overall specular color and shininess for the terrain. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Custom_|Use a custom material of your choice to render the terrain. This material should use a shader that is specialised for terrain rendering (e.g. it should handle texture splatting properly). We suggest you get a look at the source code of our built-in terrain shaders and make modifications on top of them. |
|__Reflection Probes__|How reflection probes are used on terrain. Only effective when using built-in standard material or a custom material which supports rendering with reflection. Available options are: |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Off_|Reflection probes are disabled, skybox will be used for reflection. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Blend Probes_|Reflection probes are enabled. Blending occurs only between probes. Default reflection will be used if there are no reflection probes nearby, but no blending between default reflection and probe will occur. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Blend Probes And Skybox_|Reflection probes are enabled. Blending occurs between probes or probes and default reflection. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;_Simple_|Reflection probes are enabled, but no blending will occur between probes when there are two overlapping volumes. |
|__Thickness__ |How much the terrain collision volume should extend along the negative Y-axis. Objects are considered colliding with the terrain from the surface to a depth equal to the thickness. This helps prevent high-speed moving objects from penetrating into the terrain without using expensive continuous collision detection. |

###Tree and Detail Objects

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Draw__ |Should trees, grass and details be drawn? |
|__Detail Distance__ |The distance (from camera) beyond which details will be culled. |
|__Detail Density__ |The number of detail/grass objects in a given unit of area. The value can be set lower to reduce rendering overhead. |
|__Tree Distance__ |The distance (from camera) beyond which trees will be culled. |
|__Billboard Start__ |The distance (from camera) at which 3D tree objects will be replaced by billboard images. |
|__Fade length__ |Distance over which trees will transition between 3D objects and billboards. |
|__Max Mesh Trees__ |The maximum number of visible trees that will be represented as solid 3D meshes. Beyond this limit, trees will be replaced with billboards. |


###Wind Settings

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Speed__ |The speed of the wind as it blows grass. |
|__Size__ |The size of the "ripples" on grassy areas as the wind blows over them. |
|__Bending__ |The degree to which grass objects are bent over by the wind. |
|__Grass Tint__ |Overall color tint applied to grass objects. |


###Resolution

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Terrain Width__ |Size of the terrain object in its X axis (in world units). |
|__Terrain Length__ |Size of the terrain object in its Z axis (in world units). |
|__Terrain Height__ |Difference in Y coordinate between the lowest possible heightmap value and the highest (in world units). |
|__Heightmap Resolution__ |Pixel resolution of the terrain's heightmap (should be a power of two plus one, eg, 513 = 512 + 1). |
|__Detail Resolution__ |Resolution of the map that determines the separate patches of details/grass. Higher resolution gives smaller and more detailed patches. |
|__Detail Resolution Per Patch__ |Length/width of the square of patches renderered with a single draw call. |
|__Control Texture Resolution__ |Resolution of the "splatmap" that controls the blending of the different terrain textures. |
|__Base Texture Resolution__ |Resolution of the composite texture used on the terrain when viewed from a distance greater than the _Basemap Distance_ (see above). |


###Heightmap Import/Export Buttons
The _Import Raw_ and _Export Raw_ buttons allow you to set or save the terrain's heightmap to an image file in the RAW grayscale format. RAW format can be generated by third party terrain editing tools (such as Bryce) and can also be opened, edited and saved by Photoshop. This allows for sophisticated generation and editing of terrains outside Unity.

