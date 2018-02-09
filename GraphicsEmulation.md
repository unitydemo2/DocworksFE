#Graphics hardware capabilities and emulation


The graphics hardware that ultimately renders a Scene is controlled by specialised programs called [Shaders](class-Shader). The capabilities of the hardware have improved over time, and the general set of features that were introduced with each phase is known as a [Shader Model](SL-ShaderCompileTargets). Successive Shader Models have added support for longer programs, more powerful branching instructions and other features, and these have enabled improvements in the graphics of games.

The Unity Editor supports emulation of several sets of Shader Models and graphics API restrictions, for getting a quick overview of how the game might look like when running on a particular GPU or graphics API. Note that the in-editor emulation is very approximate, and it is always advisable to actually run the game build on the hardware you are targeting.


To choose the graphics emulation level, go to the __Edit__ > __Graphics Emulation__ menu. Note that the available options change depending on the platform you are currently targeting in the [Build Settings](BuildSettings). You can restore the full capabilities of your hardware by choosing __No Emulation__. If your development computer doesn't support a particular Shader Model then the menu entry will be disabled.




#### Shader Model 4 (Standalone & Windows Store platforms)


* Emulates DirectX 10 feature set (PC GPUs made during 2007-2009).
* Turns off support for [compute Shaders](ComputeShaders)
  and related features (compute buffers, random-write Textures),
  [sparse Textures](SparseTextures), and tessellation Shaders.




#### Shader Model 3 (Standalone platform)


* Emulates DirectX 9 SM3.0 feature set (PC GPUs made during 2004-2006).
* In addition to features turned off by Shader Model 4 emulation,
  this also turns off support for [draw call instancing](GPUInstancing),
  [Texture Arrays](SL-TextureArrays), and geometry Shaders. It enforces a
  maximum of 4 simultaneous render targets, and a maximum of 16
  Textures used in a single Shader.




#### Shader Model 2 (Standalone platform)


* Emulates DirectX 9 SM2.0 feature set (PC GPUs made during 2002-2004).
* In addition to features turned off by Shader Model 3 emulation,
  this also turns off support for [HDR rendering](HDR),
  [Linear color space](LinearLighting) and
  [depth Textures](SL-DepthTextures).




#### OpenGL ES 3.0 (Android platform)


* Emulates mobile OpenGL ES 3.0 feature set.
* Turns off support for [compute Shaders](ComputeShaders) and
  related features (compute buffers, random-write Textures),
  [sparse Textures](SparseTextures), tessellation Shaders and geometry
  Shaders. Enforces maximum of 4 simultaneous render targets,
  and maximum of 16 Textures used in a single Shader. Maximum
  allowed Texture size is set to 4096, and maximum cubemap size
  to 2048. Realtime soft shadows are disabled.




#### Metal (iOS, tvOS platforms)


* Emulates mobile Metal feature set.
* Same restrictions applied as GLES3.0 emulation, except that
  the maximum cubemap size is set to 4096.




#### OpenGL ES 2.0 (Android, iOS, tvOS, Tizen platforms)


* Emulates mobile OpenGL ES 2.0 feature set.
* In addition to features turned off by GLES3.0 emulation,
  this also turns off support for [draw call instancing](GPUInstancing),
  [Texture arrays](SL-TextureArrays), 3D Textures and multiple
  render targets. Enforces a maximum of 8 Textures used in a
  single Shader. Maximum allowed cubemap size is set to 1024.


#### WebGL 1 and WebGL 2 (WebGL platform)


* Emulates typical [WebGL](webgl-graphics) graphics restrictions.
* Very similar to GLES2.0 and GLES3.0 emulation levels above, except that
  supported Texture sizes are higher (8192 for regular Textures,
  4096 for cubemaps), and 16 Textures are allowed in a single
  Shader.


#### Shader Model 2 - DX11 FL9.3 (Windows Store Platform)


* Emulates typical Windows Phone graphics feature set.
* Very similar to Shader Model 2 emulation, but also disables
  multiple render targets and separate alpha blending.