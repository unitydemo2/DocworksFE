#ShaderLab: Blending

Blending is used to make transparent objects.


![](../uploads/SL/PipelineBlend.png) 

When graphics are rendered, after all Shaders have executed and all Textures have been applied, the pixels are written to the screen. How they are combined with what is already there is controlled by the Blend command.


##Syntax

`Blend Off`: Turn off blending (this is the default)

`Blend SrcFactor DstFactor`: Configure and enable blending. The generated color is multiplied by the **SrcFactor**. The color already on screen is multiplied by **DstFactor** and the two are added together.

`Blend SrcFactor DstFactor, SrcFactorA DstFactorA`: Same as above, but use different factors for blending the alpha channel.

`BlendOp Op`: Instead of adding blended colors together, carry out a different operation on them.

`BlendOp OpColor, OpAlpha`: Same as above, but use different blend operation for color (RGB) and alpha (A) channels.

Additionally, you can set upper-rendertarget blending modes. When
using multiple render target (MRT) rendering, the regular syntax
above sets up the same blending modes for all render targets. The following syntax can set up different blending modes for individual render targets, where `N` is the render target index (0..7). This feature works on most modern APIs/GPUs (DX11/12, GLCore, Metal, PS4):

* `Blend N SrcFactor DstFactor`
* `Blend N SrcFactor DstFactor, SrcFactorA DstFactorA`
* `BlendOp N Op`
* `BlendOp N OpColor, OpAlpha`

`AlphaToMask On`: Turns on alpha-to-coverage. When MSAA is used, alpha-to-coverage modifies multisample coverage mask proportionally to the pixel Shader result alpha value. This is typically used for less aliased outlines than regular alpha test; useful for vegetation and other alpha-tested Shaders.


##Blend operations

The following blend operations can be used:


| | |
|:---|:---|
|**Add** |Add source and destination together. |
|**Sub** |Subtract destination from source. |
|**RevSub** |Subtract source from destination. |
|**Min** |Use the smaller of source and destination. |
|**Max** |Use the larger of source and destination. |
|**LogicalClear** |Logical operation: Clear (0) **DX11.1 only**. |
|**LogicalSet** |Logical operation: Set (1) **DX11.1 only**. |
|**LogicalCopy** |Logical operation: Copy (s) **DX11.1 only**. |
|**LogicalCopyInverted** |Logical operation: Copy inverted (!s) **DX11.1 only**. |
|**LogicalNoop** |Logical operation: Noop (d) **DX11.1 only**. |
|**LogicalInvert** |Logical operation: Invert (!d) **DX11.1 only**. |
|**LogicalAnd** |Logical operation: And (s & d) **DX11.1 only**. |
|**LogicalNand** |Logical operation: Nand !(s & d) **DX11.1 only**. |
|**LogicalOr** |Logical operation: Or (s \| d) **DX11.1 only**. |
|**LogicalNor** |Logical operation: Nor !(s \| d) **DX11.1 only**. |
|**LogicalXor** |Logical operation: Xor (s ^ d) **DX11.1 only**. |
|**LogicalEquiv** |Logical operation: Equivalence !(s ^ d) **DX11.1 only**. |
|**LogicalAndReverse** |Logical operation: Reverse And (s & !d) **DX11.1 only**. |
|**LogicalAndInverted** |Logical operation: Inverted And (!s & d) **DX11.1 only**. |
|**LogicalOrReverse** |Logical operation: Reverse Or (s \| !d) **DX11.1 only**. |
|**LogicalOrInverted** |Logical operation: Inverted Or (!s \| d) **DX11.1 only**. |



##Blend factors

All following properties are valid for both SrcFactor & DstFactor in the **Blend** command. **Source** refers to the calculated color, **Destination** is the color already on the screen. The blend factors are ignored if **BlendOp** is using logical operations.


