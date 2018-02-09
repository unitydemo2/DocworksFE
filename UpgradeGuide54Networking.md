#5.4 Networking API Changes

In Unity 5.4 we made a number of changes to the matchmaking API. Our intent was to simplify and clean up the API.

If you used the matchmaking API in an earlier version of Unity, you will need to check and update the classes and functions listed below.

__MatchDesc__ has been renamed to __MatchInfoSnapshot__. 

All request and response classes are removed, so there are no longer any overloaded functions in NetworkMatch. Instead we updated the parameter list of all functions to accommodate the loss of the missing classes and we updated the 2 delegates. 



###Setting up

````
using UnityEngine;
using UnityEngine.Networking;
using UnityEngine.Networking.Match;
NetworkMatch matchMaker;
void Awake()
{
    matchMaker = gameObject.AddComponent<NetworkMatch>();
}
````

### CreateMatch (Before 5.4)

````
CreateMatchRequest create = new CreateMatchRequest();
...
matchMaker.CreateMatch(create, OnMatchCreate);
````

Or

````
matchMaker.CreateMatch("roomName", 4, true, "", OnMatchCreate);
````

Is now:

````
matchMaker.CreateMatch("roomName", 4, true, "", "", "", 0, 0, OnMatchCreate);
````


###CreateMatch Callback (Before 5.4)

````
public void OnMatchCreate(CreateMatchResponse matchResponse)
{
    ...
}
````

Is now:

````
public void OnMatchCreate(bool success, string extendedInfo, MatchInfo matchInfo)
{
    ...
}
````

###ListMatches (Before 5.4)

````
ListMatchRequest list = new ListMatchRequest();

matchMaker.ListMatches(list, OnMatchList);
````

Or

````
matchMaker.ListMatches(0, 10, "", OnMatchList);
````

Is now:

````
matchMaker.ListMatches(0, 10, "", true, 0, 0, OnMatchList);
````

###ListMatches Callback (Before 5.4)

````
public void OnMatchList(ListMatchResponse matchListResponse)
{
    ...
}
````

Is now:

````
public void OnMatchList(bool success, string extendedInfo, List<MatchInfoSnapshot> matches)
{
    ...
}
````


###JoinMatch (Before 5.4)

````
JoinMatchRequest join = new JoinMatchRequest();

matchMaker.JoinMatch(join, OnMatchJoined);
````

Or

````
matchMaker.JoinMatch(match.networkId, "", OnMatchJoined);
````

Is now:

````
matchMaker.JoinMatch(networkId, "" , "", "", 0, 0, OnMatchJoined);
````

###JoinMatch Callback (Before 5.4)

````
public void OnMatchJoined(JoinMatchResponse matchJoin)
{
    ...
}
````

Is now:

````
public void OnMatchJoined(bool success, string extendedInfo, MatchInfo matchInfo)
{
    ...
}
````

###DestroyMatch (Before 5.4)

````
DestroyMatchRequest destroy = DestroyMatchRequest();

matchMaker.DestroyMatch(destroy, OnMatchDestroy);
````

Or

````
matchMaker.DestroyMatch(netId, OnDestroy);
````

Is now:

````
matchMaker.DestroyMatch(netId, 0, OnMatchDestroy);
````

###DestroyMatch Callback  (Before 5.4)

````
public void OnMatchDestroy(BasicResponse response)
{
    ...
}
````

Is now:

````
public void OnMatchDestroy(bool success, string extendedInfo)
{
    ...
}
````

###DropConnection (Before 5.4)

````
DropConnectionRequest drop = DropConnectionRequest();

matchMaker.DropConnection(drop, OnMatchDropConnection);
````

Or

````
matchMaker.DropConnection(netId, nodeId, OnMatchDropConnection);
````

Is now: 

````
matchMaker.DropConnection(netId, nodeId, 0, OnMatchDropConnection);
````

###DropConnection Callback (Before 5.4)

````
public void OnMatchDropConnection(BasicResponse response)
{
    ...
}
````

Is now:

````
public void OnMatchDropConnection(bool success, string extendedInfo)
{
    ...
}
````
