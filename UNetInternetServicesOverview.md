#Internet services

Unity offers Internet matchmaking services which complement the Unity networking system to support your game throughout production and release. This includes a multi-user server service to allow your game to communicate across the internet. It provides users with the ability to create and advertise matches, list available matches, and join matches.

**Note**: WebGl platform doesn't support Unity's matchmaking service. If you try to use this service for WebGL, a `NotImplemented` exception is thrown.

##Setting up the Multiplayer service

Before you can use the Matchmaker or the internet services you need to register the project first. See the Services Window (cloud icon in upper right corner, or go to Window->Unity Services in the application menu) where the Multiplayer panel should appear. In there you'll find a link to the cloud Multiplayer website (you can also visit [https://multiplayer.unity3d.com](https://multiplayer.unity3d.com) directly). Find your project name there and set up the Multiplayer configuration.

Note about Unity 5.1.x: The project ID is set up manually in this version of Unity, you can find the field for it in the Player settings (Edit -> Project Settings -> Player). Visit [https://multiplayer.unity3d.com](https://multiplayer.unity3d.com) and set up your project manually and create a Multiplayer configuration for it. When viewing the configuration you'll be able to see the ID (it's called UPID right now in a 12345678-1234-1234-1234-123456789ABC format).

##Matchmaking service

The multiplayer networking feature includes services for players to play with each other over the internet without needing a public IP address. Users can create games, get lists of active games and join and leave games. When playing over the internet, network traffic goes through a relay server hosted by Unity in the cloud instead of directly between the clients. This avoids problems with firewalls and NATs, allowing players to join from almost anywhere.

Matchmaking functionality can be utilized with a special script [NetworkMatch](ScriptRef:Networking.Match.NetworkMatch.html), in the UnityEngine.Networking.Match namespace. The ability to use the relay server is built into the LLAPI but the matchmaker makes it easier to use. To use it, derive a  script from NetworkMatch and attach it to a manager object. Below is an example of creating a match, listing matches, and joining a match.

````
using UnityEngine;
using UnityEngine.Networking;
using UnityEngine.Networking.Types;
using UnityEngine.Networking.Match;
using System.Collections.Generic;

public class HostGame : MonoBehaviour
{
	List<MatchDesc> matchList = new List<MatchDesc>();
	bool matchCreated;
	NetworkMatch networkMatch;

	void Awake()
	{
		networkMatch = gameObject.AddComponent<NetworkMatch>();
	}

	void OnGUI()
	{
		// You would normally not join a match you created yourself but this is possible here for demonstration purposes.
		if(GUILayout.Button("Create Room"))
		{
			CreateMatchRequest create = new CreateMatchRequest();
			create.name = "NewRoom";
			create.size = 4;
			create.advertise = true;
			create.password = "";

			networkMatch.CreateMatch(create, OnMatchCreate);
		}

		if (GUILayout.Button("List rooms"))
		{
			networkMatch.ListMatches(0, 20, "", OnMatchList);
		}

		if (matchList.Count > 0)
		{
			GUILayout.Label("Current rooms");
		}
		foreach (var match in matchList)
		{
			if (GUILayout.Button(match.name))
			{
				networkMatch.JoinMatch(match.networkId, "", OnMatchJoined);
			}
		}
	}

	public void OnMatchCreate(CreateMatchResponse matchResponse)
	{
		if (matchResponse.success)
		{
			Debug.Log("Create match succeeded");
			matchCreated = true;
			Utility.SetAccessTokenForNetwork(matchResponse.networkId, new NetworkAccessToken(matchResponse.accessTokenString));
			NetworkServer.Listen(new MatchInfo(matchResponse), 9000);
		}
		else
		{
			Debug.LogError ("Create match failed");
		}
	}

	public void OnMatchList(ListMatchResponse matchListResponse)
	{
		if (matchListResponse.success && matchListResponse.matches != null)
		{
			networkMatch.JoinMatch(matchListResponse.matches[0].networkId, "", OnMatchJoined);
		}
	}

	public void OnMatchJoined(JoinMatchResponse matchJoin)
	{
		if (matchJoin.success)
		{
			Debug.Log("Join match succeeded");
			if (matchCreated)
			{
				Debug.LogWarning("Match already set up, aborting...");
				return;
			}
			Utility.SetAccessTokenForNetwork(matchJoin.networkId, new NetworkAccessToken(matchJoin.accessTokenString));
			NetworkClient myClient = new NetworkClient();
			myClient.RegisterHandler(MsgType.Connect, OnConnected);
			myClient.Connect(new MatchInfo(matchJoin));
		}
		else
		{
			Debug.LogError("Join match failed");
		}
	}

	public void OnConnected(NetworkMessage msg)
	{
		Debug.Log("Connected!");
	}
}
````

This script sets up the matchmaker to point to the public unity matchmaker server. It calls the base class functions for creating, listing, and joining matches. [CreateMatch](ScriptRef:Networking.Match.NetworkMatch.CreateMatch.html) to create a match, [JoinMatch](ScriptRef:Networking.Match.NetworkMatch.JoinMatch.html) to join a match, and [ListMatches](ScriptRef:Networking.Match.NetworkMatch.ListMatches.html) for listing matches registered on the matchmaker server. Internally, NetworkMatch uses web services to establish a match and the given callback function is invoked when the process is complete, like OnMatchCreate for match creation.

To use a relay server instead of a direct connection, you must populate the singleton NetworkMatch.matchSingleton. This tells the system to use the relay server instead of a direct connection when connecting to the game. So later, when the client actually connects to the game, it will automatically use the right relay server for the match that was chosen.

##Relay server

The relay server works closely with the matchmaker server, as mentioned above. The higher level classes handle the relay for you automatically. There is not much extra work for you to do. Here however is an example which shows how you could use the matchmaker and relay server through the lower level transport layer, using the [NetworkTransport](ScriptRef:Networking.NetworkTransport.html) class directly.


````
using UnityEngine;
using UnityEngine.Networking;
using UnityEngine.Networking.Types;
using UnityEngine.Networking.Match;
using System.Collections.Generic;

public class SimpleSetup : MonoBehaviour
{
	// Matchmaker related
	List<MatchDesc> m_MatchList = new List<MatchDesc>();
	bool m_MatchCreated;
	bool m_MatchJoined;
	MatchInfo m_MatchInfo;
	string m_MatchName = "NewRoom";
	NetworkMatch m_NetworkMatch;

	// Connection/communication related
	int m_HostId = -1;
	// On the server there will be multiple connections, on the client this will only contain one ID
	List<int> m_ConnectionIds = new List<int>();
	byte[] m_ReceiveBuffer;
	string m_NetworkMessage = "Hello world";
	string m_LastReceivedMessage = "";
	NetworkWriter m_Writer;
	NetworkReader m_Reader;
	bool m_ConnectionEstablished;

	const int k_ServerPort = 25000;
	const int k_MaxMessageSize = 65535;

	void Awake()
	{
		m_NetworkMatch = gameObject.AddComponent<NetworkMatch>();
	}

	void Start()
	{
		m_ReceiveBuffer = new byte[k_MaxMessageSize];
		m_Writer = new NetworkWriter();
		// While testing with multiple standalone players on one machine this will need to be enabled
		Application.runInBackground = true;
	}

	void OnApplicationQuit()
	{
		NetworkTransport.Shutdown();
	}

	void OnGUI()
	{
		if (string.IsNullOrEmpty(Application.cloudProjectId))
			GUILayout.Label("You must set up the project first. See the Multiplayer tab in the Service Window");
		else
			GUILayout.Label("Cloud Project ID: " + Application.cloudProjectId);

		if (m_MatchJoined)
			GUILayout.Label("Match joined '" + m_MatchName + "' on Matchmaker server");
		else if (m_MatchCreated)
			GUILayout.Label("Match '" + m_MatchName + "' created on Matchmaker server");

		GUILayout.Label("Connection Established: " + m_ConnectionEstablished);

		if (m_MatchCreated || m_MatchJoined)
		{
			GUILayout.Label("Relay Server: " + m_MatchInfo.address + ":" + m_MatchInfo.port);
			GUILayout.Label("NetworkID: " + m_MatchInfo.networkId + " NodeID: " + m_MatchInfo.nodeId);
			GUILayout.BeginHorizontal();
			GUILayout.Label("Outgoing message:");
			m_NetworkMessage = GUILayout.TextField(m_NetworkMessage);
			GUILayout.EndHorizontal();
			GUILayout.Label("Last incoming message: " + m_LastReceivedMessage);

			if (m_ConnectionEstablished && GUILayout.Button("Send message"))
			{
				m_Writer.SeekZero();
				m_Writer.Write(m_NetworkMessage);
				byte error;
				for (int i = 0; i < m_ConnectionIds.Count; ++i)
				{
					NetworkTransport.Send(m_HostId, 
						m_ConnectionIds[i], 0, m_Writer.AsArray(), m_Writer.Position, out error);
					if ((NetworkError)error != NetworkError.Ok)
						Debug.LogError("Failed to send message: " + (NetworkError)error);
				}
			}

			if (GUILayout.Button("Shutdown"))
			{
				m_NetworkMatch.DropConnection(m_MatchInfo.networkId, 
					m_MatchInfo.nodeId, OnConnectionDropped);
			}
		}
		else
		{
			if (GUILayout.Button("Create Room"))
			{
				m_NetworkMatch.CreateMatch(m_MatchName, 4, true, "", OnMatchCreate);
			}

			if (GUILayout.Button("Join first found match"))
			{
				m_NetworkMatch.ListMatches(0, 1, "", (response) => {
					if (response.success && response.matches.Count > 0)
						m_NetworkMatch.JoinMatch (response.matches [0].networkId, "", OnMatchJoined);	
				});
			}
				
			if (GUILayout.Button ("List rooms"))
			{
				m_NetworkMatch.ListMatches (0, 20, "", OnMatchList);
			}

			if (m_MatchList.Count > 0)
			{
				GUILayout.Label ("Current rooms:");
			}
			foreach (var match in m_MatchList) 
			{
				if (GUILayout.Button (match.name))
				{
					m_NetworkMatch.JoinMatch(match.networkId, "", OnMatchJoined);
				}
			}
		}
	}

	public void OnConnectionDropped(BasicResponse callback)
	{
		Debug.Log("Connection has been dropped on matchmaker server");
		NetworkTransport.Shutdown();
		m_HostId = -1;
		m_ConnectionIds.Clear();
		m_MatchInfo = null;
		m_MatchCreated = false;
		m_MatchJoined = false;
		m_ConnectionEstablished = false;
	}

	public void OnMatchCreate(CreateMatchResponse matchResponse)
	{
		if (matchResponse.success)
		{
			Debug.Log("Create match succeeded");
			Utility.SetAccessTokenForNetwork(matchResponse.networkId, 
				new NetworkAccessToken(matchResponse.accessTokenString));

			m_MatchCreated = true;
			m_MatchInfo = new MatchInfo(matchResponse);

			StartServer(matchResponse.address, matchResponse.port, matchResponse.networkId, 
				matchResponse.nodeId);
		}
		else
		{
			Debug.LogError ("Create match failed");
		}
	}

	public void OnMatchList(ListMatchResponse matchListResponse)
	{
		if (matchListResponse.success && matchListResponse.matches != null)
		{
			m_MatchList = matchListResponse.matches;
		}
	}

	// When we've joined a match we connect to the server/host
	public void OnMatchJoined(JoinMatchResponse matchJoin)
	{
		if (matchJoin.success)
		{
			Debug.Log("Join match succeeded");
			Utility.SetAccessTokenForNetwork(matchJoin.networkId, 
				new NetworkAccessToken(matchJoin.accessTokenString));

			m_MatchJoined = true;
			m_MatchInfo = new MatchInfo(matchJoin);

			Debug.Log ("Connecting to Address:" + matchJoin.address + 
				" Port:" + matchJoin.port + 
				" NetworKID: " + matchJoin.networkId + 
				" NodeID: " + matchJoin.nodeId);
			ConnectThroughRelay(matchJoin.address, matchJoin.port, matchJoin.networkId, 
				matchJoin.nodeId);
		}
		else
		{
			Debug.LogError("Join match failed");
		}
	}

	void SetupHost(bool isServer)
	{
		Debug.Log("Initializing network transport");
		NetworkTransport.Init();
		var config = new ConnectionConfig();
		config.AddChannel(QosType.Reliable);
		config.AddChannel(QosType.Unreliable);
		var topology = new HostTopology(config, 4);
		if (isServer)
			m_HostId = NetworkTransport.AddHost(topology, k_ServerPort);
		else
			m_HostId = NetworkTransport.AddHost(topology);
	}

	void StartServer(string relayIp, int relayPort, NetworkID networkId, NodeID nodeId)
	{
		SetupHost(true);

		byte error;
		NetworkTransport.ConnectAsNetworkHost(
			m_HostId, relayIp, relayPort, networkId, Utility.GetSourceID(), nodeId, out error);
	}

	void ConnectThroughRelay(string relayIp, int relayPort, NetworkID networkId, NodeID nodeId)
	{
		SetupHost(false);

		byte error;
		NetworkTransport.ConnectToNetworkPeer(
			m_HostId, relayIp, relayPort, 0, 0, networkId, Utility.GetSourceID(), nodeId, out error);
	}

	void Update()
	{
		if (m_HostId == -1)
			return;

		var networkEvent = NetworkEventType.Nothing;
		int connectionId;
		int channelId;
		int receivedSize;
		byte error;

		// Get events from the relay connection
		networkEvent = NetworkTransport.ReceiveRelayEventFromHost (m_HostId, out error);
		if (networkEvent == NetworkEventType.ConnectEvent)
			Debug.Log ("Relay server connected");
		if (networkEvent == NetworkEventType.DisconnectEvent)
			Debug.Log ("Relay server disconnected");

		do
		{
			// Get events from the server/client game connection
			networkEvent = NetworkTransport.ReceiveFromHost(m_HostId, out connectionId, out channelId, 
				m_ReceiveBuffer, (int)m_ReceiveBuffer.Length, out receivedSize, out error);
			if ((NetworkError)error != NetworkError.Ok)
			{
				Debug.LogError("Error while receiveing network message: " + (NetworkError)error);
			}

			switch (networkEvent)
			{
				case NetworkEventType.ConnectEvent:
				{
					Debug.Log("Connected through relay, ConnectionID:" + connectionId + 
						" ChannelID:" + channelId);
					m_ConnectionEstablished = true;
					m_ConnectionIds.Add(connectionId);
					break;
				}
				case NetworkEventType.DataEvent:
				{
					Debug.Log("Data event, ConnectionID:" + connectionId + 
						" ChannelID: " + channelId +
						" Received Size: " + receivedSize);
					m_Reader = new NetworkReader(m_ReceiveBuffer);
					m_LastReceivedMessage = m_Reader.ReadString();
					break;
				}
				case NetworkEventType.DisconnectEvent:
				{
					Debug.Log("Connection disconnected, ConnectionID:" + connectionId);
					break;
				}
				case NetworkEventType.Nothing:
				break;
			}
		} while (networkEvent != NetworkEventType.Nothing);
	}
}
````