| | |
|:---|:---|
|**One** |The value of one - use this to let either the source or the destination color come through fully. |
|**Zero** |The value zero - use this to remove either the source or the destination values. |
|**SrcColor** |The value of this stage is multiplied by the source color value. |
|**SrcAlpha** |The value of this stage is multiplied by the source alpha value. |
|**DstColor** |The value of this stage is multiplied by frame buffer source color value. |
|**DstAlpha** |The value of this stage is multiplied by frame buffer source alpha value. |
|**OneMinusSrcColor** |The value of this stage is multiplied by (1 - source color). |
|**OneMinusSrcAlpha** |The value of this stage is multiplied by (1 - source alpha). |
|**OneMinusDstColor** |The value of this stage is multiplied by (1 - destination color). |
|**OneMinusDstAlpha** |The value of this stage is multiplied by (1 - destination alpha). |


##Details

Below are the most common blend types:

````
Blend SrcAlpha OneMinusSrcAlpha // Traditional transparency
Blend One OneMinusSrcAlpha // Premultiplied transparency
Blend One One // Additive
Blend OneMinusDstColor One // Soft Additive
Blend DstColor Zero // Multiplicative
Blend DstColor SrcColor // 2x Multiplicative
````


## Alpha blending, alpha testing, alpha-to-coverage

For drawing mostly fully opaque or fully transparent objects, where transparency is defined by the Texture's alpha channel (e.g. leaves, grass, chain fences etc.), several approaches are commonly used:


#### Alpha blending

![Regular alpha blending](../uploads/SL/AlphaToMask-Blending.png) 

This often means that objects have to be considered as "semitransparent", and thus can't use some of the rendering features (for example: deferred shading, can't receive shadows). Concave or overlapping alpha-blended objects often also have draw ordering issues.

Often, alpha-blended Shaders also set transparent [render queue](SL-SubShaderTags), and turn off depth writes. So the Shader code looks like:

```
// inside SubShader
Tags { "Queue"="Transparent" "RenderType"="Transparent" "IgnoreProjector"="True" }

// inside Pass
ZWrite Off
Blend SrcAlpha OneMinusSrcAlpha
```


#### Alpha testing/cutout

![clip() in pixel Shader](../uploads/SL/AlphaToMask-clip.png) 

By using `clip()` HLSL instruction in the pixel Shader, a pixel can be "discarded" or not based on some criteria. This means that object can still be considered as fully opaque, and has no draw ordering issues. However, this means that all pixels are fully opaque or transparent, leading to aliasing ("jaggies").

Often, alpha-tested Shaders also set cutout [render queue](SL-SubShaderTags), so the Shader code looks like this:

```
// inside SubShader
Tags { "Queue"="AlphaTest" "RenderType"="TransparentCutout" "IgnoreProjector"="True" }

// inside CGPROGRAM in the fragment Shader:
clip(textureColor.a - alphaCutoffValue);
```



#### Alpha-to-coverage

![AlphaToMask On, at 4xMSAA](../uploads/SL/AlphaToMask-4x.png) 

When using multisample anti-aliasing (MSAA, see [QualitySettings](class-QualitySettings)), it is possible to improve the alpha testing approach by using alpha-to-coverage GPU functionality. This improves edge appearance, depending on the MSAA level used.

This functionality works best on texures that are mostly opaque or transparent, and have very thin "partially transparent" areas (grass, leaves and similar).

Often, alpha-to-coverage Shaders also set cutout [render queue](SL-SubShaderTags). So the Shader code looks like:

```
// inside SubShader
Tags { "Queue"="AlphaTest" "RenderType"="TransparentCutout" "IgnoreProjector"="True" }

// inside Pass
AlphaToMask On
```



##Example

Here is a small example Shader that adds a Texture to whatever is on the screen already:

````
Shader "Simple Additive" {
    Properties {
        _MainTex ("Texture to blend", 2D) = "black" {}
    }
    SubShader {
        Tags { "Queue" = "Transparent" }
        Pass {
            Blend One One
            SetTexture [_MainTex] { combine texture }
        }
    }
}
````
