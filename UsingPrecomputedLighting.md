# Using precomputed lighting

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

If you set your Scene to __Auto Generate__ (menu: __Window__ > __Lighting__ > __Settings__ > __Scene__ > __Auto Generate__), Unity’s lighting precompute begins automatically, and updates automatically when any static geometry in your Scene changes. If you do not enable __Auto Generate__, you must start the lighting precompute manually.

##Auto/manual precompute

If you have checked __Auto Generate__ in the bottom of Unity’s Lighting panel (menu: __Window__ > __Lighting > Settings > Scene > Auto Generate__), this precompute begins automatically as a background process whenever the static geometry within your Scene changes.

However, if you have not enabled __Auto Generate__, you must manually start the lighting precompute process by clicking the ‘Build’ button next to it. This begins the precompute in much the same way, and gives you control over when this process starts. 

__Auto Generate __can be useful when working on smaller or less complex Scenes, because it quickly produces accurate lighting results while you move or editing static GameObjects in your Scene. However, when working on large or complex Scenes, you might prefer to switch to the manual option, so that your computer is not running a high CPU usage and repeatedly re-starting the lighting precompute each time you modify your Scene.

When you manually initiate a precompute, all aspects of your Scene lighting are evaluated and computed. To recalculate and bake just the [Reflection Probes](class-ReflectionProbe) by themselves, click the drop-down menu attached to the __Generate Lighting __button (menu: __Window__ > __Lighting > Settings > Scene > Generate Lighting__) and select __Bake Reflection Probes__. 

**NOTE:** When using __Auto Generate__ mode, Unity stores your lighting data in a temporary cache with a limited size. This means that when you exceed the cache’s size, Unity deletes old lighting data. A problem might occur when building your project if some of your Scenes rely on auto-generated lighting data that has been deleted. In this case, your Scenes might not have the correct lighting in the built project. Therefore, before building your game, you should uncheck __Auto Generate, __and generate the lighting data manually for all your Scenes. Unity then saves your lighting data as Asset files in your project folder, which means you have the data saved as part of your project and included in your build.

##Enabling Baked GI or Realtime GI

Unity enables both __Baked GI__ and __Realtime GI__ by default. __Baked GI__ is all precomputed; __Realtime GI__ carries out some precomputation when indirect lighting is used. With both enabled, you then use each individual Light in your Scene to control which GI system it should use (in the Light component, use the __Mode__ setting to do this). See documentation on the [Lighting window](GlobalIllumination) and [Global Illumination](GIIntro) to learn more.

The most flexible way to use the lighting system is to use __Baked GI__ and __Realtime GI__ together. However, this is also the most performance-heavy option. To make your game less resource-intensive, you can choose to disable __Realtime GI__ or __Baked GI__. Note that doing this this reduces the flexibility and functionality of your lighting system.

To manually enable or disable Global Illumination, open the Lighting window (__Window__ > __Lighting__ > __Settings__ > __Scene__). Tick __Realtime Global Illumination__ to enable __Realtime GI__, and tick __Baked Global Illumination__ to enable __Baked GI__. Untick these checkboxes to disable the respective GI system. If any Lights are set to the mode you have disabled, they are are overridden and set to the active GI system.

##Per-light settings

To set properties for each individual Light, select it in the Scene or Hierarchy window, then edit the settings on the [Light component](class-Light) in the Inspector window.

The default __Mode__ for each light is __Dynamic__. This means that the Light contributes direct lighting to your Scene, and Unity’s __Realtime GI__ handles indirect lighting.

If you set the Light’s __Mode__ to __Static,__ then that Light only contributes lighting to Unity’s __Baked GI__ system. Both direct and indirect lighting from those Lights are baked into light maps, and cannot be changed during gameplay.

If you set the Light’s __Mode__ to __Stationary__, GameObjects marked as __Static__ still include this light in their __Baked GI__ light maps. However, unlike Lights marked as __Static__, __Stationary__ Lights still contribute real-time lighting, based on the stationary bake mode in the Lighting window (menu: __Window__ > __Lighting__ > __Settings__). This is useful if you are using light maps in a static environment, but you still want a good integration between dynamic and light map static geometry.

![A Directional Light with the __Mode__ set to __Dynamic__.](../uploads/GlobalIllumination/LightBakingType.png)

See documentation on [Lighting Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit?usp=sharing) for more details.

##GI cache

In either Baked GI or Precomputed Realtime GI, Unity caches (stores) data about your scene lighting in the ‘GI Cache’, and will try to reuse this data whenever possible to save time during precompute. The number and nature of the changes you have made to your scene will determine how much of this data can be reused, if at all.

This cache is stored outside of your Unity project and can be cleared using (__Preference__ > __GI Cache__ > __Clear Cache__). Clearing this means that all stages of the precompute will need to be recalculated from the beginning and this can therefore be time consuming. However in some cases, where perhaps you need to reduce disk usage, this may be helpful.

##LOD for baked GI

Level-of-detail is taken into consideration when Unity generates baked lightmaps. Direct lighting is computed using the actual surfaces of all LODs. Lower LOD levels use light probes to fetch indirect lighting. The resulting lighting is baked into lightmap.

This means that you should place light probes around your LODs to capture indirect lighting. The object will not use lightprobes at runtime if you use fully baked GI.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>