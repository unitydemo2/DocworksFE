#Upgrading to Unity 2017.1


This page lists any changes in 2017.1 which might affect existing projects when you upgrade from earlier versions of Unity.

For example:

* Changes in data format which may require re-baking.

* Changes to the meaning or behavior of any existing functions, parameters or component values.

* Deprecation of any function or feature. (Alternatives are suggested.)

* * *

**UnityWebRequestTexture.GetTexture() nonReadable parameter change**
 
This convenience API had a bug where nonReadable worked the opposite way then it should, that is setting it to true would result in a readable texture and vice versa. Now this has been corrected and parameter works the way it’s documented. Note, that if you create DownloadHandlerTexture directly, you are not affected.
 
***

 
**Particle System Stretched Billboard Pivot parameter change**
 
X axis pivots are now accurate on Stretched Billboards. You may need to reconfigure your pivot settings on affected projects.
 
Y axis pivots are also accurate now and Unity automatically reconfigures these pivots when you upgrade your project.
 

***


<br/>
* <span class="page-edit"> 2017-05-19 <!-- include IncludeTextAmendPageSomeEdit --></span>