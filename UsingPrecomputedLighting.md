# Using precomputed lighting

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|


In Unity, precomputed lighting is calculated in the background either as an automatic process or when manually initiated. In either case, it is possible to continue working in the editor while these processes run behind the scenes.

When the precompute process is running, a blue progress bar will appear in the bottom right of the Editor. There are different stages which need to be completed depending on whether Baked GI or Precomputed Realtime GI is enabled. Information on the current process is shown on-top of the progress bar.

![](../uploads/GlobalIllumination/BakingJobs.png)

Progress bar showing the current state of Unity’s precompute.

In the example above, we can see that we are at task 5 of 11 which is, ‘Clustering’ and there are 6 jobs remaining before that task is complete and the precompute moves on to task 6. The various stages are listed below:

__Precomputed Realtime GI__

1. Create Geometry			
2. Layout Systems				
3. Create Systems				
4. Create Atlas				
5. Clustering					
6. Visibility					
7. Light Transport			
8. Tetrahedralize Probes			
9. Create ProbeSet			
								
__Probes__

1. Ambient Probes				
2. Baked/Realtime Ref. Probes	

__Baked GI__

1. Create Geometry
2. Atlassing
3. Create Baked Systems
4. Baked Resources
5. Bake AO
6. Export Baked Texture
7. Bake Visibility
8. Bake Direct
9. Ambient and Emissive
10. Create Bake Systems
11. Bake Runtime
12. Upsampling Visibility
13. Bake Indirect
14. Final Gather
15. Bake ProbesSet
16. Compositing

##Starting a precompute

Only static geometry is considered by Unity’s precomputed lighting solutions. To begin the lighting precompute process we need at least one GameObject marked as ‘static’ in our scene. This can either be done individually, or by shift-selecting multiple GameObjects from the hierarchy panel.

From the Inspector panel, the Static checkbox can be selected (**Inspector > Static**). This will set all of the GameObject’s ‘static options’, or ‘flags’, including navigation and batching, to be static, which may not be desirable. For Precomputed Realtime GI, only 'Lightmap Static' needs to be checked.

For more fine-grained control, individual static options can be set from the drop-down list accessible to the right of the Static checkbox in the Inspector panel. Additionally, objects can also be set to Static in the Object area of the lighting window.

If your scene is set to Auto (**Lighting > Scene > Auto**), Unity’s lighting precompute will now begin automatically. Otherwise it will need to be started manually as described below.

##Auto/manual precompute

If ‘Auto’ is checked from the bottom of Unity’s Lighting panel (**Lighting > Scene > Auto**), then this precompute will begin automatically as a background process whenever changes are made to static geometry within your scene.

However, if Auto is not selected, you will need to manually start a precompute by clicking the ‘Build’ button next to it. This will begin the precompute in much the same way, while giving you control over when this process starts.

Manually initiating a precompute will cause all aspects of your scene lighting to be evaluated and (re)computed. If you wish to selectively recalculate Reflection probes by themselves, this can be done via the drop-down menu next to the Build button (**Lighting > Scene > Build**).

##Enabling baked GI or precomputed realtime GI

By default, both Precomputed Realtime GI and Baked GI are enabled in Unity’s Lighting panel (**Lighting > Scene**). With both enabled, which technique is used can then be controlled by each light individually (**Inspector > Light > Baking**).

Using both Baked GI and Precomputed Realtime GI together in your scene can be detrimental to performance. A good practise is to ensure that only one system is used at a time, by disabling the other globally. This can be done by unchecking the box next to either Precomputed Realtime GI or Baked GI from Unity’s lighting panel (**Lighting > Scene)**. Now only the checked option will be present in your scene, and any settings configured per-light will be overridden.

##Per-light settings

The default baking mode for each light is ‘Realtime’. This means that the selected light(s) will still contribute direct light to your scene, with indirect light handled by Unity’s Precomputed Realtime GI system.

However, if the baking mode is set to ‘Baked’ then that light will contribute lighting solely to Unity’s Baked GI system. Both direct and indirect light from those lights selected will be ‘baked’ into lightmaps and cannot be changed during gameplay.

![](../uploads/GlobalIllumination/LightBakingType.png)

Baking ModePoint light with the per-light Baking mode set to ‘Realtime’.

Selecting the ‘Mixed’ baking mode, GameObjects marked as static will still include this light in their Baked GI lightmaps. However, unlike lights marked as ‘Baked’, Mixed lights will still contribute realtime, direct light to non-static GameObjects within your scene. This can be useful in cases where you are using lightmaps in your static environment, but you still want a character to use these same lights to cast realtime shadows onto lightmapped geometry.

##GI cache

In either Baked GI or Precomputed Realtime GI, Unity ‘caches’ (stores) data about your scene lighting in the ‘GI Cache’, and will try to reuse this data whenever possible to save time during precompute. The number and nature of the changes you have made to your scene will determine how much of this data can be reused, if at all.

This cache is stored outside of your Unity project and can be cleared using (**Preference > GI Cache > Clear Cache**). Clearing this means that all stages of the precompute will need to be recalculated from the beginning and this can therefore be time consuming. However in some cases, where perhaps you need to reduce disk usage, this may be helpful.

##LOD for baked GI

Level-of-detail is taken into consideration when Unity generates baked lightmaps. Direct lighting is computed using the actual surfaces of all LODs. Lower LOD levels use light probes to fetch indirect lighting. The resulting lighting is baked into lightmap.

This means that you should place light probes around your LODs to capture indirect lighting. The object will not use lightprobes at runtime if you use fully baked GI.