# Patching with AssetBundles

Patching AssetBundles is as simple as downloading a new AssetBundle and replacing the existing one. If `WWW.LoadFromCacheOrDownload` or `UnityWebRequest` are used to manage an application's cached AssetBundles, passing a different version parameter to the chosen API will trigger a download of the new AssetBundles.

The more difficult problem to solve in the patching system is detecting which AssetBundles to replace. A patching system requires two lists of information:

* A list of the currently downloaded AssetBundles, and their versioning information
* A list of the AssetBundles on the server, and their versioning information

The patcher should download the list of server-side AssetBundles and compare the AssetBundle lists. Missing AssetBundles, or AssetBundles whose versioning information has changed, should be re-downloaded.

It is also possible to write a custom system for detecting changes to AssetBundles. Most developers who write their own system choose to use an industry-standard data format for their AssetBundle file lists, such as JSON, and a standard C# class for computing checksums, such as MD5.

Unity builds AssetBundles with data ordered in a deterministic manner. This allows applications with custom downloaders to implement differential patching.

Unity does not provide any built-in mechanism for differential patching and neither `WWW.LoadFromCacheOrDownload` nor `UnityWebRequest` perform differential patching when using the built-in caching system. If differential patching is a requirement, then a custom downloader must be written.

---

* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>

