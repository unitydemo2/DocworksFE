#WebGL Browser Compatibility

Unity WebGL supports all major desktop browsers to some degree. However, the level of support and the expected performance varies between different browsers. See the table below for an overview of browser features of interest to Unity WebGL content, and which browsers support them.

Note that Unity WebGL content is not currently supported on mobile devices. It may still work, especially on high-end devices, but many current devices are not powerful enough and don't have enough memory to support Unity WebGL content well. For this reason, Unity WebGL shows a warning message when trying to load content on mobile browsers (which can be disabled if needed).

Note that this compatibility table is valid for the specific versions of the browsers as stated. Support should continue for future versions, but may not be stable in previous versions.

|**Desktop browser compatibility table** |||||||
|:---|:---|:---|:---|:---|:---|:---|
||**Mozilla Firefox 52**|**Google Chrome 57**|**Apple Safari 11**|**MS Edge 16**||
|**WebGL Support**|**Yes** <br/> GPU blacklists apply. WebGL may be unsupported for specific older graphics cards. Details available on the [Mozilla wiki page on Blocklisting/Blocked Graphics Drivers](https://wiki.mozilla.org/Blocklisting/Blocked_Graphics_Drivers) and the [Khronos wiki page on Blacklists and Whitelists](https://www.khronos.org/webgl/wiki/BlacklistsAndWhitelists).|**Yes** <br/> GPU blacklists apply. WebGL may be unsupported for specific older graphics cards. Details available on the [Mozilla wiki page on Blocklisting/Blocked Graphics Drivers](https://wiki.mozilla.org/Blocklisting/Blocked_Graphics_Drivers) and the [Khronos wiki page on Blacklists and Whitelists](https://www.khronos.org/webgl/wiki/BlacklistsAndWhitelists).|**Yes** <br/> Safari 8 and higher|**Yes**|
|**Web Audio** <br/>(See [Web Audio](webgl-audio)) <br/>The Web Audio API is required to play sound in Unity WebGL content.|**Yes**|**Yes**|**Yes**|**Yes**|
|**Full-screen support** <br/>(See [Full-screen support](webgl-cursorfullscreen))|**Yes**|**Yes**|**Yes**<br/>Safari 10.1 or newer|**Yes**|
|**Cursor locking support** <br/>(see [Cursor Locking support](webgl-cursorfullscreen))|**Yes**|**Yes**|**Yes**|**Yes** <br/> Edge 13 and newer.|
|**Gamepad support** <br/>(See [Gamepad support](webgl-input))|**Yes**|**Yes**|**Yes**|**Yes**|
|**IndexedDB** <br/>Required for local storage as used by the Data Caching feature, the [PlayerPrefs](ScriptRef:PlayerPrefs.html) class, and [WWW.LoadFromCacheOrDownload](ScriptRef:WWW.LoadFromCacheOrDownload.html).|**Yes** <br/> Firefox up to version 42 does not support IndexedDB for content running in an iFrame. Firefox 43 and higher fixes this.|**Yes**|**Yes** <br/> Safari does not support IndexedDB for content running in an iFrame.|**Yes**|
|**WebSockets** <br/>Required for [Networking](UNet). |**Yes**|**Yes**|**Yes**|**Yes**|
|**WebRTC** <br/>Required by the [WebCamTexture](ScriptRef:WebCamTexture.html) class.|**Yes**|**Yes**|**No**|**Yes**|
|**WebGL 2.0** <br/>(See [WebGL 2.0](webgl-graphics))|**Yes** <br/> Firefox 51 and newer|**Yes** <br/> Chrome 56 and newer|**No**|**No**|
|**asm.js AOT compilation** <br/>asm.js is a susbset of JavaScript for which a browser can specifically optimize. Browsers which implement asm.js support may be able to run Unity WebGL content faster, because Unity uses asm.js.|**Yes**|**No**|**No**|**Yes**|
|**WebAssembly** <br/>WebAssembly or wasm is a new portable, size-efficient and load-time-efficient format suitable for compilation to the web.|**Yes** <br/> Firefox 52 and newer.|**Yes** <br/> Chrome 57 and newer.|**Yes**<br/>Safari 11 or newer|**Yes**<br/>Edge 16 or newer|
|**Large-Allocation Http header** <br/>Helps browsers make sure enough memory is available to load your content (See [Large-Allocation Http Header](webgl-memory))|**Yes** <br/> Firefox 53 and newer.|**No**|**No**|**No**|
|**Brotli Compression** <br/>Reduces build size (See [Brotli compression](webgl-deploying))|**Yes**|**Yes**|**No**|**Yes**|
##Notes

* Chrome may need a large amount of memory to parse the generated JavaScript code, which can cause out-of-memory errors or crashes when loading content on 32-bit browsers. See [Memory Considerations](webgl-memory) for more information on memory usage.

<br/><br/>

-----

*  <span class="page-edit">2017-05-15  <!-- include IncludeTextAmendPageNoEdit --></span>

*  <span class="page-history">Brotli compression first documented on this page in User Manual 5.6</span>
