# Build manifest as ScriptableObject

`BuildManifestObject` is a [ScriptableObject](ScriptRef:ScriptableObject.html) that you can use to access the values in the [Build manifest](UnityCloudBuildManifest) via script, without needing to manually load the __UnityCloudBuildManifest.json__ TextAsset. 

It is an optional parameter to the pre-export invoked by Unity Cloud Build, if the __UnityCloudBuildManifest.json__ TextAsset has not been written. (See documentation on [Manifest as JSON](UnityCloudBuildManifestAsJSON).)

The following example C# code demonstrates a pre-export method that updates the `bundleVersion` in `PlayerSettings` based on the `buildNumber` provided in the manifest. For more info about pre-export methods, see documentation on [Pre- and Post-export methods](UnityCloudBuildPreAndPostExportMethods).

````
using UnityEngine;
using UnityEditor;
using System;

public class CloudBuildHelper : MonoBehaviour
{
    public static void PreExport(UnityEngine.CloudBuild.BuildManifestObject manifest)
    {
        PlayerSettings.bundleVersion = String.Format("1.0.{0}", manifest.GetValue("buildNumber", "unknown"));
    }
}
````

This is the public interface for the `BuildManifestObject` class:

````
namespace UnityEngine.CloudBuild
{
    public class BuildManifestObject : ScriptableObject
    {
        // Try to get a manifest value - returns true if key was found and could be cast to type T, otherwise returns false.
        public bool TryGetValue<T>(string key, out T result);
        // Retrieve a manifest value or throw an exception if the given key isn't found.
        public T GetValue<T>(string key);
        // Set the value for a given key.
        public void SetValue(string key, object value);
        // Copy values from a dictionary. ToString() will be called on dictionary values before being stored.
        public void SetValues(Dictionary<string, object> sourceDict);
        // Remove all key/value pairs.
        public void ClearValues();
        // Return a dictionary that represents the current BuildManifestObject.
        public Dictionary<string, object> ToDictionary();
        // Return a JSON formatted string that represents the current BuildManifestObject
        public string ToJson();
        // Return an INI formatted string that represents the current BuildManifestObject
        public override string ToString();
    }
}
````