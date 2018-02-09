State Synchronization
=============================

State Synchronization is done from the Server to Remote Clients. The local client does not have data serialized to it, since it shares the scene with the server. Any data serialized to a local client would be redundant. SyncVar hooks however are called on local clients.

Data is not synchronized from remote clients to the server.  This is job of Commands.

SyncVars
--------

SyncVars are member variables of NetworkBehaviour scripts that are synchronized from the server to clients. When an object is spawned, or a new player joins a game in progress, they are sent the latest state of all SyncVars on networked objects that are visible to them. Member variables are made into SyncVars by using the [SyncVar] custom attribute:

````
class Player : NetworkBehaviour
{

	[SyncVar]
	int health;

	public void TakeDamage(int amount)
	{
		if (!isServer)
			return;

		health -= amount;
	}
}
````

The state of SyncVars is applied to objects on clients before OnStartClient() is called, so the state of the object is guaranteed to be up-to-date inside OnStartClient().

SyncVars can be basic types such as integers, strings and floats. They can also be Unity types such as Vector3 and user-defined structs, but updates for struct SyncVars are sent as monolithic updates, not incremental changes if fields within a struct change. There can be up to 32 SyncVars on a single NetworkBehaviour script - this includes SyncLists.

SycnVar updates are sent automatically by the server when the value of a SyncVar changes. There is no need to perform any manual dirtying of fields for SyncVars.

SyncLists
---------

SyncLists are like SyncVars but they are lists of values instead of individual values. SyncList contents are included in initial state updates with SyncVar state.  SyncLists do not require the SyncVar attributes, they are specific classes. There are built-in SyncList types for basic types:

* SyncListString
* SyncListFloat
* SyncListInt
* SyncListUInt
* SyncListBool

There is also SyncListStruct which can be used for lists of user-defined structs. The struct used SyncListStruct derived class can contain members of basic types, arrays, and common Unity types. They cannot contain complex classes or generic containers.

SyncLists have a SyncListChanged delegate named Callback that allows clients to be notified when the contents of the list change. This delegate is called with the type of operation that occurred, and th eindex of the item that the operation was for.

```
public class MyScript : NetworkBehaviour
{
	public struct Buf
	{
		public int id;
		public string name;
		public float timer;
	};
			
	public class TestBufs : SyncListStruct<Buf> {}
	TestBufs m_bufs = new TestBufs();
	
	void BufChanged(SyncListStruct<Buf>.Operation op, int itemIndex)
	{
	    Debug.Log("buf changed:" + op);
	}
	
	void Start()
	{
	    m_bufs.Callback = BufChanged;
	}
}
```		


Custom Serialization Functions
------------------------------

Often the use of SyncVars is enough for scripts to serialize their state to clients, but some cases require more complex serialization code. The virtual functions on NetworkBehaviour that are used for SyncVar serialization can be implmented by developers to perform their own custom serialization. These functions are:

````
public virtual bool OnSerialize(NetworkWriter writer, bool initialState);
public virtual void OnDeSerialize(NetworkReader reader, bool initialState);
````

The initialState flag is useful to differentiate between the first time an object is serialized and when incremental updates can be sent. The first time an object is sent to a client, it must include a full state snapshot, but subsequent updates can save on bandwidth by including only incremental changes. Note that SyncVar hook fucntion are not called when initialState is true, only for incremental updates.

If a class has SyncVars, then implementations of these functions are added automatically to the class. So a class that has SyncVars cannot also have custom serialization functions.

The OnSerialize function should return true to indicate that an update should be sent. If it returns true, then the dirty bits for that script are set to zero, if it returns false then the dirty bits are not changed. This allows multiple changes to a script to be accumulated over time and sent when the system is ready, instead of every frame.

Serialization Flow
------------------
Game objects with the NetworkIdentity component can have multiple scripts derived from NetworkBehaviour. The flow for serializing these objects is:

On the server:

