#Coroutines

When you call a function, it runs to completion before returning. This effectively means that any action taking place in a function must happen within a single frame update; a function call can't be used to contain a procedural animation or a sequence of events over time. As an example, consider the task of gradually reducing an object's alpha (opacity) value until it becomes completely invisible.

````
void Fade() {
	for (float f = 1f; f >= 0; f -= 0.1f) {
		Color c = renderer.material.color;
		c.a = f;
		renderer.material.color = c;
	}
}

````

As it stands, the Fade function will not have the effect you might expect. In order for the fading to be visible, the alpha must be reduced over a sequence of frames to show the intermediate values being rendered. However, the function will execute in its entirety within a single frame update. The intermediate values will never be seen and the object will disappear instantly.

It is possible to handle situations like this by adding code to the Update function that executes the fade on a frame-by-frame basis. However, it is often more convenient to use a coroutine for this kind of task.

A coroutine is like a function that has the ability to pause execution and return control to Unity but then to continue where it left off on the following frame. In C#, a coroutine is declared like this:



````
IEnumerator Fade() {
	for (float f = 1f; f >= 0; f -= 0.1f) {
		Color c = renderer.material.color;
		c.a = f;
		renderer.material.color = c;
		yield return null;
	}
}

````

It is essentially a function declared with a return type of IEnumerator and with the yield return statement included somewhere in the body. The yield return line is the point at which execution will pause and be resumed the following frame. To set a coroutine running, you need to use the [StartCoroutine](ScriptRef:MonoBehaviour.StartCoroutine.html) function:



````
void Update() {
	if (Input.GetKeyDown("f")) {
		StartCoroutine("Fade");
	}
}

````

In UnityScript, things are slightly simpler. Any function that includes the yield statement is understood to be a coroutine and the IEnumerator return type need not be explicitly declared:



````
function Fade() {
	for (var f = 1.0; f >= 0; f -= 0.1) {
		var c = renderer.material.color;
		c.a = f;
		renderer.material.color = c;
		yield;
	}
}

````

Also, a coroutine can be started in UnityScript by calling it as if it were a normal function:



````
function Update() {
	if (Input.GetKeyDown("f")) {
		Fade();
	}
}

````

You will notice that the loop counter in the Fade function maintains its correct value over the lifetime of the coroutine. In fact any variable or parameter will be correctly preserved between yields.

By default, a coroutine is resumed on the frame after it yields but it is also possible to introduce a time delay using [WaitForSeconds](ScriptRef:WaitForSeconds.html):



````
IEnumerator Fade() {
	for (float f = 1f; f >= 0; f -= 0.1f) {
		Color c = renderer.material.color;
		c.a = f;
		renderer.material.color = c;
		yield return new WaitForSeconds(.1f);
	}
}

````

and in UnityScript:



````
function Fade() {
	for (var f = 1.0; f >= 0; f -= 0.1) {
		var c = renderer.material.color;
		c.a = f;
		renderer.material.color = c;
		yield WaitForSeconds(0.1);
	}
}

````

This can be used as a way to spread an effect over a period of time, but it is also a useful optimization. Many tasks in a game need to be carried out periodically and the most obvious way to do this is to include them in the Update function. However, this function will typically be called many times per second. When a task doesn't need to be repeated quite so frequently, you can put it in a coroutine to get an update regularly but not every single frame. An example of this might be an alarm that warns the player if an enemy is nearby. The code might look something like this:



````
function ProximityCheck() {
	for (int i = 0; i < enemies.Length; i++) {
		if (Vector3.Distance(transform.position, enemies[i].transform.position) < dangerDistance) {
				return true;
		}
	}
	
	return false;
}

````

If there are a lot of enemies then calling this function every frame might introduce a significant overhead. However, you could use a coroutine to call it every tenth of a second:



````
IEnumerator DoCheck() {
	for(;;) {
		ProximityCheck;
		yield return new WaitForSeconds(.1f);
	}
}

````

This would greatly reduce the number of checks carried out without any noticeable effect on gameplay.

Note: Coroutines are not stopped when a MonoBehaviour is disabled, but only when it is definitely destroyed. You can stop a Coroutine using MonoBehaviour.StopCoroutine and MonoBehaviour.StopAllCoroutines. Coroutines are also stopped when the MonoBehaviour is destroyed.