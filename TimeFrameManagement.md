#Time and Framerate Management

The [Update](ScriptRef:MonoBehaviour.Update.html) function allows you to monitor inputs and other events regularly from a script and take appropriate action. For example, you might move a character when the "forward" key is pressed. An important thing to remember when handling time-based actions like this is that the game's framerate is not constant and neither is the length of time between Update function calls.

As an example of this, consider the task of moving an object forward gradually, one frame at a time. It might seem at first that you could just shift the object by a fixed distance each frame:

````
//C# script example
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	public float distancePerFrame;
	
	void Update() {
		transform.Translate(0, 0, distancePerFrame);
	}
}


//JS script example
var distancePerFrame: float;

function Update() {
	transform.Translate(0, 0, distancePerFrame);
}
````


However, given that the frame time is not constant, the object will appear to move at an irregular speed. If the frame time is 10 milliseconds then the object will step forward by _distancePerFrame_ one hundred times per second. But if the frame time increases to 25 milliseconds (due to CPU load, say) then it will only step forward forty times a second and therefore cover less distance. The solution is to scale the size of the movement by the frame time which you can read from the [Time.deltaTime](ScriptRef:Time-deltaTime.html) property:

````
//C# script example
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	public float distancePerSecond;
	
	void Update() {
		transform.Translate(0, 0, distancePerSecond * Time.deltaTime);
	}
}


//JS script example
var distancePerSecond: float;

function Update() {
	transform.Translate(0, 0, distancePerSecond * Time.deltaTime);
}
````

Note that the movement is now given as _distancePerSecond_ rather than _distancePerFrame_. As the framerate changes, the size of the movement step will change accordingly and so the object's speed will be constant.


##Fixed Timestep

Unlike the main frame update, Unity's physics system _does_ work to a fixed timestep, which is important for the accuracy and consistency of the simulation. At the start of the physics update, Unity sets an "alarm" by adding the fixed timestep value onto the time when the last physics update ended. The physics system will then perform calculations until the alarm goes off.

You can change the size of the fixed timestep from the [Time Manager](class-TimeManager) and you can read it from a script using the [Time.fixedDeltaTime](ScriptRef:Time-fixedDeltaTime.html) property. Note that a lower value for the timestep will result in more frequent physics updates and more precise simulation but at the cost of greater CPU load. You probably won't need to change the default fixed timestep unless you are placing high demands on the physics engine.


##Maximum Allowed Timestep

The fixed timestep keeps the physical simulation accurate in real time but it can cause problems in cases where the game makes heavy use of physics and the gameplay framerate has also become low (due to a large number of objects in play, say). The main frame update processing has to be "squeezed" in between the regular physics updates and if there is a lot of processing to do then several physics updates can take place during a single frame. Since the frame time, positions of objects and other properties are frozen at the start of the frame, the graphics can get out of sync with the more frequently updated physics.

Naturally, there is only so much CPU power available but Unity has an option to let you effectively slow down physics time to let the frame processing catch up. The _Maximum Allowed Timestep_ setting (in the [Time Manager](class-TimeManager)) puts a limit on the amount of time Unity will spend processing physics and FixedUpdate calls during a given frame update. If a frame update takes longer than _Maximum Allowed Timestep_ to process, the physics engine will "stop time" and let the frame processing catch up. Once the frame update has finished, the physics will resume as though no time has passed since it was stopped. The result of this is that rigidbodies will not move perfectly in real time as they usually do but will be slowed slightly. However, the physics "clock" will still track them as though they were moving normally. The slowing of physics time is usually not noticeable and is an acceptable trade-off against gameplay performance.


##Time Scale

For special effects, such as "bullet-time", it is sometimes useful to slow the passage of game time so that animations and script responses happen at a reduced rate. Furthermore, you may sometimes want to freeze game time completely, as when the game is paused. Unity has a _Time Scale_ property that controls how fast game time proceeds relative to real time. If the scale is set to 1.0 then game time matches real time. A value of 2.0 makes time pass twice as quickly in Unity (ie, the action will be speeded-up) while a value of 0.5 will slow gameplay down to half speed. A value of zero will make time "stop" completely. Note that the time scale doesn't actually slow execution but simply changes the time step reported to the Update and FixedUpdate functions via [Time.deltaTime](ScriptRef:Time-deltaTime.html) and [Time.fixedDeltaTime](ScriptRef:Time-fixedDeltaTime.html). The Update function is likely to be called more often than usual when game time is slowed down but the _deltaTime_ step reported each frame will simply be reduced. Other script functions are not affected by the time scale so you can, for example, display a GUI with normal interaction when the game is paused.

The [Time Manager](class-TimeManager) has a property to let you set the time scale globally but it is generally more useful to set the value from a script using the [Time.timeScale](ScriptRef:Time-timeScale.html) property:

````
//C# script example
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	void Pause() {
		Time.timeScale = 0;
	}
	
	void Resume() {
		Time.timeScale = 1;
	}
}

//JS script example
function Pause() {
	Time.timeScale = 0;
}

function Resume() {
	Time.timeScale = 1;
}
````

##Capture Framerate

A very special case of time management is where you want to record gameplay as a video. Since the task of saving screen images takes considerable time, the usual framerate of the game will be drastically reduced if you attempt to do this during normal gameplay. This will result in a video that doesn't reflect the true performance of the game.

Fortunately, Unity provides a [Capture Framerate](ScriptRef:Time-captureFramerate.html) property that lets you get around this problem. When the property's value is set to anything other than zero, game time will be slowed and the frame updates will be issued at precise regular intervals. The interval between frames is equal to 1 / Time.captureFramerate, so if the value is set to 5.0 then updates occur every fifth of a second. With the demands on framerate effectively reduced, you have time in the Update function to save screenshots or take other actions:

````
//C# script example
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	// Capture frames as a screenshot sequence. Images are
	// stored as PNG files in a folder - these can be combined into
	// a movie using image utility software (eg, QuickTime Pro).
	// The folder to contain our screenshots.
	// If the folder exists we will append numbers to create an empty folder.
	string folder = "ScreenshotFolder";
	int frameRate = 25;
		
	void Start () {
		// Set the playback framerate (real time will not relate to game time after this).
		Time.captureFramerate = frameRate;
		
		// Create the folder
		System.IO.Directory.CreateDirectory(folder);
	}
	
	void Update () {
		// Append filename to folder name (format is '0005 shot.png"')
		string name = string.Format("{0}/{1:D04} shot.png", folder, Time.frameCount );
		
		// Capture the screenshot to the specified file.
		Application.CaptureScreenshot(name);
	}
}

//JS script example

// Capture frames as a screenshot sequence. Images are
// stored as PNG files in a folder - these can be combined into
// a movie using image utility software (eg, QuickTime Pro).
// The folder to contain our screenshots.
// If the folder exists we will append numbers to create an empty folder.
var folder = "ScreenshotFolder";
var frameRate = 25;


function Start () {
	// Set the playback framerate (real time will not relate to game time after this).
	Time.captureFramerate = frameRate;

	// Create the folder
	System.IO.Directory.CreateDirectory(folder);
}

function Update () {
	// Append filename to folder name (format is '0005 shot.png"')
	var name = String.Format("{0}/{1:D04} shot.png", folder, Time.frameCount );

	// Capture the screenshot to the specified file.
	Application.CaptureScreenshot(name);
}
````

Although the video recorded using this technique typically looks very good, the game can be hard to play when slowed-down drastically. You may need to experiment with the value of Time.captureFramerate to allow ample recording time without unduly complicating the task of the test player.