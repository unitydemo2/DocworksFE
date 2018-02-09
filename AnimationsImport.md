#Animation from external sources 

Animation from external sources is imported into Unity in the same way as regular 3D files. These files, whether they're generic FBX files or native formats from 3D software such as Maya, Cinema 4D, 3D Studio Max, can contain animation data in the form of a linear recording of the movements of objects within the file.

![An imported FBX 3D Asset containing an animation titled 'Run'](../uploads/Main/AnimationSelectingImportedClip.png) 

In some situations the object to be animated (eg, a character) and the animations to go with it can be present in the same file. In other cases, the animations may exist in a separate file to the model to be animated. 

It may be that animations are specific to a particular model, and cannot be re-used on other models. For example, a giant octopus end-boss in your game might have a unique arrangement of limbs and bones, and its own set of animations.

In other situations, it may be that you have a library of animations which are to be used on various different models in your scene. For example, a number of different humanoid characters might all use the same walk and run animations. In these situations, it's common to have a simple placeholder model in your animation files for the purposes of previewing them. Alternatively, it is possible to use animation files even if they have no geometry at all, just the animation data.

When importing multiple animations, the animations can each exist as separate files within your project folder, or you can extract multiple animation clips from a single FBX file if exported as takes from Motion builder or with a plugin / script for Maya, Max or other 3D packages. You might want to do this if your file contains multiple separate animations arranged on a single timeline. For example, a long motion captured timeline might contain the animation for a few different jump motions, and you may want to cut out certain sections of this to use as individual clips and discard the rest. Unity provides animation cutting tools to achieve this when you import all animations in one timeline by allowing you to select the frame range for each clip.

##Importing animation files

Before any animation can be used in Unity, it must first be imported into your project. Unity can import native Maya (.mb or .ma), 3D Studio Max (.max) and Cinema 4D (.c4d) files, and also generic FBX files which can be exported from most animation packages (see [this page](HOWTO-importObject) for further details on exporting).
To import an animation, simply drag the file to the __Assets__ folder of your project. When you select the file in the __Project View__ you can edit the __Import Settings__ in the inspector:

![The Import Settings Dialog for a mesh](../uploads/Main/MecanimImporterModelTab.png) 

See the [FBX importer](class-FBXImporter) page for a full description of the available import options.

##Viewing and copying data from imported animation files

You can view the keyframes and curves of imported animation clips in the Animation window. Sometimes, if these imported clips have lots of bones with lots of keyframes, the amount of information can look overwhelmingly complex. For example, the image below is what a humanoid running animation looks like in the Animation window:

![](../uploads/Main/AnimationViewingImportedCurves.png) 

To simplify the view, select the specific bones you are interested in examining. The Animation window then displays only the keyframes or curves for those bones.

![Limiting the view to just the selected bones](../uploads/Main/AnimationViewingImportedCurvesSelected.png) 

When viewing imported Animation keyframes, the Animation window provides a read-only view of the Animation data. To edit this data, create a new empty Animation Clip in Unity (see [Creating a new Animation Clip](animeditor-CreatingANewAnimationClip)), then select, copy and paste the Animation data from the imported Animation Clip into your new, writable Animation Clip.

![Selecting keyframes from an imported clip.](../uploads/Main/AnimationSelectingKeysOnImportedClip.png) 


