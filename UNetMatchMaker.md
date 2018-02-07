
Matchmaker
===========

The multiplayer networking feature includes services for players to play with each other over the internet without needing a public IP address. Users can create games, get lists of active games; and join and leave games. When playing over the internet, network traffic goes through a relay server hosted by Unity in the cloud instead of directly between the clients. This avoids problems with firewalls and NATs, allowing play from almost anywhere.

Matchmaking functionality can be utilized with a special script [NetworkMatch](ScriptRef:Networking.Match.NetworkMatch.html), in the UnityEngine.Networking.Match namespace. The ability to use the relay server is built into the LLAPI but the matchmaker makes it easier to use. To use it, derive a  script from NetworkMatch and attach it to a manager object. Below is an example of creating a match, listing matches, and joining a match.

*(note, the terms "match", "game", and "room" are used interchangeably to mean an individual instance of the multiuser game running on the server)*

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

This script sets up the matchmaker to point to the public unity matchmaker server. It calls the base class functions for creating, listing, and joining matches. [CreateMatch](ScriptRef:Networking.Match.NetworkMatch.CreateMatch.html) to create a match, [JoinMatch](ScriptRef:Networking.Match.NetworkMatch.JoinMatch.html) to join a match, and [ListMatches](ScriptRef:Networking.Match.NetworkMatch.ListMatches.html) for listing matches registered on the match maker server. Internally, NetworkMatch uses web services to establish a match and the given callback function is invoked when the process is complete, like OnMatchCreate for match creation.

Populating the singleton NetworkMatch.matchSingleton tells the system to use the relay server instead of a direct connection when connecting to the game. So later, when the client actually connects to the game, it will automatically use the right relay server for the match that was chosen.