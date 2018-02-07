#Integration using the HUD

To integrate Unity Multiplayer Services using the __NetworkManagerHUD__, follow these steps:

1. Create an empty GameObject in your Scene.

2. Add the components __NetworkManager__ and __NetworkManagerHUD__ to the empty GameObject. Rename this object to "Network Manager" so that you know what it is.

    ![](../uploads/Main/UnityMultiplayerHUDComponents.png)

3. Create a prefab to represent your player. Players connected to your game will each control an instance of this prefab.

4. Add the __NetworkIdentity__ and __NetworkTransform__ component to your player prefab. The __NetworkTransform__ component synchronizes the player GameObject's movement. If you're making a game where players don't move, you don't need this.

    ![](../uploads/Main/UnityMultiplayerNetworkPlayerPrefab.png)

5. Add your player prefab to the the __Network Manager__'s __Player Prefab__ property in the inspector.

    ![](../uploads/Main/UnityMultiplayerNetworkManagerPlayerPrefabSlot.png)

6. Build and run your project. The Network Manager HUD shows an in-game menu. Click __Enable Match Maker__.

    ![](../uploads/Main/UnityMultiplayerHUDEnableMM.png)

7. Choose a room name and click __Create Internet Match__ on the hosting application.

    ![](../uploads/Main/UnityMultiplayerHUDCreateMatch.png)

8. Run more instances of your project, and click __Find Internet Match__ on these clients. Your room name should now appear.

    ![](../uploads/Main/UnityMultiplayerHUDFindMatch.png)

9. Click __Join Match__. Your players should now be connected to the same match.

    ![](../uploads/Main/UnityMultiplayerHUDJoinMatch.png)







