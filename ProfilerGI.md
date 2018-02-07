# Global Illumination Profiler

![](../uploads/Main/ProfilerGI.png)

The Global Illumination Profiler shows statistics and how much CPU time is consumed by the real-time Global Illumination (GI) subsystem across all worker threads. GI is managed in Unity by a piece of middleware called Enlighten. See documentation on [Global Illumination](GlobalIllumination) for more information. 

|:---|:---| 
|**Name** | **Description** |
|__Total CPU Time__|Total Enlighten CPU time across all threads.|
|__Probe Update Time__| Time spent updating Light Probes.|
|__Setup Time__|Time spent in the Setup stage.|
|__Environment Time__ |Time spent processing Environment lighting.|
|__Input Lighting Time__|Time spent processing input lighting.|
|__Systems Time__|Time spent updating Systems.|
|__Solve Tasks Time__|Time spent running radiosity solver tasks.|
|__Dynamic Objects Time__|Time spent updating Dynamic GameObjects.|
|__Time Between Updates__|Time between Global Illumination updates.|
|__Other Commands Time__|Time spent processing other commands.|
|__Blocked Command Write Time__|Time spent in blocked state.|
|__Blocked Buffer Writes__|Number of blocked writes.|
|__Total Light Probes__|Total number of Light Probes in the Scene.|
|__Solved Light Probes__|Number of solved Light Probes since the last update.|
|__Probe Sets__|Number of Light Probe sets in the Scene.|
|__Systems__|Number of Enlighten Systems in the Scene.|

---
* <span class="page-edit">2017-08-30  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in Unity 2017.2</span>









