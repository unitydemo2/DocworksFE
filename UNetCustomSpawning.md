Custom Spawn Functions
-----------------------

The default behaviour of creating spawned objects from prefabs on the client can be customized by using spawn handler functions. This way you have full control of how you spawn the object as well as how you un-spawn it. You can register functions to spawn and un-spawn client objects with [ClientScene.RegisterSpawnHandler](ScriptRef:Networking.ClientScene.RegisterSpawnHandler). The server creates objects directly and then spawn them on the clients though this functionality. This function takes the asset ID of the object and two function delegates, one to handle creating objects on the client and one to handler destroying objects on the client. The asset ID can be a dynamic one or just the asset ID found on the prefab object you want to spawn (if you have one). 

The spawn / un-spawner need to have this object signature, this is defined in the high level API.

````
// Handles requests to spawn objects on the client
public delegate GameObject SpawnDelegate(Vector3 position, NetworkHash128 assetId);

// Handles requests to unspawn objects on the client
public delegate void UnSpawnDelegate(GameObject spawned);
````

The asset ID passed to the spawn function can be found on [NetworkIdentity.assetId](ScriptRef:Networking.NetworkIdentity-assetId) for prefabs, where it is populated automatically. The registration for a dynamic asset ID is handled liked his:

````
// generate a new unique assetId 
NetworkHash128 creatureAssetId = NetworkHash128.Parse("e2656f");

// register handlers for the new assetId
ClientScene.RegisterSpawnHandler(creatureAssetId, SpawnCreature, UnSpawnCreature);

// get assetId on an existing prefab
NetworkHash128 bulletAssetId = bulletPrefab.GetComponent<NetworkIdentity>().assetId;

// register handlers for an existing prefab you'd like to custom spawn
ClientScene.RegisterSpawnHandler(bulletAssetId, SpawnBullet, UnSpawnBullet);

// spawn a bullet - SpawnBullet will be called on client.
NetworkServer.Spawn(gameObject, creatureAssetId);
````

The spawn functions themselves are implemented with the delegate signature, here is the bullet spawner but the SpawnCreature would look the same but have different spawn logic

````
public GameObject SpawnBullet(Vector3 position, NetworkHash128 assetId)
{
	return (GameObject)Instantiate(m_BulletPrefab, position, Quaternion.identity);
}
public void UnSpawnBullet(GameObject spawned)
{
	Destroy(spawned);
}
````

When using custom spawn functions, it is sometimes useful to be able to unspawn objects without destroying them. This can be done by calling [NetworkServer.UnSpawn](ScriptRef:Networking.NetworkServer.UnSpawn). This causes a message to be sent to clients to un-spawn the object, so that the custom un-spawn function will be called on the clients. The object is not destroyed when this function is called.

Note that on the host, object are not spawned for the local client as they already exist on the server. So no spawn handler functions will be called.

Setting up an object pool with custom spawn handlers
-----------------------

Here is an example of how you might set up a very simple object pooling system with custom spawn handlers. Spawning and unspawning then just puts objects in or out of the pool.

````
using UnityEngine;
using UnityEngine.Networking;
using System.Collections;

public class SpawnManager : MonoBehaviour
{
	public int m_ObjectPoolSize = 5;
	public GameObject m_Prefab;
	public GameObject[] m_Pool;

	public NetworkHash128 assetId { get; set; }
	
	public delegate GameObject SpawnDelegate(Vector3 position, NetworkHash128 assetId);
	public delegate void UnSpawnDelegate(GameObject spawned);

	void Start()
	{
		assetId = m_Prefab.GetComponent<NetworkIdentity> ().assetId;
		m_Pool = new GameObject[m_ObjectPoolSize];
		for (int i = 0; i < m_ObjectPoolSize; ++i)
		{
			m_Pool[i] = (GameObject)Instantiate(m_Prefab, Vector3.zero, Quaternion.identity);
			m_Pool[i].name = "PoolObject" + i;
			m_Pool[i].SetActive(false);
		}
		
		ClientScene.RegisterSpawnHandler(assetId, SpawnObject, UnSpawnObject);
	}

	public GameObject GetFromPool(Vector3 position)
	{
		foreach (var obj in m_Pool)
		{
			if (!obj.activeInHierarchy)
			{
				Debug.Log("Activating object " + obj.name + " at " + position);
				obj.transform.position = position;
				obj.SetActive (true);
				return obj;
			}
		}
		Debug.LogError ("Could not grab object from pool, nothing available");
		return null;
	}
	
	public GameObject SpawnObject(Vector3 position, NetworkHash128 assetId)
	{
		return GetFromPool(position);
	}
	
	public void UnSpawnObject(GameObject spawned)
	{
		Debug.Log ("Re-pooling object " + spawned.name);
		spawned.SetActive (false);
	}
}
````

To use this manager do the following

* This works in a scene like the one in the [Getting Started](UNetSetup) guide.
* Create a new empty game object called "SpawnManager"
* Create a SpawnManager script for the code above and add that to a new SpawnManager object
* Drag a prefab you want to spawn multiple times to the prefab field and set the size (default is 5).
* Set up a reference to the spawn manager in the player movement script

````
SpawnManager spawnManager;

void Start()
{
	spawnManager = GameObject.Find("SpawnManager").GetComponent<SpawnManager> ();
}
````

* The player logic could contain something like this to move and fire bullets

````
void Update()
{
	if (!isLocalPlayer)
		return;
	
	var x = Input.GetAxis("Horizontal")*0.1f;
	var z = Input.GetAxis("Vertical")*0.1f;
	
	transform.Translate(x, 0, z);

	if (Input.GetKeyDown(KeyCode.Space))
	{
		// Command function is called on the client, but invoked on the server
		CmdFire();
	}
}
````

* In the fire logic on the player, make it use the object pool

````
[Command]
void CmdFire()
{
	// Set up bullet on server
	var bullet = spawnManager.GetFromPool(transform.position + transform.forward);	
	bullet.GetComponent<Rigidbody>().velocity = transform.forward*4;
	
	// spawn bullet on client, custom spawn handler will be called
	NetworkServer.Spawn(bullet, spawnManager.assetId);
	
	// when the bullet is destroyed on the server it is automatically destroyed on clients
	StartCoroutine (Destroy (bullet, 2.0f));
}

public IEnumerator Destroy(GameObject go, float timer)
{
	yield return new WaitForSeconds (timer);
	spawnManager.UnSpawnObject(go);
	NetworkServer.UnSpawn(go);
}
````

The automatic destruction shows how the objects are returned to the pool and re-used when you fire again.