* Each NetworkBehaviour has a dirty mask. This mask is available inside OnSerialize as syncVarDirtyBits
* Each SyncVar in a NetworkBehaviour script is assigned a bit in the dirty mask.
* Changing the value of SyncVars causes the bit for that SyncVar to be set in the dirty mask
* Alternatively, calling SetDirtyBit() writes directly to the dirty mask
* NetworkIdentity objects are checked on the server as part of it's update loop
* If any NetworkBehaviours on a NetworkIdentity are dirty, then an UpdateVars packet is created for that object
* The UpdateVars packet is populated by calling OnSerialize on each NetworkBehaviour on the object
* NetworkBehaviours that are NOT dirty write a zero to the packet for their dirty bits
* NetworkBehaviours that are dirty write their dirty mask, then the values for the SyncVars that have changed
* If OnSerialize returns true for a NetworkBehaviour, the dirty mask is reset for that NetworkBehaviour, so it will not send again until it's value changes.
* The UpdateVars packet is sent to ready clients that are observing the object

On the client:

* an UpdateVars packet is received for an object
* The OnDeserialize function is called for each NetworkBehaviour script on the object
* Each NetworkBehaviour script on the object reads a dirty mask.
* If the dirty mask for a NetworkBehaviour is zero, the OnDeserialize functions returns without reading any more
* If the dirty mask is non-zero value, then the OnDeserialize function reads the values for the SyncVars that correspond to the dirty bits that are set
* If there are SyncVar hook functions, those are invoked with the value read from the stream.

So for this script:

````
public class data : NetworkBehaviour
{

	[SyncVar]
	public int int1 = 66;

	[SyncVar]
	public int int2 = 23487;

	[SyncVar]
	public string MyString = "esfdsagsdfgsdgdsfg";
}
````

The generated OnSerialize function is something like:

````
public override bool OnSerialize(NetworkWriter writer, bool forceAll)
{
	if (forceAll)
	{
		// the first time an object is sent to a client, send all the data (and no dirty bits)
		writer.WritePackedUInt32((uint)this.int1);
		writer.WritePackedUInt32((uint)this.int2);
		writer.Write(this.MyString);
		return true;
	}
	bool wroteSyncVar = false;
	if ((base.get_syncVarDirtyBits() & 1u) != 0u)
	{
		if (!wroteSyncVar)
		{
			// write dirty bits if this is the first SyncVar written
			writer.WritePackedUInt32(base.get_syncVarDirtyBits());
			wroteSyncVar = true;
		}
		writer.WritePackedUInt32((uint)this.int1);
	}
	if ((base.get_syncVarDirtyBits() & 2u) != 0u)
	{
		if (!wroteSyncVar)
		{
			// write dirty bits if this is the first SyncVar written
			writer.WritePackedUInt32(base.get_syncVarDirtyBits());
			wroteSyncVar = true;
		}
		writer.WritePackedUInt32((uint)this.int2);
	}
	if ((base.get_syncVarDirtyBits() & 4u) != 0u)
	{
		if (!wroteSyncVar)
		{
			// write dirty bits if this is the first SyncVar written
			writer.WritePackedUInt32(base.get_syncVarDirtyBits());
			wroteSyncVar = true;
		}
		writer.Write(this.MyString);
	}

	if (!wroteSyncVar)
	{
		// write zero dirty bits if no SyncVars were written
		writer.WritePackedUInt32(0);
	}
	return wroteSyncVar;
}
````

And the OnDeserialize function is something like:

````
public override void OnDeserialize(NetworkReader reader, bool initialState)
{
	if (initialState)
	{
		this.int1 = (int)reader.ReadPackedUInt32();
		this.int2 = (int)reader.ReadPackedUInt32();
		this.MyString = reader.ReadString();
		return;
	}
	int num = (int)reader.ReadPackedUInt32();
	if ((num & 1) != 0)
	{
		this.int1 = (int)reader.ReadPackedUInt32();
	}
	if ((num & 2) != 0)
	{
		this.int2 = (int)reader.ReadPackedUInt32();
	}
	if ((num & 4) != 0)
	{
		this.MyString = reader.ReadString();
	}
}
````

If a NetworkBehaviour has a base class that also has serialization functions, the base class functions should also be called.

Note that the UpdateVar packets created for object state updates may be aggregated in buffers before being sent to the client, so a single transport layer packet may contain updates for multiple objects.
