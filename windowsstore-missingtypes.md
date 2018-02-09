# Windows Store Apps: Missing .NET Types on .NET Scripting Backend

The .NET scripting backend that is used on Windows Store is a special .NET version for this platform, which is not entirely compatible with Mono. In particular some data types are missing and some other classes don't have certain methods, that the same classes do have in Mono.

To make porting existing games to Windows Store easier, some of the missing .NET types are provided by Unity. In addition some extension methods and replacement types were added to make migration easier.

These types are placed in **PlaybackEngines\metrosupport\Managed\WinRTLegacy.dll**, every Windows Store SDK has its own WinRTLegacy.dll.

Types, provided by Unity include:

* System.Collections.ArrayList
* System.Collections.Hashtable
* System.Collections.Queue
* System.Collections.SortedList
* System.Collections.Stack
* System.Collections.Specialized.HybridDictionary
* System.Collections.Specialized.ListDictionary
* System.Collections.Specialized.NameValueCollection
* System.Collections.Specialized.OrderedDictionary
* System.Collections.Specialized.StringCollection
* System.IO.Directory
* System.IO.File
* System.IO.FileStream
* System.Xml.XmlDocument
* System.Xml.XmlTextReader
* System.Xml.XmlTextWriter

In addition to these a namespace WinRTLegacy is added to provide additional classes and extention methods. Among there are:

* Extention methods Close() for most System.IO classes (alternatively you can use Dispose(), which is available on both Mono and .NET for Windows Store Apps)
* WinRTLegacy.TypeExtensions has methods GetConstructor(), GetMethod(), GetProperty() for System.Type
* WinRTLegacy.IO.StreamReader class, that is compatible with Mono System.IO.StreamReader
* WinRTLegacy.IO.StreamWriter class, that is compatible with Mono System.IO.StreamWriter
* WinRTLegacy.Xml.XmlReader class, that is compatible with Mono System.Xml.XmlReader
* WinRTLegacy.Xml.XmlWriter class, that is compatible with Mono System.Xml.XmlWriter

The simplest way to use the replacement classes from WinRTLegacy is via using directive:

```C#
#if NETFX_CORE
using XmlReader = WinRTLegacy.Xml.XmlReader;
#else
using XmlReader = System.Xml.XmlReader;
#endif
```

This way you can use XmlReader class, which will be taken from WinRTLegacy.Xml namespace on Windows Store and from System.Xml namespace elsewhere.


### Universal Windows 10 Apps

Some of the types were brought back to .NET for Universal Windows 10 Apps, thus implementations for these types were removed in WinRTLegacy.dll