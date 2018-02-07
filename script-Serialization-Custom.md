# Custom serialization

Serialization is the automatic process of transforming data structures or object states into a format that Unity can store and reconstruct later. (See the documentation on [Script Serialization](script-Serialization) for further information on Unity's serialization.)

Sometimes you might want to serialize something that Unity's serializer doesn't support. In many cases the best approach is to use serialization callbacks. (See Unity's Scripting API Reference: [ISerializationCallbackReceiver](ScriptRef:ISerializationCallbackReceiver.html) for further information on custom serialization using serlialization callbacks.)

Serialization callbacks allow you to be notified before the serializer reads data from your fields and after it has finished writing to them. You can use serialization callbacks to give your hard-to-serialize data a different representation at runtime to its representation when you actually serialize.


To do this, transform your data into something Unity understands right before Unity wants to serialize it.  Then, right after Unity has written the data to your fields, you can transform the serialized form back into the form you want to have your data in at runtime 

For example: You want to have a tree data structure. If you let Unity directly serialize the data structure, the "no support for null" limitation would cause your data stream to become very big, leading to performance degradations in many systems. This is shown in Example 1, below.

**Example 1**: Unity's direct serlialization, leading to performance issues

````

using UnityEngine;
using System.Collections.Generic;
using System;

public class VerySlowBehaviourDoNotDoThis : MonoBehaviour {
	[Serializable]
	public class Node {
		public string interestingValue = "value";
		//The field below is what makes the serialization data become huge because
		//it introduces a 'class cycle'.
		public List<Node> children = new List<Node>();
	}
	//this gets serialized
	public Node root = new Node();
	void OnGUI() {
		Display (root);
	}
	void Display(Node node) {
		GUILayout.Label ("Value: ");
		node.interestingValue = GUILayout.TextField(node.interestingValue, GUILayout.Width(200));
		GUILayout.BeginHorizontal ();
		GUILayout.Space (20);
		GUILayout.BeginVertical ();
		foreach (var child in node.children)
		Display (child);
		if (GUILayout.Button ("Add child"))
		node.children.Add (new Node ());
		GUILayout.EndVertical ();
		GUILayout.EndHorizontal ();
	}
}
````

Instead, you tell Unity not to serialize the tree directly, and you make a separate field to store the tree in a serialized format, suited to Unity’s serializer. This is shown in Example 2, below.

**Example 2**:  Avoiding Unity's direct serlialization and avoiding performance issues

````

using System.Collections.Generic;
using System;

public class BehaviourWithTree : MonoBehaviour, ISerializationCallbackReceiver {
	// Node class that is used at runtime.
	// This is internal to the BehaviourWithTree class and is not serialized.
	public class Node {
		public string interestingValue = "value";
		public List<Node> children = new List<Node>();
	}
	// Node class that we will use for serialization.
	[Serializable]
	public struct SerializableNode {
		public string interestingValue;
		public int childCount;
		public int indexOfFirstChild;
	}
	// The root node used for runtime tree representation. Not serialized.
	Node root = new Node();
	// This is the field we give Unity to serialize.
	public List<SerializableNode> serializedNodes;
	public void OnBeforeSerialize() {
		// Unity is about to read the serializedNodes field's contents.
		// The correct data must now be written into that field "just in time".
		if (serializedNodes == null) serializedNodes = new List<SerializableNode>();
		if (root == null) root = new Node ();
		serializedNodes.Clear();
		AddNodeToSerializedNodes(root);
		// Now Unity is free to serialize this field, and we should get back the expected 
		// data when it is deserialized later.
	}
	void AddNodeToSerializedNodes(Node n) {
		var serializedNode = new SerializableNode () {
			interestingValue = n.interestingValue,
			childCount = n.children.Count,
			indexOfFirstChild = serializedNodes.Count+1
		}
		;
		serializedNodes.Add (serializedNode);
		foreach (var child in n.children)
		AddNodeToSerializedNodes (child);
	}
	public void OnAfterDeserialize() {
		//Unity has just written new data into the serializedNodes field.
		//let's populate our actual runtime data with those new values.
		if (serializedNodes.Count > 0) {
			ReadNodeFromSerializedNodes (0, out root);
		} else
		root = new Node ();
	}
	int ReadNodeFromSerializedNodes(int index, out Node node) {
		var serializedNode = serializedNodes [index];
		// Transfer the deserialized data into the internal Node class
		Node newNode = new Node() {
			interestingValue = serializedNode.interestingValue,
			children = new List<Node> ()
		}
		;
		// The tree needs to be read in depth-first, since that's how we wrote it out.
		for (int i = 0; i != serializedNode.childCount; i++) {
			Node childNode;
			index = ReadNodeFromSerializedNodes (++index, out childNode);
			newNode.children.Add (childNode);
		}
		node = newNode;
		return index;
	}
	// This OnGUI draws out the node tree in the Game View, with buttons to add new nodes as children.
	void OnGUI() {
		if (root != null)
		Display (root);
	}
	void Display(Node node) {
		GUILayout.Label ("Value: ");
		// Allow modification of the node's "interesting value".
		node.interestingValue = GUILayout.TextField(node.interestingValue, GUILayout.Width(200));
		GUILayout.BeginHorizontal ();
		GUILayout.Space (20);
		GUILayout.BeginVertical ();
		foreach (var child in node.children)
		Display (child);
		if (GUILayout.Button ("Add child"))
		node.children.Add (new Node ());
		GUILayout.EndVertical ();
		GUILayout.EndHorizontal ();
	}
}

````
<br/><br/>

----

<span class="page-edit">• 2017-05-15  <!-- include IncludeTextNewPageYesEdit --></span><br/>
