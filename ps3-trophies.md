#Playstation3: Trophies

##Usage

Unity allows you to use the Trophy System part of the PS3 by means of the NPToolkit class, which has now replaced the [PS3TrophyUtility](ScriptRef:PS3TrophyUtility.html) class. As such any projects still using the old system will no longer have functionality for trophies, although they will still build and run. The PS3 sample package "Trophy" available within the release notes shows how to save and load trophies to/from the PS3.

Here is a table of nearest equivalent functions in the new NP system, compared to the old one:

|**_PS3TrophyUtility_** |**_NP Toolkit_** |
|:---|:---|
|GetTrophyCount                  |Sony.NP.Trophies.GameInfo.numTrophies |
|GetTrophyDescription(trophyId)  |Sony.NP.Trophies.TrophyDetails[trophyId].description |
|GetTrophyName(trophyId)         |Sony.NP.Trophies.TrophyDetails[trophyId].name |
|GetTrophyUnlockState(trophyId)  |Sony.NP.Trophies.TrophyData[trophyId].unlocked |
|HasCompleted                    |Sony.NP.Trophies.TrophiesAreAvailable |
|UnlockTrophy(trophyId)          |Sony.NP.Trophies.AwardTrophy(trophyId) |

###1. Initializing the Toolkit

````
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {
    void Start(){
        // Register a callback for completion of NP initialization.
        Sony.NP.Main.OnNPInitialized += OnNPInitialized;
        
        // Initialize the NP Toolkit.
        Sony.NP.Main.Initialize(Sony.NP.Main.kNpToolkitCreate_CacheTrophyIcons);
        
    	// NP event handlers for trophies
    	Sony.NP.Trophies.OnGotGameInfo += OnTrophyGotGameInfo;
    	Sony.NP.Trophies.OnGotTrophyInfo += OnTrophyGotTrophyInfo;
    	Sony.NP.Trophies.OnAwardedTrophy += OnSomeEvent;
    	Sony.NP.Trophies.OnAwardTrophyFailed += OnSomeEvent;
    	Sony.NP.Trophies.OnAlreadyAwardedTrophy += OnSomeEvent;
    	Sony.NP.Trophies.OnUnlockedPlatinum += OnSomeEvent;
    }
    
    void Update(){
        // The main update loop that keeps the messaging pumping and event handling working
        Sony.NP.Main.Update();
    }
    
    void OnNPInitialized(Sony.NP.Messages.PluginMessage msg){
    	// NP has been fully initialized so it's now safe to sign in.
    	Sony.NP.User.SignIn();
    }
    
    void OnSomeEvent(Sony.NP.Messages.PluginMessage msg){
		Debug.Log("Event: " + msg.type);

		// Get the info for the trophies to reflect any changes that may have occurred
		UpdateTrophies();
	}
}

````

The Toolkit will require the use of event handlers for callbacks on most functions. Through these you will be able to act upon the kit when it's ready, rather than checking for it to be ready yourself.  Please note that in order for the NPToolkit to process messages and events, you will need to regularly call on ``Sony.NP.Main.Update()`` (in the example above, we do this in Update).

###2. Retrieving the Current Trophies
Extending the example above, we can now attempt to retrieve Trophies from the Toolkit. Once the system receives a callback stating that we've received our Game Info, we know that the toolkit is ready. Then we simply need to request Trophy Info and await for the event handler we set up previously.

````
void UpdateTrophies()
{
	// Get the latest trophy info if we're signed in and aren't already requesting them
	if(Sony.NP.User.IsSignedIn && Sony.NP.Trophies.TrophiesAreAvailable && !Sony.NP.Trophies.RequestTrophyInfoIsBusy())
	{
		Sony.NP.Trophies.RequestTrophyInfo();
	}
}

void OnTrophyGotGameInfo(Sony.NP.Messages.PluginMessage msg)
{
	/* This is the game info, within this we have all the information for the game
	 * such as the title, number of trophies, and number of trophies within each
	 * grade (bronze, silver, gold, platinum) */
	gameInfo = Sony.NP.Trophies.GetCachedGameInfo();

	// Get the info for the trophies
	UpdateTrophies();
}

void OnTrophyGotTrophyInfo(Sony.NP.Messages.PluginMessage msg)
{
	/* These are the trophies themselves. TrophyDetails contains the grade, name,
	 * description, ID and hidden state for each Trophy. TrophyData contains the
	 * icon information and unlocked state for each of the trophies. */
	trophyDetails = Sony.NP.Trophies.GetCachedTrophyDetails();
	trophyData = Sony.NP.Trophies.GetCachedTrophyData();
}

````

Note that whenever there has been a change to the current list of trophies such as when a trophy is awarded (see below) we will need to update the list of trophies again.

!!!3. Awarding/Unlocking Trophies
After we've initialized and retrieved the trophies, we can then unlock them. Extending the above example:

````
void UnlockTrophy(int trophyId)
{
	if(!trophyData[trophyId].unlocked)
	{
		// Award a trophy if we're signed in and have all our trophies available
		if(Sony.NP.User.IsSignedIn && Sony.NP.Trophies.TrophiesAreAvailable)
		{
			Sony.NP.Trophies.AwardTrophy(trophyId);
		}
	}
}

````

Note that attempting to award a trophy that is already unlocked will display an error message, so it is important to check if it has already been awarded in the list we retrieved previously.

Once you have verified the locked state of the trophy you are trying to award, you can then proceed to unlock it. At this point you should check if the NP User is signed in and that the trophies system is available, otherwise unlocking will fail.

###4. Displaying Trophies
It is possible to get the details of each specific Trophy from the data we retrieved previously. Extending the example again:

````
void OnGUI(){
	GUILayout.BeginHorizontal();
    
	if(trophyDetails != null)
	{
		for(int i=0; i<gameInfo.numTrophies; i++)
		{
			GUILayout.BeginVertical();
            
			GUILayout.Label("(" + trophyDetails[i].trophyId + ")");
			GUILayout.Label("Name: " + trophyDetails[i].name);
			GUILayout.Label("Desc: " + trophyDetails[i].description);
			GUILayout.Label("Unlocked : " + trophyData[i].unlocked);
            
			GUILayout.EndVertical();
		}
	}
    
	GUILayout.EndHorizontal();
}

````

One advantage of the new NP Toolkit over the old system is the ability to display icons for trophies. Note however that `hasIcon` will always return false if the trophy is currently locked. Add the following in to your OnTrophyGotTrophyInfo function:

````
// Store the trophy icons now so we're not creating them every frame in OnGUI!
trophyIcons = new Texture[gameInfo.numTrophies];
for(int i=0; i<gameInfo.numTrophies; i++)
{
	if(trophyData[i].hasIcon)
		trophyIcons[i] = trophyData[i].icon;
}
````

And then add the following to your OnGUI display of trophies:

````
if(trophyData[i].hasIcon)
	GUILayout.Box(trophyIcons[i]);
````



