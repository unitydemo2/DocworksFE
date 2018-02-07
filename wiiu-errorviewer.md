Using ErrorViewer
==================

In many cases ErrorViewer will work automatically. You can also present it manually by creating a `WiiU.ErrorViewerArg` object, setting mandatory properties and passing it to `WiiU.ErrorViewer.Invoke`. Here's a example:


````
using WiiU = UnityEngine.WiiU;

private float time = 0.0f;

void Update()
{
    time += Time.deltaTime;
      
    if (time > 5.0f)
    {
        time -= 5.0f;
        WiiU.ErrorViewerArg arg = new WiiU.ErrorViewerArg();
        arg.screenType = WiiU.ErrorViewerArg.ScreenType.Tv;
        // You must set the valid errorCode value if errorType is ErrorType.Code.
        arg.errorType = WiiU.ErrorViewerArg.ErrorType.Code;
        arg.errorCode = 1010102;
        arg.mainText = "Your Error Message\n";
        
        switch( WiiU.ErrorViewer.Invoke(arg) )
        {
            case WiiU.ErrorViewer.InvokeResult.NONE:
                Debug.Log("WiiU.ErrorViewer.InvokeResult.NONE");
                break;
            case WiiU.ErrorViewer.InvokeResult.Button:
                Debug.Log("WiiU.ErrorViewer.InvokeResult.Button");
                break;
            case WiiU.ErrorViewer.InvokeResult.LeftButton:
                Debug.Log("WiiU.ErrorViewer.InvokeResult.LeftButton");
                break;
            case WiiU.ErrorViewer.InvokeResult.RightButton:
                Debug.Log("WiiU.ErrorViewer.InvokeResult.RightButton");
                break;
        }
    }
}
````

`WiiU.ErrorViewer.Invoke` is a blocking call and calling it will block main loop. The runtime will continue only when the call returns. Also, invoking ErrorViewer will pause Unity and callback `MonoBehaviour.OnApplicationPause(bool)` will be called.

All error codes can be found: "cafe_sdk/system/docs/man/en_us/nn/erreula/ErrorCodeList/".
