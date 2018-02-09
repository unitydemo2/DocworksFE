iOS Hardware Guide
==================


Hardware models
---------------


The following list summarizes iOS hardware available in devices of various generations. Current device shader performance can compared on [gfxbench](http://gfxbench.com/result.jsp?benchmark=gfx30&test=547&order=median&base=device&os-check-Android_gl=0&os-check-Windows_gl=0&arch-check-unknown=0&arch-check-x86=0) which compares different hardware features using benchmarks.


###[iPhone Models](http://en.wikipedia.org/wiki/IPhone#Model_comparison)


###iPhone 3GS

* Screen: 320x480 pixels, LCD at 163ppi
* ARM Cortex A8, 600 MHz CPU
* PowerVR SGX535 graphics processor
* 256MB of memory
* 3 megapixel camera with video capture capability
* GPS support
* Compass support


![](../uploads/Main/shadowgun2.jpg) 
iPhone 3GS: Shader-capable hardware, per-pixel-lighting (bumpmaps) can only be on small portions of the screen at once.
Requires scripting optimization for complex games. This is the average hardware of the app market as of July 2012

###iPhone 4

* Screen: 960x640 pixels, LCD at 326 ppi, 800:1 contrast ratio.
* Apple A4 1 GHz ARM Cortex-A8 CPU
* PowerVR SGX535 GPU
* 512MB of memory
* Rear 5.0 MP backside illuminated CMOS image sensor with 720p HD video at 30 fps and LED flash
* Front 0.3 MP (VGA) with geotagging, tap to focus, and 480p SD video at 30 fps
* GPS support
* Compass Support

###iPhone 4S

* Screen: 960x640 pixels, LCD at 326 ppi, 800:1 contrast ratio.
* Apple A5 Dual-Core 1 GHz ARM Cortex-A9 MPCore CPU
* Dual-Core PowerVR SGX543MP2 GPU
* 512MB of memory
* Rear 8.0 MP infra-red cut-off filter, back-illuminated sensor, 1080p HD videos at 30 fps.
* Front 0.3 MP (VGA) with geotagging, tap to focus, and 480p SD video at 30 fps
* GPS support
* Compass Support


![](../uploads/Main/csrCar.jpg) 
The iPhone 4S, with the new A5 chip, is capable of rendering complex shaders throughout the entire screen. Even image effects may be possible. However, optimizing your shaders is still crucial. But if your game isn't trying to push limits of the device, optimizing scripting and gameplay is probably as much of a waste of time on this generation of devices as it is on PC.

###iPhone 5

* Screen: 1136x640 pixels, LCD at 326 ppi.
* Apple A6 Dual-Core 1.3 GHz Apple-designed ARMv7s CPU
* Triple-Core PowerVR SGX543MP3 GPU
* 1GB LPDDR2 of memory
* Rear 8.0 MP infra-red cut-off filter, back-illuminated sensor, 1080p HD videos at 30 fps.
* Front 1.2 MP tagging, tap to focus, and 720p SD video at 30 fps
* GPS support
* Compass Support

###iPhone 5S

* Screen: 4" 1136x640 pixels, LCD at 326 ppi.
* Apple A7 Dual-Core 1.3 GHz Apple-designed ARMv8 64-bit CPU
* M7 Motion Coprocessor
* Four Cluster PowerVR G643 GPU
* 1GB LPDDR3 of memory
* Rear 8.0 MP infra-red cut-off filter, back-illuminated sensor, 1080p HD videos at 30 fps.
* Front 1.2 MP tagging, tap to focus, and 720p SD video at 30 fps
* GPS and GLONASS support
* Compass Support
* Three-axis gyro
* Proximity sensor
* Ambient light sensor
* Touch ID Fingerbringt identity sensor

###iPhone 6(+)

* Screen iPhone6: 4.7" 1134x750 pixels, LCD at 326 ppi.
* Screen iPhone6+: 5.5" 1920x1080 pixels, LCD at 401 ppi.
* Apple A8 Dual-Core 1.4 GHz Apple-designed ARMv8-A 64-bit CPU
* M8 motion coprocessor
* Quad-Core PowerVR GX6450 GPU
* 1GB LPDDR3 of memory
* Rear 8.0 MP infra-red cut-off filter, back-illuminated sensor, 1080p HD videos at 60 fps.
* Front 1.2 MP tagging, tap to focus, and 720p SD video at 30 fps
* GPS and GLONASS support
* Compass Support
* Three-axis gyro
* Proximity sensor
* Ambient light sensor
* Touch ID Fingerbringt identity sensor
* NFC


###[iPod Touch Models](http://en.wikipedia.org/wiki/IPod_Touch#Specifications)



###iPod Touch 3rd generation

* Screen: 320x480 pixels, LCD at 163ppi
* Samsung S5L8920, 833MHz (underclocked to 600MHz) ARM Cortex-A8 CPU
* PowerVR SGX535 graphics processor
* 256MB DRAM

![](../uploads/Main/csrRacing.jpg) 
iPod Touch 3rd gen: Shader-capable hardware, per-pixel-lighting (bumpmaps) can only be on small portions of the screen at once.
Requires scripting optimization for complex games. This is the average hardware of the app market as of July 2012

###iPod Touch 4th generation

* Screen: 960x640 pixels, LCD at 326 ppi, 800:1 contrast ratio.
* Apple A4 1 GHz (underclocked to 800MHz) ARM Cortex-A8 CPU
* PowerVR SGX535 GPU
* 256MB DRAM
* Rear 0.7 MP CMOS image sensor with 720p HD video at 30 fps and LED flash
* Front 0.3 MP (VGA) with geotagging, tap to focus, and 480p SD video at 30 fps

###iPod Touch 5th generation

* Screen: 1136x640 pixels, LCD at 326 ppi
* Apple A5 Dual-Core 1GHz (underclocked to 800MHz) ARM Cortex-A9 MPCore CPU
* Dual-Core PowerVR SGX543MP2 GPU
* 512MB of memory
* Rear 5.0 MP backside illuminated CMOS image sensor with 1080p HD video at 30 fps, face detection and video stabilization.
* Front 1.2 MP with geotagging, tap to focus, and 720p HD video at 30 fps


###[iPad Models](http://en.wikipedia.org/wiki/IPad#Technical_specifications)

###iPad

* Screen: 1024x768 pixels, LCD at 132 ppi, LED-backlit.
* Apple A4 1 GHz MHz ARM Cortex-A8 CPU
* PowerVR SGX535 GPU
* 256MB DDR Ram
* GPS support
* Accelerometer, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 2.1 + (3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.


![](../uploads/Main/airmail.jpg) 
iPad: Similar to iPod Touch 4th Generation and iPhone 4.



###iPad 2

* Screen: 1024x768 pixels, LCD at 132 ppi, LED-backlit.
* Apple A5 Dual-Core 1 GHz ARM Cortex-A9 MPCore CPU
* Dual-Core PowerVR SGX543MP2 GPU
* 512MB DDR2 Ram
* GPS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 2.1 + (3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.


![](../uploads/Main/deadtrigger.jpg) 
iPad2: The A5 can do full screen bumpmapping, assuming the shader is simple enough. However, it is likely that your game will perform best with bumpmapping only on crucial objects. Full screen image effects still out of reach. Scripting optimization less important.



###iPad (3rd generation)

* Screen: 2048x1536 pixels, LCD at 264 ppi, LED-backlit.
* Apple A5X
* Dual-Core 1 GHz ARM Cortex-A9 MPCore CPU
* Quad-Core PowerVR SGX543MP4 GPU
* 1GB LPDDR2 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.


![](../uploads/Main/bladeslinger.jpg) 
The iPad 3 has been shown to be capable of render-to-texture effects such as reflective water and fullscreen image effects. However, optimized shaders are still crucial. But if your game isn't trying to push limits of the device, optimizing scripting and gameplay is probably as much of a waste of time on this generation of devices as it is on PC.



###iPad (4th generation)

* Screen: 2048x1536 pixels, LCD at 264 ppi, LED-backlit.
* Apple A6X Dual-Core 1.4 GHz Apple Swift
* Quad-Core PowerVR SGX554MP4 GPU
* 1GB LPDDR2 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.


###iPad Air

* Screen: 2048x1536 pixels, LCD at 264 ppi, LED-backlit.
* Apple A7 Dual-Core 1.4 GHz Apple Cyclone
* Quad-Core PowerVR G6430 GPU
* M7 Motion Coprocessor
* 1GB LPDDR3 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.

###iPad Air 2

* Screen: 2048x1536 pixels, LCD at 264 ppi, LED-backlit.
* Apple A8X 1.5 GHz tripple-core
* Hex-Core PowerVR GX6650 GPU
* M8 Motion Coprocessor
* 2GB LPDDR3 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.
 

###iPad Mini 

* Screen: 1024x768 pixels, LCD at 163 ppi, LED-backlit.
* Apple A5 Dual-Core 1 GHz ARM Cortex-A9
* Dual-Core PowerVR SGX543MP2 GPU
* 512MB DDR2 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.

###iPad Mini 2

* Screen: 2048x1536 pixels, LCD at 326 ppi, LED-backlit.
* Apple A7 Dual-Core 1.3 GHz Apple Cyclone
* Quad-Core PowerVR G6430 GPU
* 1GB LPDDR3 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.

###iPad Mini 3

* Screen: 2048x1536 pixels, LCD at 326 ppi, LED-backlit.
* Apple A7 Dual-Core 1.3 GHz Apple Cyclone
* Quad-Core PowerVR G6430 GPU
* 1GB LPDDR3 Ram
* GPS and GLONASS support
* Accelerometer, Three-axis Gyro, Proximity Sensor, Ambient Light Sensor, Magnetometer
* Wifi + Blueooth 4.0 + (LTE, 3G Cellular HSDPA, 2G cellular EDGE on the 3G version)
* Mechanical keys: Home, sleep, function switch, volume.


Graphics Processing Unit and Hidden Surface Removal
---------------------------------------------------

The iPhone/iPad graphics processing unit (GPU) is a Tile-Based Deferred Renderer. In contrast with most GPUs in desktop computers, the iPhone/iPad GPU focuses on minimizing the work required to render an image as early as possible in the processing of a scene. That way, only the visible pixels will consume processing resources.

The GPU's frame buffer is divided up into tiles and rendering happens tile by tile. First, triangles for the whole frame are gathered and assigned to the tiles. Then, visible fragments of each triangle are chosen. Finally, the selected triangle fragments are passed to the rasterizer (triangle fragments occluded from the camera are rejected at this stage).

In other words, the iPhone/iPad GPU implements a __Hidden Surface Removal__ operation at reduced cost. Such an architecture consumes less memory bandwidth, has lower power consumption and utilizes the texture cache better. Tile-Based Deferred Rendering allows the device to reject occluded fragments before actual rasterization, which helps to keep overdraw low.

For more information see also:-

* [Apple Notes on iPhone/iPad GPU and OpenGL ES](https://developer.apple.com/library/ios/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Introduction/Introduction.html)
* [Apple Performance Advices for OpenGL ES in General](http://developer.apple.com/library/ios/#documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Performance/Performance.html)
* [Apple Performance Advices for OpenGL ES Shaders](http://developer.apple.com/library/ios/#documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/BestPracticesforShaders/BestPracticesforShaders.html)


###SGX series

Starting with the iPhone 3GS, newer devices are equipped with the __SGX__ series of GPUs. The SGX series features support for the __OpenGL ES2.0__ and newer devices support the __OpenGL ES3.0__ rendering API and vertex and pixel shaders. The Fixed-function pipeline is not supported natively on such GPUs, but instead is emulated by generating vertex and pixel shaders with analogous functionality on the fly.

The SGX series fully supports MultiSample anti-aliasing.


###Texture Compression

The only texture compression format supported by iOS is __PVRTC__. PVRTC provides support for RGB and RGBA (color information plus an alpha channel) texture formats and can compress a single pixel to two or four bits.

The PVRTC format is essential to reduce the memory footprint and to reduce consumption of memory bandwidth (ie, the rate at which data can be read from memory, which is usually very limited on mobile devices).


###Vertex Processing Unit
The iPhone/iPad has a dedicated unit responsible for vertex processing which runs calculations in parallel with rasterization. In order to achieve better parallelization, the iPhone/iPad processes vertices one frame ahead of the rasterizer.


Unified Memory Architecture
---------------------------

Both the CPU and GPU on the iPhone/iPad share the same memory. The advantage is that you don't need to worry about running out of video memory for your textures (unless, of course, you run out of main memory too). The disadvantage is that you share the same memory bandwidth for gameplay and graphics. The more memory bandwidth you dedicate to graphics, the less you will have for gameplay and physics.


Multimedia CoProcessing Unit
----------------------------

The iPhone/iPad main CPU is equipped with a powerful SIMD (Single Instruction, Multiple Data) coprocessor supporting either the __VFP__ or the __NEON__ architecture. The Unity iOS run-time takes advantage of these units for multiple tasks such as calculating skinned mesh transformations, geometry batching, audio processing and other calculation-intensive operations.
