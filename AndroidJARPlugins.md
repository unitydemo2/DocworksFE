#JAR plug-ins


JAR(Java Archive) plug-ins are primarily used to enable interaction with the Android OS or to call methods written in Java from within your C# scripts.

They can only contain Java code (for example, they can’t contain Android resources), which makes their use very limited.
To add a JAR plug-in to your project, copy the .jar file into any of your project folders, then select it in Unity to open the Import Settings in the Inspector window. Tick the Android checkbox to mark this .jar file as compatible with Android:


![JAR plug-in import settings as displayed in the Inspector window](../uploads/Main/AndroidJARPlugins.png)


Using Java plug-ins
Unity uses the [Java Native Interface (JNI)](http://en.wikipedia.org/wiki/Java_Native_Interface) both when calling code from Java and when interacting with Java or the Java VM(Virtual Machine) from native code or C# scripts. 

##Using your Java plug-in from native (C/C++) code
Note: This information in this section requires advanced knowledge of the Android Java Native Interface (JNI).

To access your Java code from C or C++ plug-ins, you need access to the Java VM. Add the following method to your C/C++ code to access the Java VM.

```
jint JNI_OnLoad(JavaVM* vm, void* reserved) {
  JNIEnv* jni_env = 0;
  vm->AttachCurrentThread(&jni_env, 0);
  return JNI_VERSION_1_6;
}
```

It is beyond the scope of this document to explain JNI completely, but this method usually involves finding the class definition, resolving the constructor (\<init\>) method and creating a new object instance, as shown in this example:

```
jobject createJavaObject(JNIEnv* jni_env) {
  jclass cls_JavaClass = jni_env->FindClass("com/your/java/Class");         // find class definition
  jmethodID mid_JavaClass = jni_env->GetMethodID (cls_JavaClass, "<init>", "()V");      // find constructor method
  jobject obj_JavaClass = jni_env->NewObject(cls_JavaClass, mid_JavaClass);     // create object instance
  return jni_env->NewGlobalRef(obj_JavaClass);                      // return object with a global reference
}
```

For more information about JNI, see [Android Developer documentation on JNI](https://developer.android.com/training/articles/perf-jni.html)

##Using Your Java plug-in from C# scripts with helper classes
Note: This information in this section requires advanced knowledge of the Android Java Native Interface (JNI).

The [`AndroidJNIHelper`](ScriptRef:AndroidJNIHelper.html) and [`AndroidJNI`](ScriptRef:AndroidJNI.html) Unity API classes are used as a wrapper around a “raw” JNI interface.

The AndroidJavaObject and AndroidJavaClass Unity API classes automate a lot of tasks when using JNI calls, and they also use caching to make calls to Java faster. The combination of `AndroidJavaObject` and `AndroidJavaClass` is built on top of `AndroidJNI` and `AndroidJNIHelper`, but also has some additional functionality. These classes also have static methods that are used to  access static members of Java classes.

There are three ways to make Java JNI calls from your C# scripts:

* raw JNI through the `AndroidJNI` methods ;
* `AndroidJNIHelper` class together with `AndroidJNI`;
* `AndroidJavaObject` and `AndroidJavaClass` classes as the most convenient high-level APIs.

[UnityEngine.AndroidJNI](ScriptRef:AndroidJNI.html) is a wrapper for the JNI calls available in C (as described above). All methods in this class are static and have a 1:1 mapping to the Java Native Interface.

[UnityEngine.AndroidJNIHelper](ScriptRef:AndroidJNIHelper.html) provides helper functionality used by the next level, which is exposed as public methods and might be useful in special cases.

Instances of [UnityEngine.AndroidJavaObject](ScriptRef:AndroidJavaObject.html) and [UnityEngine.AndroidJavaClass](ScriptRef:AndroidJavaClass.html) have a one-to-one mapping to an instance of java.lang.Object and java.lang.Class (or their subclasses) on the Java side, respectively. They essentially provide 3 types of interaction with the Java side:

* Call a method

* Get the value of a field

* Set the value of a field

The call is separated into two categories: A call to a ‘void’ method, and call to a method with non-void return type. A generic type is used to represent the return type of those methods which return a non-void type. The Get and Set always take a generic type representing the field type.
##Examples

###Example 1

```
 AndroidJavaObject jo = new AndroidJavaObject("java.lang.String", "some_string"); 
 // jni.FindClass("java.lang.String"); 
 // jni.GetMethodID(classID, "<init>", "(Ljava/lang/String;)V"); 
 // jni.NewStringUTF("some_string"); 
 // jni.NewObject(classID, methodID, javaString); 
 int hash = jo.Call<int>("hashCode"); 
 // jni.GetMethodID(classID, "hashCode", "()I"); 
 // jni.CallIntMethod(objectID, methodID);
```

This example creates an instance of [java.lang.String](http://developer.android.com/reference/java/lang/String.html) initialized with a [string](http://developer.android.com/reference/java/lang/String.html#String(java.lang.StringBuilder)), and retrieves the [hash value](http://developer.android.com/reference/java/lang/String.html#hashCode()) for that string.

The `AndroidJavaObject` constructor takes at least one parameter - the name of the class of to construct an instance of. Any parameters after the class name are for the constructor call on the object, in this case the string “some_string”. The subsequent call to hashCode() returns an ‘int’ which is is used as the generic type parameter to the call method in this example.

__Note__: A nested Java class cannot be instantiated  using dotted notation. Inner classes must use the $ separator. Use `android.view.ViewGroup$LayoutParams` or `android/view/ViewGroup$LayoutParams`, where LayoutParams class is nested in ViewGroup class.

###Example 2

This example shows how to get the cache directory for the current application in C# without using plug-ins:

```
AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer"); 
 // jni.FindClass("com.unity3d.player.UnityPlayer"); 
 AndroidJavaObject jo = jc.GetStatic AndroidJavaObject>("currentActivity"); 
 // jni.GetStaticFieldID(classID, "Ljava/lang/Object;"); 
 // jni.GetStaticObjectField(classID, fieldID); 
 // jni.FindClass("java.lang.Object"); 

 Debug.Log(jo.Call AndroidJavaObject>("getCacheDir").Call<string>("getCanonicalPath")); 
 // jni.GetMethodID(classID, "getCacheDir", "()Ljava/io/File;"); // or any baseclass thereof! 
 // jni.CallObjectMethod(objectID, methodID); 
 // jni.FindClass("java.io.File"); 
 // jni.GetMethodID(classID, "getCanonicalPath", "()Ljava/lang/String;"); 
 // jni.CallObjectMethod(objectID, methodID); 
 // jni.GetStringUTFChars(javaString);
```

This example starts with `AndroidJavaClass` instead of `AndroidJavaObject` in order to access a static member of `com.unity3d.player.UnityPlayer` rather than create a new object. Then the static field “currentActivity” is accessed but this time `AndroidJavaObject` is used as the generic parameter. This is because the actual field type [android.app.Activity](http://developer.android.com/reference/android/app/Activity.html) is a subclass of [`java.lang.Object`](http://developer.android.com/reference/java/lang/Object.html), and any [non-primitive type](http://developer.android.com/reference/java/lang/Class.html) must be accessed as `AndroidJavaObject`. The exceptions to this rule are strings, which are accessed directly even though they don’t represent a primitive type in Java.

[`getCacheDir()`](http://developer.android.com/reference/android/content/Context.html#getCacheDir()) can then be called on the Activity object to get the File object representing the cache directory, [`getCanonicalPath()`](http://developer.android.com/reference/java/io/File.html#getCanonicalPath()) can then be called to get a string representation.

Unity provides access to the application’s cache and file directory with [`Application.temporaryCachePath`](https://docs.unity3d.com/ScriptReference/Application-temporaryCachePath.html) and [`Application.persistentDataPath`](https://docs.unity3d.com/ScriptReference/Application-persistentDataPath.html) APIs.

###Example 3

This example shows how to pass data from Java to Unity using `UnitySendMessage`.
using UnityEngine; 

```
public class NewBehaviourScript : MonoBehaviour { 

    void Start () { 
        AndroidJNIHelper.debug = true; 
        using (AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer")) { 
        jc.CallStatic("UnitySendMessage", "Main Camera", "JavaMessage", "NewMessage");
        } 
    } 

    void JavaMessage(string message) { 
        Debug.Log("message from java: " + message); 
    }
} 
```

The Java class `com.unity3d.player.UnityPlayer` has a static method [`UnitySendMessage`](https://docs.unity3d.com/Manual/PluginsForIOS.html), equivalent to the iOS method: `UnitySendMessage`. It is used in Java to pass data to Unity.

Although `UnitySendMessage` is called from within Unity, it relays the message using Java, then Java calls back to the native/Unity code to deliver the message to the object named “Main Camera”. This object has a script attached which contains a method called `JavaMessage`.

##Best practice when using Java plug-ins with Unity

`AndroidJavaObject` and `AndroidJavaClass` are computationally expensive methods (as are any methods that use raw JNI). Keep the number of transitions between managed and native/Java code to a minimum, for better performance and also code clarity.

```
//The first time you call a Java method like 
AndroidJavaObject jo = new AndroidJavaObject("java.lang.String", "some_string"); // somewhat expensive
int hash = jo.Call<int>("hashCode"); // first time - expensive
int hash = jo.Call<int>("hashCode"); // second time - not as expensive as we already know the java method and can call it directly
```

The Mono garbage collector should release all created instances of `AndroidJavaObject` and `AndroidJavaClass` after use, but it is advisable to keep them in a `using(){}` statement to ensure they are deleted as soon as possible. Without this, you cannot be sure when they are be destroyed. If you set `AndroidJNIHelper.debug` to true, you will see a record of the garbage collector’s activity in the debug output.

```
//Getting the system language safely
void Start () { 
    using (AndroidJavaClass cls = new AndroidJavaClass("java.util.Locale")) { 
        using(AndroidJavaObject locale = cls.CallStatic<AndroidJavaObject>("getDefault")) { 
            Debug.Log("current lang = " + locale.Call<string>("getDisplayLanguage")); 

        } 
    } 
}
```

<br/>

----
* <span class="page-edit">2017-05-18  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">Updated features in 5.5</span>
