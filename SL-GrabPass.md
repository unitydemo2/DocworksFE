# ShaderLab: GrabPass

GrabPass is a special pass type - it grabs the contents of the screen where the object is about to be drawn into a texture. This texture can be used in subsequent passes to do advanced image based effects.

## Syntax

The GrabPass belongs inside a [subshader](SL-SubShader). It can take two forms:

* Just `GrabPass { }` grabs the current screen contents into a texture. The texture can be accessed in further passes by `_GrabTexture` name. Note: this form of grab pass will do the time-consuming screen grabbing operation for each object that uses it.
* `GrabPass { "TextureName" }` grabs the current screen contents into a texture, but will only do that once per frame for the first object that uses the given texture name. The texture can be accessed in further passes by the given texture name. This is a more performant method when you have multiple objects using GrabPass in the scene.

Additionally, GrabPass can use [Name](SL-Name) and [Tags](SL-PassTags) commands.


## Example


Here is an inefficient way to invert the colors of what was rendered before:


````
Shader "GrabPassInvert"
{
    SubShader
    {
        // Draw ourselves after all opaque geometry
        Tags { "Queue" = "Transparent" }

        // Grab the screen behind the object into _BackgroundTexture
        GrabPass
        {
            "_BackgroundTexture"
        }

        // Render the object with the texture generated above, and invert the colors
        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"

            struct v2f
            {
                float4 grabPos : TEXCOORD0;
                float4 pos : SV_POSITION;
            };

            v2f vert(appdata_base v) {
                v2f o;
                // use UnityObjectToClipPos from UnityCG.cginc to calculate 
                // the clip-space of the vertex
                o.pos = UnityObjectToClipPos(v.vertex);
                // use ComputeGrabScreenPos function from UnityCG.cginc
                // to get the correct texture coordinate
                o.grabPos = ComputeGrabScreenPos(o.pos);
                return o;
            }

            sampler2D _BackgroundTexture;

            half4 frag(v2f i) : SV_Target
            {
                half4 bgcolor = tex2Dproj(_BackgroundTexture, i.grabPos);
                return 1 - bgcolor;
            }
            ENDCG
        }

    }
}
````


This shader has two passes: The first pass grabs whatever is behind the object at the time of rendering, then applies that in the second pass. Note that the same effect could be achieved more efficiently using an invert [blend mode](SL-Blend).


## See Also


* [Regular Pass command](SL-Pass).
* [Platform differences](SL-PlatformDifferences).
* [Built-in shader helper functions](SL-BuiltinFunctions).
