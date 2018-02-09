# Environment Shadow

You can use Look Dev to simulate environmental shadows. Note that this simulation is not completely accurate, and only shows harsh shadows.

To simulate environmental shadows, click the __Environment Shadow__ button in the top menu of the Look Dev window (highlighted in the image below).

![The top menu of the Look Dev window with the __Environment Shadow__ button highlighted](../uploads/Main/LookDevEnvironmentShadow-Button-0.png)

Use the HDRI view to control the direction of the shadows. When you toggle the __Environment Shadow__ on, a sun icon appears over the selected HDRI in the browser. Click and drag this to orient the shadow, and hold Shift+left click to manipulate the shadow direction. 

![Manipulate the sun icon (here in the middle pane on the right-hand screen) to control shadow direction](../uploads/Main/LookDevEnvironmentShadow-ShadowManipulate-1.png)

__Environment Shadow__ works best when there is a key light source in the HDRI (like the Sun, or a lamp). To make that a light source, drag and drop the sun icon on top of it. By default, the light source is set up on the brightest texel of the HDRI. For more evenly distributed light sources (like an overcast sky), this might not give accurate or expected results.

When __Environment Shadow__ is enabled, Look Dev uses one HDRI for the Prefab when it is lit by the key light source (this is called the __Lit HDRI__), and one for the Prefab when it is in the shadow of the key light source (this is called the __Shadow HDRI__). The shadow in the __Shadow HDRI__ is based on the light direction from the light icon. By default, the __Shadow HDRI__ is the same as the __Lit HDRI__, but with reduced luminosity.

To get more accurate results, provide your own __Shadow HDRI__. For best results, make this the same as the __Lit HDRI__ but without the key light source (for example, by removing the Sun from the image).

To pair up a __Shadow HDRI__ and a __Lit HDRI__, drag and drop the __Shadow HDRI__ onto the __Lit HDRI__. The __Shadow HDRI__ appears over the __Lit HDRI__ with a moon icon, as shown in the image below.

![Pairing up a __Shadow HDRI__ and a __Lit HDRI__](../uploads/Main/LookDevEnvironmentShadow-ShadowAndLit-2.png)

When __Environment Shadow__ is enabled, the __Lit HDRI__ switches to the assigned __Shadow HDRI__.

To remove the __Shadow HDRI__, click on the cross.

![Click on the cross to remove the __Shadow HDRI__](../uploads/Main/LookDevEnvironmentShadow-RemoveShadowHDRI-3.png)

 __Note__: You can manipulate __Shadow HDRI__ like any other HDRI in the library.