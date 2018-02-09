# Build manifest

It’s often useful for your game’s run-time code to know key information about the build itself. Information like the name and number of the build is very useful when reporting bugs or tracking analytics. To help facilitate this, Unity Cloud Build injects a "manifest" into your game at build time, so that this key data can be accessed later at runtime.

The Unity Cloud Build manifest is provided as a JSON formatted [TextAsset](class-TextAsset). This is stored as a game resource, accessible via `Resources.Load()`. The build manifest contains the following values:

|**Value:** |**Properties:** |
|:---|:---|
|`scmCommitId`|	The commit or changelist that was built.|
|`scmBranch`|	The name of the branch that was built.|
|`buildNumber`|	The Unity Cloud Build "build number" corresponding to this build.|
|`buildStartTime`|	The UTC timestamp when the build process was started.|
|`projectId`|	The Unity project identifier.|
|`bundleId`|	The `bundleIdentifier` configured in Unity Cloud Build (iOS and Android only).|
|`unityVersion`|	The version of Unity that Unity Cloud Build used to create the build.|
|`xcodeVersion`|	The version of XCode used to build the project (iOS only).|
|`cloudBuildTargetName`|	The name of the build target that was built.|

The manifest TextAsset, called __UnityCloudBuildManifest.json__, is written to the _Assets/UnityCloud/Resources_ folder.

##For local testing

To test the build manifest functionality locally, name your file **UnityCloudBuildManifest.json.txt** (but don't commit this file to your project's **Assets/UnityCloud/Resources** folder in your code repository, because it might interfere with the Unity Cloud Build manifest file).

##Using the manifest

You can access the manifest at runtime via:

* [Manifest as JSON](UnityCloudBuildManifestAsJSON)

* [Manifest as ScriptableObject](UnityCloudBuildManifestAsScriptableObject)