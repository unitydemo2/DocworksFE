Debugging on Blackberry10
=========================


When the game runs on device it will write a log file. This is where your `Debug.Log` messages will go, together with any asserts, information and error messages from Unity. You can fetch this log from the device from the editor. Use Edit-&gt;Project Settings-&gt;Player-&gt;Publishing Settings-&gt;Get Log. The log can be written to the hard drive of your computer. An example log file is:


````
Set current directory to /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc
Found path: /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/com.unity.doc.testDev_ProductName5a2477fc
Data folder: /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data
Loading in pref's!
Mono path[0] = '/accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed'
Mono config path = '/accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed'
Renderer: Adreno (TM) 225
Vendor: Qualcomm
Version: OpenGL ES 2.0 2644020
GL_AMD_compressed_ATC_texture GL_AMD_performance_monitor GL_AMD_program_binary_Z400 GL_EXT_robustness GL_EXT_texture_format_BGRA8888
GL_EXT_texture_type_2_10_10_10_REV GL_NV_fence GL_OES_compressed_ETC1_RGB8_texture GL_OES_depth_texture GL_OES_depth24 GL_OES_EGL_image
GL_OES_EGL_image_external GL_OES_element_index_uint GL_OES_fbo_render_mipmap GL_OES_fragment_precision_high GL_OES_get_program_binary
GL_OES_packed_depth_stencil GL_OES_rgb8_rgba8 GL_OES_standard_derivatives GL_OES_texture_3D GL_OES_texture_float GL_OES_texture_half_float
GL_OES_texture_half_float_linear GL_OES_texture_npot GL_OES_vertex_half_float GL_OES_vertex_type_10_10_10_2 GL_OES_vertex_array_object
GL_QCOM_alpha_test GL_QCOM_binning_control GL_QCOM_driver_control GL_QCOM_perfmon_global_mode GL_QCOM_extended_get GL_QCOM_extended_get2
GL_QCOM_tiled_rendering GL_QCOM_writeonly_rendering GL_AMD_compressed_3DC_texture GL_EXT_sRGB GL_EXT_texture_filter_anisotropic
GL_ANGLE_framebuffer_multisample GL_ANGLE_framebuffer_blit GL_OES_mapbuffer 
Creating OpenGLES2.0 graphics device
Initialize engine version: 4.2.0a1 (20a94a2c4d7f)
Begin MonoManager ReloadAssembly
Platform assembly: /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed/UnityEngine.dll (this message is harmless)
Loading /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed/UnityEngine.dll into Unity Child Domain
Platform assembly: /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed/Assembly-CSharp.dll (this message is harmless)
Loading /accounts/1000/appdata/com.unity.doc.testDev_ProductName5a2477fc/app/native/Data/Managed/Assembly-CSharp.dll into Unity Child Domain
- Completed reload, in 0.129 seconds

````
