#Shadowmask mode

Shadowmask mode is a lighting mode shared by all Mixed Lights in a Scene. To set Mixed lighting to Shadowmask, open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), click the __Scene tab__, navigate to __Mixed Lighting__ and set the __Lighting Mode__ to __Shadowmask__. 

You also need to select the desired Shadowmask mode to use from the __Quality Settings__ (menu: __Edit__ > __Project Settings__ > __Quality__): 

* [Shadowmask](LightMode-Mixed-Shadowmask): Static GameObjects that cast shadows always use baked shadows.
* [Distance Shadowmask](LightMode-Mixed-DistanceShadowmask): Unity uses real-time shadows up to the __Shadow Distance__, and baked shadows beyond.

See documentation on [Mixed lighting](LightMode-Mixed) and [Light modes](LightModes) to learn more about the other modes available.

---

* <span class="page-edit">2017-09-18  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">Shadowmask modes added to Quality Settings in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>