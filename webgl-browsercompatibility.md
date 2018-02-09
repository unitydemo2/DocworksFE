#WebGL Browser Compatibility

Unity WebGL supports all major desktop browsers to some degree. However, the level of support and the expected performance varies between different browsers. See the table below for an overview of browser features of interest to Unity WebGL content, and which browsers support them.

Note that Unity WebGL content is not currently supported on mobile devices. It may still work, especially on high-end devices, but many current devices are not powerful enough and don't have enough memory to support Unity WebGL content well. For this reason, Unity WebGL shows a warning message when trying to load content on mobile browsers (which can be disabled if needed).

Note that this compatibility table is valid for the specific versions of the browsers as stated. Support should continue for future versions, but may not be stable in previous versions.

|**Desktop browser compatibility table** |||||||
|:---|:---|:---|:---|:---|:---|:---|
||**Mozilla Firefox 51**|**Google Chrome 56**|**Apple Safari 10.1**|**MS Internet Explorer 11**|**MS Edge 14**||
|**WebGL Support**|**Yes** <br/> GPU blacklists apply. WebGL may be unsupported for specific older graphics cards. Details available on the [Mozilla wiki page on Blocklisting/Blocked Graphics Drivers](https://wiki.mozilla.org/Blocklisting/Blocked_Graphics_Drivers) and the [Khronos wiki page on Blacklists and Whitelists](https://www.khronos.org/webgl/wiki/BlacklistsAndWhitelists).|**Yes** <br/> GPU blacklists apply. WebGL may be unsupported for specific older graphics cards. Details available on the [Mozilla wiki page on Blocklisting/Blocked Graphics Drivers](https://wiki.mozilla.org/Blocklisting/Blocked_Graphics_Drivers) and the [Khronos wiki page on Blacklists and Whitelists](https://www.khronos.org/webgl/wiki/BlacklistsAndWhitelists).|**Yes** <br/> Safari 8 and higher|**Yes** <br/> IE 11 and higher|**Yes**|
|**Web Audio** <br/>(See [Web Audio](webgl-audio)) <br/>The Web Audio API is required to play sound in Unity WebGL content.|**Yes**|**Yes**|**Yes**|**No**|**Yes**|
|**Full-screen support** <br/>(See [Full-screen support](webgl-cursorfullscreen))|**Yes**|**Yes**|**Yes**|**Yes**|**Yes**|
|**Cursor locking support** <br/>(see [Cursor Locking support](webgl-cursorfullscreen))|**Yes**|**Yes**|**Yes**|**No**|**Yes** <br/> Edge 13 and newer.|
|**Gamepad support** <br/>(See [Gamepad support](webgl-input))|**Yes**|**Yes**|**Yes**|**No**|**Yes**|
|**IndexedDB** <br/>Required for local storage as used by the Data Caching feature, the [PlayerPrefs](ScriptRef:PlayerPrefs.html) class, and [WWW.LoadFromCacheOrDownload](ScriptRef:WWW.LoadFromCacheOrDownload.html).|**Yes** <br/> Firefox up to version 42 and Safari will not support IndexedDB for content running in an iFrame. Firefox 43 and higher will fix this.|**Yes**|**Yes** <br/> Firefox up to version 42 and Safari will not support IndexedDB for content running in an iFrame. Firefox 43 and higher will fix this.|**Yes**|**Yes**|
|**WebSockets** <br/>Required for [Networking](UNet). |**Yes**|**Yes**|**Yes**|**Yes**|**Yes**|
|**WebRTC** <br/>Required by the [WebCamTexture](ScriptRef:WebCamTexture.html) class.|**Yes**|**Yes**|**No**|**No**|**Yes**|
|**WebGL 2.0** <br/>(See [WebGL 2.0](webgl-graphics))|**Yes** <br/> Firefox 51 and newer|**Yes** <br/> Chrome 56 and newer|**No**|**No**|**No**|
|**asm.js AOT compilation** <br/>asm.js is a susbset of JavaScript for which a browser can specifically optimize. Browsers which implement asm.js support may be able to run Unity WebGL content faster, because Unity uses asm.js.|**Yes**|**No**|**No**|**No**|**Yes**|

|**Large-Allocation Http header** <br/>Helps browsers make sure enough memory is available to load your content (See [Large-Allocation Http Header](webgl-memory))|**Yes** <br/> Firefox 53 and newer.|**No**|**No**|**No**|
##Notes

* Chrome may need a large amount of memory to parse the generated JavaScript code, which can cause out-of-memory errors or crashes when loading content on 32-bit browsers. See [Memory Considerations](webgl-memory) for more information on memory usage.
* Internet Explorer does not support audio and is too slow to support most Unity WebGL content with decent results. For this reason, we will show a warning about using an unsupported browser when opening content in Internet Explorer. It is only listed in this compatibility table for completeness. You should advise IE users to update to Microsoft's new Edge browser.

