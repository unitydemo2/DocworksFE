WebGL: Interacting with browser scripting
=========================================

When building content for the web, you might need to communicate with other elements on your web page. Or you might want to implement functionality using Web APIs which Unity does not currently expose by default. In both cases, you need to directly interface with the browser's JavaScript engine. Unity WebGL provides different methods to do this.

Calling between JavaScript code from Unity
------------------------------------------

You can use the __[Application.ExternalCall()](ScriptRef:Application.ExternalCall.html)__  and __[Application.ExternalEval()](ScriptRef:Application.ExternalEval.html)__  functions to invoke JavaScript code on the embedding web page. To call methods on GameObjects in your content from browser JavaScript, you can use the following code:

```
sendMessage ('MyGameObject', 'MyFunction', 'example');
```

Calling JavaScript functions from a plugin
------------------------------------------

The other way to use browser JavaScript in your project is to add your JavaScript sources to your project, and then call those functions directly from your script code. To do so, place files with JavaScript code using the .jslib extension (as the normal .js would be picked up by the UnityScript compiler) into a "Plugins/WebGL" folder in your Assets folder. The file needs to have a syntax like this:

Assets/Plugins/WebGL/MyPlugin.jslib

```
var MyPlugin = {
	Hello: function()
	{
		window.alert("Hello, world!");
	},
	HelloString: function(str)
	{
		window.alert(Pointer_stringify(str));
	},
	PrintFloatArray: function(array, size)
	{
		for(var i=0;i<size;i++)
			console.log(HEAPF32[(array>>2)+size]);
	},
	AddNumbers: function(x,y)
	{
		return x + y;
	},
	StringReturnValueFunction: function()
	{
		var returnStr = "bla";
		var buffer = _malloc(lengthBytesUTF8(returnStr) + 1);
		writeStringToMemory(returnStr, buffer);
		return buffer;
	},
	BindWebGLTexture: function(texture)
	{
		GLctx.bindTexture(GLctx.TEXTURE_2D, GL.textures[texture]);
	}
};

mergeInto(LibraryManager.library, MyPlugin);
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

Simple numeric types can be passed to JavaScript in function parameters without requiring any conversion. Other data types will be passed as a pointer in the emscripten heap (which is really just a big array in JavaScript). For strings, you can use the __Pointer_stringify__ helper function to convert to a JavaScript string. To return a string value you need to call ___malloc__ to allocate some memory and the __writeStringToMemory__ helper function to write a JavaScript string to it. If the string is a return value, then the il2cpp runtime will take care of freeing the memory for you. For arrays of primitive types, emscripten provides different ArrayBufferViews into it's heap for different sizes of integer, unsigned integer or floating point representations of memory: __HEAP8, HEAPU8, HEAP16, HEAPU16, HEAP32, HEAPU32, HEAPF32, HEAPF64__. To access a texture in WebGL, emscripten provides the __GL.textures__ array which maps native texture IDs from Unity to WebGL texture objects. WebGL functions can be called on emscripten's WebGL context, __GLctx__.


Calling C++ functions from a plugin
-----------------------------------

Since Unity compiles your sources into JavaScript from C++ code using emscripten, you can also write plugins in C or C++ code, and call these functions from C#. So, instead of the jslib file in the example above, you could have a c file like below in your project - it will automatically get compiled with your scripts, and you can call functions from it, just like in the JavaScript example above.

If you are using C++ (.cpp) to implement the plugin then you must ensure the functions are declared with C linkage to avoid name mangling issues.

Assets/Plugins/WebGL/MyPlugin.c

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


Customizing Compatibility Checks or Error handlers
--------------------------------------------------

Unity will write some JavaScript code to builds by default, which will check platform compatibility and handles errors. This code will display warning messages when running on unsupported platforms, like when trying to run Unity WebGL content on mobile devices. It will also parse error and exception strings from the browser, to check for known errors and display error dialogs with more comprehensive error messages.

You can customize this handling, for instance, if you want to suppress the warning messages when running on mobile devices. To do so, open the generated index.html, and replace this code with actual JavaScript function implementations for errorhandler and/or compatibilitycheck:

```
  var Module = {
    TOTAL_MEMORY: 268435456,
    errorhandler: null,
    compatibilitycheck: null,
  };
```

The compatibilitycheck function will just be called at startup, and you can put any code in here to show messages when you detect that the content is not supported.

The errorhandler function will be called when the page invokes its window.onerror event handler, and uses the same parameters. Return "true" from this function to resume execution, and "false" to pass the error to Unity's default error handler.

Example:

```
  var Module = {
    TOTAL_MEMORY: 268435456,
    errorhandler: function(err, url, line) {
        alert("error " + err + " occurred at line " + line);

        // return true so Unity's error handler is not executed.
        return true;
    },
    compatibilitycheck: function() {
        // check compatibility ...
    }
  };
```