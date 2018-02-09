#Reverb Zones



__Reverb Zones__ take an [Audio Clip](class-AudioClip) and distorts it depending where the audio listener is located inside the reverb zone. They are used when you want to gradually change from a point where there is no ambient effect to a place where there is one, for example when you are entering a cavern.


Properties
----------

![](../uploads/Main/AudioReverbZone.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Min Distance__ |Represents the radius of the inner circle in the gizmo, this determines the zone where there is a gradually reverb effect and a full reverb zone.|
|__Max Distance__ |Represents the radius of the outer circle in the gizmo, this determines the zone where there is no effect and where the reverb starts to get applied gradually.|
|__Reverb Preset__ |Determines the reverb effect that will be used by the reverb zone.|

This diagram illustrates the properties of the reverb zone.

![How the sound works in a reverb zone](../uploads/Main/ReverbZoneExpl.png) 


Hints
------

You can mix reverb zones to create combined effects.
