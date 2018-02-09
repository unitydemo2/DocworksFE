#Photo capture
Use the  [PhotoCapture](ScriptRef:VR.WSA.WebCam.PhotoCapture.html) API to take photos from the HoloLens web camera. You must enable the __WebCam__ and __Microphone__ capabilities to use the PhotoCapture API. The following example demonstrates how to take a photo using the PhotoCapture functionality and display it on a Unity [GameObject](ScriptRef:GameObject.html).

````
using UnityEngine;
using System.Collections;
using System.Linq;
using UnityEngine.VR.WSA.WebCam;

public class PhotoCaptureExample : MonoBehaviour {
    PhotoCapture photoCaptureObject = null;
    Texture2D targetTexture = null;

    // Use this for initialization
    void Start() {
        Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();
        targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

        // Create a PhotoCapture object
        PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject) {
            photoCaptureObject = captureObject;
            CameraParameters cameraParameters = new CameraParameters();
            cameraParameters.hologramOpacity = 0.0f;
            cameraParameters.cameraResolutionWidth = cameraResolution.width;
            cameraParameters.cameraResolutionHeight = cameraResolution.height;
            cameraParameters.pixelFormat = CapturePixelFormat.BGRA32;

            // Activate the camera
            photoCaptureObject.StartPhotoModeAsync(cameraParameters, delegate (PhotoCapture.PhotoCaptureResult result) {
                // Take a picture
                photoCaptureObject.TakePhotoAsync(OnCapturedPhotoToMemory);
            });
        });
    }

    void OnCapturedPhotoToMemory(PhotoCapture.PhotoCaptureResult result, PhotoCaptureFrame photoCaptureFrame) {
        // Copy the raw image data into the target texture
        photoCaptureFrame.UploadImageDataToTexture(targetTexture);

        // Create a GameObject to which the texture can be applied
        GameObject quad = GameObject.CreatePrimitive(PrimitiveType.Quad);
        Renderer quadRenderer = quad.GetComponent<Renderer>() as Renderer;
        quadRenderer.material = new Material(Shader.Find("Custom/Unlit/UnlitTexture"));

        quad.transform.parent = this.transform;
        quad.transform.localPosition = new Vector3(0.0f, 0.0f, 3.0f);

        quadRenderer.material.SetTexture("_MainTex", targetTexture);

        // Deactivate the camera
        photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
    }

    void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result) {
        // Shutdown the photo capture resource
        photoCaptureObject.Dispose();
        photoCaptureObject = null;
    }
}
````
##Capture a photo to memory

When you capture an image to memory, a [PhotoCaptureFrame](ScriptRef:VR.WSA.WebCam.PhotoCaptureFrame.html) is returned. A `PhotoCaptureFrame` contains both the native image data and spatial matrices that indicate where the image was taken.

Capturing an image to memory allows you to reference the captured image in a Shader, or apply it to a GameObject. There are three ways to extract the image data from the `PhotoCaptureFrame`. These are:

1. Access the image data as a [Texture2D](ScriptRef:Texture2d.html). This is the most common way to extract image data, because most components in Unity understand how to access image data in a Texture2D. Once your image has been captured to memory, you need to upload the image data into a Texture2D. Once the image data is uploaded into a Texture2D, you can then begin referencing that image data in materials, scripts, or any other relevant element of your project. The Unity API Documentation has an example which demonstrates how to capture a photo to memory and then upload it to a Texture2D. See
[WebCam.PhotoCapture.TakePhotoAsync](ScriptRef:VR.WSA.WebCam.PhotoCapture.TakePhotoAsync.html) to learn how to capture a photo to a Texture2D. Uploading the image data to a Texture2D via the upload command is the easiest way to start working with your image data in Unity. The upload operation happens on the main thread. This operation is resource-intensive and can affect the performance of your project.

2. Capture the native image data as a __WinRT IMFMediaBuffer__. See Microsoft's documentation on [IMFMediaBuffer](https://msdn.microsoft.com/en-us/library/windows/desktop/ms696261(v=vs.85).aspx) to learn more. Make a copy of the native image data by passing a byte list into the 
[PhotoFrame.CopyRawImageDataIntoBuffer](ScriptRef:VR.WSA.WebCam.PhotoCaptureFrame.CopyRawImageDataIntoBuffer.html) function. Please note that the copy operation occurs on the main thread. This operation is resource-intensive and can affect the performance of your project.

3. If you create your own plugin, or process the image data on a separate thread, you can get a pointer to the native image data via the [PhotoFrame.GetUnsafePointerToBuffer](ScriptRef:VR.WSA.WebCam.PhotoCaptureFrame.GetUnsafePointerToBuffer.html) function. The pointer returned is a pointer to an IMFMediaBuffer Component Object Model (COM). See Microsoft’s documentation on [IMFMediaBuffer](https://msdn.microsoft.com/en-us/library/windows/desktop/ms696261(v=vs.85).aspx) and [Component Object Models](https://msdn.microsoft.com/en-us/library/windows/desktop/ms694363(v=vs.85).aspx) for more information. Once you call this function, a reference is added to the COM object. You are responsible for releasing the reference when you no longer need the resource.
