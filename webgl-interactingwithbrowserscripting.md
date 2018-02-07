# WebGL: Interacting with browser scripting

When building content for the web, you might need to communicate with other elements on your web page. Or you might want to implement functionality using Web APIs which Unity does not currently expose by default. In both cases, you need to directly interface with the browser’s JavaScript engine. Unity WebGL provides different methods to do this.

## Calling JavaScript functions from Unity scripts

The recommended way of using browser JavaScript in your project is to add your JavaScript sources to your project, and then call those functions directly from your script code. To do so, place files with JavaScript code using the .jslib extension (as the normal .js would be picked up by the UnityScript compiler) under a "Plugins" subfolder in your Assets folder. The plugin file needs to have a syntax like this:

```
mergeInto(LibraryManager.library, {

  Hello: function () {
	window.alert("Hello, world!");
  },

  HelloString: function (str) {
	window.alert(Pointer_stringify(str));
  },

  PrintFloatArray: function (array, size) {
	for(var i = 0; i < size; i++)
  	console.log(HEAPF32[(array >> 2) + i]);
  },

  AddNumbers: function (x, y) {
	return x + y;
  },

  StringReturnValueFunction: function () {
    var returnStr = "bla";
    var bufferSize = lengthBytesUTF8(returnStr) + 1;
    var buffer = _malloc(bufferSize);
    stringToUTF8(returnStr, buffer, bufferSize);
    return buffer;
  },

  BindWebGLTexture: function (texture) {
	GLctx.bindTexture(GLctx.TEXTURE_2D, GL.textures[texture]);
  },

});
```

Then you can call these functions from your C# scripts like this:

```
using UnityEngine;
using System.Runtime.InteropServices;

public class NewBehaviourScript : MonoBehaviour {

    [DllImport("__Internal")]
    private static extern void Hello();

    [DllImport("__Internal")]
    private static extern void HelloString(string str);

    [DllImport("__Internal")]
    private static extern void PrintFloatArray(float[] array, int size);

    [DllImport("__Internal")]
    private static extern int AddNumbers(int x, int y);

    [DllImport("__Internal")]
    private static extern string StringReturnValueFunction();

    [DllImport("__Internal")]
    private static extern void BindWebGLTexture(int texture);

    void Start() {
        Hello();
        
        HelloString("This is a string.");
        
        float[] myArray = new float[10];
        PrintFloatArray(myArray, myArray.Length);
        
        int result = AddNumbers(5, 7);
        Debug.Log(result);
        
        Debug.Log(StringReturnValueFunction());
        
        var texture = new Texture2D(0, 0, TextureFormat.ARGB32, false);
        BindWebGLTexture(texture.GetNativeTextureID());
    }
}
```

Simple numeric types can be passed to JavaScript in function parameters without requiring any conversion. Other data types will be passed as a pointer in the emscripten heap (which is really just a big array in JavaScript). For strings, you can use the `Pointer_stringify` helper function to convert to a JavaScript string. To return a string value you need to call `_malloc_` to allocate some memory and the  `stringToUTF8` helper function to write a JavaScript string to it. If the string is a return value, then the il2cpp runtime will take care of freeing the memory for you. For arrays of primitive types, `emscripten` provides different `ArrayBufferViews` into it’s heap for different sizes of integer, unsigned integer or floating point representations of memory: __HEAP8, HEAPU8, HEAP16, HEAPU16, HEAP32, HEAPU32, HEAPF32, HEAPF64__. To access a texture in WebGL, emscripten provides the `GL.textures` array which maps native texture IDs from Unity to WebGL texture objects. WebGL functions can be called on emscripten’s WebGL context, `GLctx`.

### Legacy ways of calling JavaScript code from Unity

*Note: Starting from Unity 5.6 the recommended way of calling JavaScript code from Unity is through a .jslib plugin. The method described below is only supported for compatibility reasons and might become deprecated in the future versions of Unity.*

You can use the [Application.ExternalCall()](ScriptRef:Application.ExternalCall.html) and [Application.ExternalEval()](ScriptRef:Application.ExternalEval.html) functions to invoke JavaScript code on the embedding web page. Note that expressions are evaluated in the local scope of the build. If you would like to execute JavaScript code in the global scope, see the *Code Visibility* section below.

## Calling Unity scripts functions from JavaScript

Sometimes you need to send some data or notification to the Unity script from the browser’s JavaScript. The recommended way of doing it is to call methods on GameObjects in your content. If you are making the call from a JavaScript plugin, embedded in your project, you can use the following code:

  `SendMessage(objectName, methodName, value);`

Where __objectName __is the name of an object in your scene; __methodName __is the name of a method in the script, currently attached to that object; __value __can be a string, a number, or can be empty. For example:

```
SendMessage('MyGameObject', 'MyFunction');
SendMessage('MyGameObject', 'MyFunction', 5);

SendMessage('MyGameObject', 'MyFunction', 'MyString');
```

If you would like to make a call from the global scope of the embedding page, see the *Code Visibility* section below.

## Calling C++ functions from Unity scripts

Since Unity compiles your sources into JavaScript from C++ code using emscripten, you can also write plugins in C or C++ code, and call these functions from C#. So, instead of the jslib file in the example above, you could have a c file like below in your project - it will automatically get compiled with your scripts, and you can call functions from it, just like in the JavaScript example above.

If you are using C++ (.cpp) to implement the plugin then you must ensure the functions are declared with C linkage to avoid name mangling issues.

```
#include <stdio.h>
void Hello ()
{
    printf("Hello, world!\n");
}
int AddNumbers (int x, int y)
{
    return x + y;
}
```

### Code visibility

Starting from Unity 5.6 all the build code is executed in its own scope. This approach makes it possible to embed your game on an arbitrary page without causing conflicts with the embedding page code, as well as makes it possible to embed more than one build on the same page.

If you have all your JavaScript code in the form of *.jslib* plugins inside your project, then this JavaScript code will run inside the same scope as the compiled build and your code should work pretty much the same way as in previous versions of Unity (for example, the following objects and functions should be directly visible from the JavaScript plugin code: *Module, SendMessage, HEAP8, ccall etc.*).

However, if you are planning to call the internal JavaScript functions from the global scope of the embedding page, you should always assume that there are multiple builds embedded on the page, so you should explicitly specify which build you are referencing to. For example, if your game has been instantiated as:

`var gameInstance = UnityLoader.instantiate("gameContainer", "Build/build.json", {onProgress: UnityProgress});`

Then you can send a message to the build using *gameInstance.SendMessage()*, or access the build Module object like this *gameInstance.Module*.

---

* <span class="page-edit">2017-11-14  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Fixed error in code example.</span>

* <span class="page-history">Updated in 5.6</span>

