#Mobile Device Input


On mobile devices, the [Input](ScriptRef:Input.html) class offers access to touchscreen, accelerometer and geographical/location input. 

Access to keyboard on mobile devices is provided via the [iOS keyboard](MobileKeyboard).

###Multi-Touch Screen


The iPhone and iPod Touch devices are capable of tracking up to five fingers touching the screen simultaneously. You can retrieve the status of each finger touching the screen during the last frame by accessing the [Input.touches](ScriptRef:Input-touches.html) property array.

Android devices don't have a unified limit on how many fingers they track. Instead, it varies from device to device and can be anything from two-touch on older devices to five fingers on some newer devices.

Each finger touch is represented by an [Input.Touch](ScriptRef:Touch.html) data structure:

|**_Property:_** |**_Function:_** |
|:---|:---|
|__fingerId__ |The unique index for a touch.|
|__position__ |The screen position of the touch.|
|__deltaPosition__ |The screen position change since the last frame.|
|__deltaTime__ |Amount of time that has passed since the last state change.|
|__tapCount__ |The iPhone/iPad screen is able to distinguish quick finger taps by the user. This counter will let you know how many times the user has tapped the screen without moving a finger to the sides. Android devices do not count number of taps, this field is always 1.|
|__phase__ |Describes so called "phase" or the state of the touch. It can help you determine if the touch just began, if user moved the finger or if they just lifted the finger.|

Phase can be one of the following:

| | |
|:---|:---|
|__Began__ |A finger just touched the screen.|
|__Moved__ |A finger moved on the screen.|
|__Stationary__ |A finger is touching the screen but hasn't moved since the last frame.|
|__Ended__ |A finger was lifted from the screen. This is the final phase of a touch.|
|__Canceled__ |The system cancelled tracking for the touch, as when (for example) the user puts the device to their face or more than five touches happened simultaneously. This is the final phase of a touch.|

Following is an example script which will shoot a ray whenever the user taps on the screen:


````
var particle : GameObject;
function Update () {
	for (var touch : Touch in Input.touches) {
		if (touch.phase == TouchPhase.Began) {
			// Construct a ray from the current touch coordinates
			var ray = Camera.main.ScreenPointToRay (touch.position);
			if (Physics.Raycast (ray)) {
				// Create a particle if hit
				Instantiate (particle, transform.position, transform.rotation);
			}
		}
	}
}


````

###Mouse Simulation
On top of native touch support Unity iOS/Android provides a mouse simulation. You can use mouse functionality from the standard [Input](ScriptRef:Input.html) class. Note that iOS/Android devices are designed to support multiple finger touch.  Using the mouse functionality will support just a single finger touch.  Also, finger touch on mobile devices can move from one area to another with no movement between them.  Mouse simulation on mobile devices will provide movement, so is very different compared to touch input.  The recommendation is to use the mouse simulation during early development but to use touch input as soon as possible.

###Accelerometer


As the mobile device moves, a built-in accelerometer reports linear acceleration
changes along the three primary axes in three-dimensional space. Acceleration
along each axis is reported directly by the hardware as G-force values. A value
of 1.0 represents a load of about +1g along a given axis while a value of -1.0
represents -1g. If you hold the device upright (with the home button at the
bottom) in front of you, the X axis is positive along the right, the Y axis is
positive directly up, and the Z axis is positive pointing toward you.

You can retrieve the accelerometer value by accessing the [Input.acceleration](ScriptRef:Input-acceleration.html) property.

The following is an example script which will move an object using the accelerometer:


````
var speed = 10.0;
function Update () {
	var dir : Vector3 = Vector3.zero;

	// we assume that the device is held parallel to the ground
	// and the Home button is in the right hand

	// remap the device acceleration axis to game coordinates:
	// 1) XY plane of the device is mapped onto XZ plane
	// 2) rotated 90 degrees around Y axis
	dir.x = -Input.acceleration.y;
	dir.z = Input.acceleration.x;

	// clamp acceleration vector to the unit sphere
	if (dir.sqrMagnitude > 1)
		dir.Normalize();

	// Make it move 10 meters per second instead of 10 meters per frame...
	dir *= Time.deltaTime;

	// Move object
	transform.Translate (dir * speed);
}


````

###Low-Pass Filter
Accelerometer readings can be jerky and noisy. Applying low-pass filtering on the signal allows you to smooth it and get rid of high frequency noise.

The following script shows you how to apply low-pass filtering to accelerometer readings:


````
var AccelerometerUpdateInterval : float = 1.0 / 60.0;
var LowPassKernelWidthInSeconds : float = 1.0;

private var LowPassFilterFactor : float = AccelerometerUpdateInterval / LowPassKernelWidthInSeconds; // tweakable
private var lowPassValue : Vector3 = Vector3.zero;
function Start () {
	lowPassValue = Input.acceleration;
}

function LowPassFilterAccelerometer() : Vector3 {
	lowPassValue = Vector3.Lerp(lowPassValue, Input.acceleration, LowPassFilterFactor);
	return lowPassValue;
}


````

The greater the value of `LowPassKernelWidthInSeconds`, the slower the filtered value will converge towards the current input sample (and vice versa).

###I'd like as much precision as possible when reading the accelerometer. What should I do?
Reading the [Input.acceleration](ScriptRef:Input-acceleration.html) variable does not equal sampling the hardware. Put simply, Unity samples the hardware at a frequency of 60Hz and stores the result into the variable. In reality, things are a little bit more complicated -- accelerometer sampling doesn't occur at consistent time intervals, if under significant CPU loads. As a result, the system might report 2 samples during one frame, then 1 sample during the next frame.

You can access all measurements executed by accelerometer during the frame. The following code will illustrate a simple average of all the accelerometer events that were collected within the last frame:



````
var period : float = 0.0;
var acc : Vector3 = Vector3.zero;
for (var evnt : iPhoneAccelerationEvent in iPhoneInput.accelerationEvents) {
	acc += evnt.acceleration * evnt.deltaTime;
	period += evnt.deltaTime;
}
if (period > 0)
	acc *= 1.0/period;
return acc;


````

