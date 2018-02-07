#UI Profiler 

The UI Profiler is a profiler module dedicated to in-game UI.

Access it via the [Profiler Window's](ProfilerWindow) menu: __Add Profiler__ > __UI and UI Details__.

![The UI and UI Details Profiler window](../uploads/Main/UI_Profiler_Image_1.png)

Use this feature to help with understanding the ui batching, why and how objects are batched, which part of the UI is responsible for a slow down, preview the UI or part of it when scrubbing the timeline.

Note that this Profiler is quite resource intensive, similar to other Profiler modules.

##Settings

The UI Details chart has a togglable __Markers__ group, similarl to what the CPU chart offers.
In the preview panel, there's a button __Detach__ and two drop-down menus.

* The Markers toggle displays or hide event markers on the UI details chart.

* Detach pops the preview out in a separate window.

* The two drop-down menus allow you to choose the preview background (black, white, or checkerboard) and the preview type  (original render, overdraw, or omposite overdraw).

##Helpful Notes

* Markers can be overwhelming, depending on the usecase profiled. Hiding or showing them when needed helps the chart readability.

* To make visibility clearer, you can select the preview background according to the UI you are previewing. A white-ish UI on a white background won't be readable, for example, so you can change it. 

* Detaching the preview allows better screen estate management.

* Overdraw and composite overdraw are used to determine which parts of the UI are drawn for nothing.

##Definitions

__Marker__: markers are recorded when the user interacts with the UI (button click, slider value change, ...) and then drawn, if enabled, as vertical lines and labels on the chart.

__Batch__:  the UI system tries to batch draw calls. There are many reasons two objects could not be batched together.
<br/>

**Batch Breaking Reasons**

* Not Coplanar With Canvas: <br/>The batching needs the object's rect transform to be coplanar (unrotated) with the canvas.

* CanvasInjectionIndex: <br/>A CanvasGroup component is present and forces a new batch, ie. when displaying the drop down list of a combo box on top of the rest.

* Different Material Instance, Rect clipping, Texture, A8TextureUsage: <br/>Only objects with identical materials, masking, textures, texture alpha channel usage can be batched together.
  

## Tips

Treeview rows have a context menu with a "find matching object in scene" entry, which is also triggerable by double clicking on a row.

<br/>

---

* <span class="page-edit">2017-05-17  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in Unity [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>


