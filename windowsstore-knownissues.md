#Known issues

This page contains known issues with apps built for the Universal Windows Platform caused by external factors that aren’t related to Unity, such as drivers and libraries.

|**Setup**|**Issue**|**Reason**|**Workaround**|
|:---|:---|:---|:---|
| Nokia Lumia 630/635/1520| Specific sampler ordering in the Shader causes the Texture Wrap mode to change to Clamp mode. This might also be reproduced on other 3xx Adreno devices. | Adreno driver bug.| Change the sampler register for the affected Texture in the Shader code file (for example, change `sampler2D _MainTex;` to `sampler2D _MainTex:register(s0);`). |
|UWP| Scrolling the mouse wheel can break mouse movement if the cursor is locked (if [Cursor.lockState](ScriptRef:Cursor-lockState.html) `!= None`). | Windows OS issue.| Open the __Player Settings__ (__Edit__ > __Project Settings__ > __Player__). Select the __Publishing Settings__ tab, and tick the __Independent Input Source__ checkbox. |
|UWP .Net Native| The functions `Terrain.GetHeights`, `Terrain.SetHeights`, and `Terrain.SetHeightsDelayLOD` crash the player.| .Net Native bug when calling `GCHandle.Alloc` with multi-dimensional arrays.| Currently no workaround.|

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>