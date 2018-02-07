#Unity Google VR Video Async Reprojection

<!-- XR overhaul - https://trello.com/c/Qw7imxOL -->

##What is Video Async Reprojection?

Async Reprojection Video is a layer (referred to as an __external surface__) that an application can use to feed video frames directly into the async reprojection system. The main advantages to using the API are:

1. Without the API, the video is sampled once to render it into the app's color buffer, then the color buffer is sampled again to perform distortion correction. This introduces double sampling artifacts. The external surface passes video directly to the EDS compositor, so it's only sampled once, thus improving visual quality of the video.

2. When using the external surface API, video frame rate is decoupled from the app frame rate. The application can take 1 second to render a new frame and the only result is that the user will see black bars when they move their head, the video will keep playing normally. This should significantly reduce dropped video frames, and maintain AV sync

3. The application can mark that it wants to playback DRM video, and the API will create a protected path that shows protected video and maintains Async Reprojection frame rate.

##Known issues:

1. When using Video Async Reprojection, the camera must start at the origin (0,0,0). Errors may occur if the camera’s position is not set to 0,0,0.

2. There is no publicly accessible C# interface for Async Reprojection. The public API is Java only.

##Enabling Async Video Reprojection

Async Video Reprojection is a part of the Daydream VR Device settings. 

![Adding Daydream to the Virtual Reality SDKs list settings](../uploads/Main/GoogleVRVideoAsyncReprojection0.png)

Click the grey arrow next to Daydream and then check the __Enable Video Surface__ box to enable use of the Async Video Reprojection feature

![Virtual Reality SDKs List Daydream settings](../uploads/Main/GoogleVRVideoAsyncReprojection1.png)

Select the __Use Protected Memory__ option only if you require memory protection for all of your content as enabling this means that it is enabled for the lifetime of the application.

![Enable Video Surface checkbox to enable Async Video Reprojection](../uploads/Main/GoogleVRVideoAsyncReprojection2.png)

##API documentation

To take advantage of the Google VR API you will need to extend the UnityPlayerActivity. For more information, see documentation on [Extending the UnityPlayerActivity](AndroidUnityPlayerActivity).

Java plug-ins cannot directly access Objects in your scene, so you will need to provide a simple API to your C# code that will allow you to pass a transform to the Java side and tell your Java code when to start rendering.

__Note:__ This code is not complete. It contains no implementation of a video player as that is a client specific implementation detail. It also doesn’t have any playback controls, which would have to be implemented as objects in the scene and actions on those objects would need to call into Java.

For information on using Java in Unity and extending the UnityPlayerActivity, see documentation on [Android development in Unity](android).

For information about the Google Video Async Reprojection system, refer to the Android Developer Network documentation on [Video Viewports](https://developers.google.com/vr/reference/android-ndk/gvr-ndk-rendering#using_video_viewports).

###Java sample code:

```
package com.unity3d.samplevideoplayer;

import com.unity3d.player.GoogleVrVideo;

import com.unity3d.player.GoogleVrApi;

import android.app.Activity;

import android.os.Bundle;

import android.util.Log;

import android.view.Surface;

public class GoogleAVRPlayer implements GoogleVrVideo.GoogleVrVideoCallbacks {

	private static final String TAG = GoogleAVRPlayer.class.getSimpleName();

	private MyOwnVideoPlayer videoPlayer;

	private boolean canPlayVideo = false;

	private boolean isSceneLoaded = false;

	// API you present to your C# code to handle initialization of your

	// video system.

	public void initVideoPlayer(UnityPlayerActivity activity) {

	 // Initialize Video player and any other support you need…

	 // Register this instance as the Google Vr Video Listener to get

	 // lifetime and control callbacks.

    	 GoogleVrVideo gvrv = GoogleVrApi.getGoogleVrVideo();

    	 if (gvrv != null) gvrv.registerGoogleVrVideoListener(this); 

	}

 

	// API you present to your C# code to start your video system

	// playing a video.

	public void play()

	{

    	   if (canPlayVideo && videoPlayer != null && videoPlayer.isPaused())

        	videoPlayer.play();

	}

	// API you present to your C# code to stop your video system

	// playing a video

	public void pause()

	{

    	    if (canPlayVideo && videoPlayer != null && !videoPlayer.isPaused())

        	videoPlayer.pause();    	

	}

	// Google Vr Video Listener

	@Override

	public void onSurfaceAvailable(Surface surface) {

	 // Google Vr has a surface available for you to render into.

	 // Use this surface with your video player as needed.

    	 if (videoPlayer != null){

        	videoPlayer.setSurface(surface);

        	canPlayVideo = true;

        	if (isSceneLoaded)

        	{

            	videoPlayer.play();

        	}

    	  }

	}

	@Override

	public void onSurfaceUnavailable() {

	 // The Google Vr Video Surface is going away. You need to remove

	 // it from anything you have holding it and stop your video player.

        if (videoPlayer != null){

        	videoPlayer.pause();

        	canPlayVideo = false;

    	  }

	 }

	@Override

	public void onFrameAvailable() {

	 // Handle Google Vr frame available callback

	}
}

```
###Unity C# sample code:

```
using System;

using System.Collections;

using System.Collections.Generic;

using System.Text;

using UnityEngine;

public class GoogleVRVideo : MonoBehaviour {

 private AndroidJavaObject googleAvrPlayer = null;

 private AndroidJavaObject googleVrVideo = null;

 void Awake()

 {

    if (googleAvrPlayer == null)

    {

      googleAvrPlayer = new AndroidJavaObject("com.unity3d.samplevideoplayer.GoogleAVRPlayer");

    }

    AndroidJavaObject googleVrApi = new AndroidJavaClass("com.unity3d.player.GoogleVrApi");

    if (googleVrApi != null) googleVrVideo = googleVrApi.CallStatic<AndroidJavaObject>("getGoogleVrVideo");

 }

 void Start()

 {

  if (googleVrVideo != null)

  {

   // We need to tell Google VR the location of the video suface in

   // world space. Since there isn't a way to get at that info from

   // Java, we can do it here and then pass the calculated matrix

   // down to the api we expose on our UnityPlayerActivity subclass.

   Matrix4x4 wm = transform.localToWorldMatrix;
   
   wm = Camera.main.transform.parent.worldToLocalMatrix * wm;
   
   wm = wm * Matrix4x4.Scale(new Vector3(0.5f, 0.5f, 1));


   // Convert 4x4 Row Ordered matrix into a 16 element column ordered

   // flat array. The transposition is to make sure that the matrix is

   // in the order that Google uses and the we flatten it to make passing

   // over the JNI boundary easier. The complication being that you have to

   // then convert it back to an 4x4 matrix on the Java side.

   float[] matrix = new float[16];

   for (int i = 0; i < 4; i++)

   {

    for (int j = 0; j < 4; j++)

    {

     matrix[i * 4 + j] = wm[j,i];

    }

   }

   googleVrVideo.Call("setVideoLocationTransform", matrix);  

  }

  

  if (googleAvrPlayer != null)

  {

    AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer");

    AndroidJavaObject jo = jc.GetStatic<AndroidJavaObject>("currentActivity");

    googleAvrPlayer.Call("initVideoPlayer", jo);

    googleAvrPlayer.Call("play");

  }

 }

}

```
---

* <span class="page-edit">2017-08-03  <!-- include IncludeTextNewPageSomeEdit --></span>
* <span class="page-history">Added in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>
