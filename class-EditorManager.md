# Editor Settings


![](../uploads/Main/EditorSettings173.png)


## Properties

|| Property: | Function: |
|:---|:---|:---| 
| __Unity Remote__||| 
| __Device__|| [Unity Remote](UnityRemote5) is a downloadable app designed to help with Android, iOS and tvOS development. Use the drop-down to select the device type you want to use for Unity Remote testing. |
| __Compression__|| Use the drop-down to select the type of image compression Unity uses when transmitting the game screen to the device via Unity Remote. This is set to __JPEG__ by default. |
|| JPEG | JPEG usually gives higher compression and performance, but the graphics quality is a little lower. This is the default option. |
|| PNG | PNG gives a more accurate representation of the game display, but can result in lower performance. |
| __Resolution__|| Use the drop-down to select the resolution the game should run at on Unity Remote. This is set to __Downsize__ by default. |
|| Downsize | Choose __Downsize__ to display the game at a lower resolution. This results in better performance, but lower graphical accuracy. This is the default option. |
|| Normal | Choose __Normal__ to display the game at normal resolution. This results in better graphical accuracy, but lower performance. |
| __Joystick Source__|| Use the drop-down to select the connection source for the joysticks you are using. This is set to __Remote__ by default. |
|| Remote | Choose __Remote__ to use joysticks that are connected to a device running Unity Remote. This is the default option.  |
|| Local | Select __Local__ to use joysticks that are connected to the computer running the Editor. |
| __Version Control__|||
| __Mode__|| You can use Unity in conjunction with most common version control tools, including Perforce and PlasticSCM. See documentation on [Version Control](VersionControl) for more information. <br/>Use the drop-down to select the visibility of meta files. See documentation on [Version Control](VersionControl) for different options available for different systems. This is set to __Hidden Meta Files__ by default. For more information on showing or hiding meta files, see the Unity Answers page [Visible or hidden meta files](http://answers.unity3d.com/questions/932348/visible-or-hidden-meta-files-with-git.html). |
|| Hidden Meta Files | Set Unity to hide meta files. This is the default option. |
|| Visible Meta Files | Set Unity to display meta files. This is useful when using version control, because it allows other users and machines to view these meta files. |
| __Asset Serialization__|||
| __Mode__|| Unity uses [serialization](script-Serialization-BuiltInUse) to load and save Assets and AssetBundles to and from your computer’s hard drive. To help with version control merges, Unity can store Scene files in a text-based format (see documentation on [text scene format](TextSceneFormat) for further details). If Scene merges are not performed, Unity can store Scenes in a more space-efficient binary format, or allow both text and binary Scene files to exist at the same time. <br/>Use the drop-down to select which format Unity should use to store serialized Assets. This is set to __Force Text __by default. |
|| Mixed | Assets in Binary mode remain in Binary mode, and assets in Text mode remain in Text mode. Unity uses Binary mode by default for new Assets. |
|| Force Binary | This converts all Assets to Binary mode, and Unity uses Binary mode for new Assets. |
|| Force Text | This converts all Assets to Text mode, and Unity uses Text mode for new Assets. This is the default option. |
| __Default Behavior Mode__|||
| __Mode__|| Unity allows you to choose between 2D or 3D development, and sets up certain default behaviors depending on which one you choose, to make development easier. For more information on the specific behaviors that change with this setting, see documentation on [2D and 3D Mode settings](2DAnd3DModeSettings). <br/>Use the drop-down to choose a default behaviour for Unity. This is set to __3D__ by default. |
|| 3D | Choose __3D__ to set Unity up for 3D development. This is the default option. |
|| 2D | Choose __2D__ to set Unity up for 2D development.  |
| __Sprite Packer__|||
| __Mode__|| Unity provides a [Sprite Packer](SpritePacker) tool to automate the process of generating atlases from individual Sprite Textures. Use these settings to configure the Sprite Packer. Use the drop-down to select a Sprite Packer Mode. This is set to __Disabled__ by default. See documentation on [Sprite Atlas](SpriteAtlas) for more information. |
|| Disabled | Unity does not pack Atlases. This is the default setting. |
|| Enabled For Builds (Legacy Sprite Packer) | Unity packs Atlases for builds only, and not in-Editor Play mode. This __Legacy Sprite Packer__ option refers to the Tag-based version of the Sprite Packer, rather than the Sprite Atlas version. |
|| Always Enabled (Legacy Sprite Packer) | Unity packs Atlases for builds and before entering in-Editor Play mode. This __Legacy Sprite Packer__ option refers to the Tag-based version rather than the Sprite Atlas version. |
|| Enabled For Builds | Unity packs Atlases for builds only, and not in-Editor Play mode. |
|| Always Enabled | Unity packs Atlases for builds and before entering in-Editor Play mode. |
| __Padding Power (Legacy Sprite Packer)__|| Use __Padding Power__ to set the value that the packing algorithm uses when calculating the amount of space or "padding" to allocate between packed Sprites, and between Sprites and the edges of the generated atlas. |
|| 1 | This represents the value 2^1. Use this setting to allocate 2 pixels between packed Sprites and atlas edges. This is the default setting. |
|| 2 | This represents the value 2^2. Use this setting to allocate 4 pixels between packed Sprites and atlas edges. |
|| 3 | This represents the value 2^3. Use this setting to allocate 8 pixels between packed Sprites and atlas edges. |
| __C# Project Generation__|||
| __Additional extensions to include__|| Use this text field to include a list of additional file types to add to the C# Project. Separate each file type with a semicolon. By default, this field contains `txt;xml;fnt;cd`. |
| __Root namespace__|| Use this text field to fill in the namespace to use for the C# project `RootNamespace` property. See Microsoft developer documentation on [Common MSBuild Project Properties](https://msdn.microsoft.com/en-us/library/bb629394.aspx) for more information. This field is blank by default. |
| __ETC Texture Compressor__|||
| __Behavior__|| Unity allows you to specify the compression tool to use for different compression qualities of ETC Textures. The properties __Fast__, __Normal__ and __Best__ define the compression quality. These map to the __Compressor Quality __setting in the [Texture Importer](class-TextureImporter) for the supported platforms. The compression tools available are [etcpak](https://bitbucket.org/wolfpld/etcpak/wiki/Home), [ETCPACK](https://github.com/Ericsson/ETCPACK) and [Etc2Comp](https://github.com/google/etc2comp). These are all third-party compressor libraries. |
|| Legacy | Select __Legacy__ to use the configuration that was available before ETC Texture compression became configurable. This sets the following properties: <br/> - __Fast__: ETCPACK Fast <br/> - __Normal__: ETCPACK Fast <br/> - __Best__: ETCPACK Best |
|| Default | Select __Default__ to use the default configuration for Unity. This sets the following properties: <br/> - __Fast__: etcpack <br/> - __Normal__: ETCPACK Fast <br/> - __Best__: Etc2Comp Best |
|| Custom | Select __Custom__ to customise the ETC Texture compression configuration.  |
| __Line Endings For New Scripts__|||
| __Mode__|| Use the drop-down to configure file line endings to apply to new scripts created within the Editor. Note that configuring these settings does not convert existing scripts.  |
|| OS Native | Choose __OS Native__ to apply line endings based on the OS the Editor is running on. |
|| Unix | Choose __Unix__ to apply line endings based on the Unix OS. |
|| Windows | Choose __Windows__ to apply line endings based on the Windows OS. |

---

* <span class="page-history">2017-11-03 Documentation updated to reflect multiple changes since 5.6</span>

* <span class="page-edit"> 2017-11-03  <!-- include IncludeTextAmendPageYesEdit --></span>
