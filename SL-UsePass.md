# ShaderLab: UsePass

The UsePass command uses named passes from another shader.

## Syntax

````
UsePass "Shader/Name"
````

Inserts all passes with a given name from a given shader. _Shader/Name_ contains the name of the shader and the name of the pass, separated by a slash character. Note that only first supported [subshader](SL-SubShader) is taken into account.


## Details


Some of the shaders could reuse existing passes from other shaders, reducing code duplication. For example, you might have a shader pass that draws object outline, and you'd want to reuse that pass in other shaders. The UsePass command does just that - it includes a given pass from another shader. As an example the following command uses the pass with the name "SHADOWCASTER" from the built-in _VertexLit_ shader:

````
UsePass "VertexLit/SHADOWCASTER"
````

In order for UsePass to work, a name must be given to the pass one wishes to use. The [Name](SL-Name) command inside the pass gives it a name:

````
Name "MyPassName"
````

Note that internally all pass names are uppercased, so UsePass must refer to the name **in uppercase**.
