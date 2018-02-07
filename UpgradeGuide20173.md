#Upgrading to Unity 2017.3

<!-- Change submissions: https://docs.google.com/document/d/1Vi8WlG3ysu1RHrkNWPQ_N2q9glmSI8wr33fm2VCWNQ8/edit -->

This page lists any changes in 2017.3 which might affect existing projects when you upgrade from earlier versions of Unity.

For example:

* Changes in data format which may require re-baking.

* Changes to the meaning or behavior of any existing functions, parameters or component values.

* Deprecation of any function or feature. (Alternatives are suggested.)

***

**PassType.VertexLMRGBM has been deprecated**

In Unity 2017.3, the shader pass **VertexLMRGB** is ignored. For example: 
```
Tags { "LightMode" = "VertexLMRGBM" }
```

Instead, provide or update a **VertexLM** shader pass using the DecodeLightmap shader function that supports all types of lightmap encodings. Built-in mobile shaders also use DecodeLightmap shader function now. 

Lighting output may change in your existing projects that use built-in mobile shaders such as Mobile or VertexLit on desktop platforms. This is because the maximum range of RGBM encoded values has changed from [0, 8] to [0, 5].

----

* <span class="page-edit">2017-12-04  <!-- include IncludeTextNewPageSomeEdit --></span>