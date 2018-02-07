Creating and Destroying GameObjects
===================================


Some games keep a constant number of objects in the scene, but it is very common for characters, treasures and other object to be created and removed during gameplay. In Unity, a GameObject can be created using the [Instantiate](ScriptRef:Object.Instantiate.html) function which makes a new copy of an existing object:



````
public GameObject enemy;

void Start() {
	for (int i = 0; i < 5; i++) {
		Instantiate(enemy);
	}
}

````

Note that the object from which the copy is made doesn't have to be present in the scene. It is more common to use a prefab dragged to a public variable from the Project panel in the editor. Also, instantiating a GameObject will copy all the Components present on the original.

There is also a [Destroy](ScriptRef:Object.Destroy.html) function that will destroy an object after the frame update has finished or optionally after a short time delay:



````
void OnCollisionEnter(Collision otherObj) {
    if (otherObj.gameObject.tag == "Missile") {
        Destroy(gameObject,.5f);
    }
}

````

Note that the Destroy function can destroy individual components without affecting the GameObject itself. A common mistake is to write something like:


	 Destroy(this);

...which will actually just destroy the script component that calls it rather than destroying the GameObject the script is attached to.
