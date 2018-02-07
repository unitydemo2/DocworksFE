# Timeline overview

Use the __Timeline Editor window__ to create cut-scenes, cinematics, and game-play sequences by visually arranging tracks and clips linked to GameObjects in your scene. 

![A cinematic in the Timeline Editor window. The tracks and clips are saved to the project. The references to GameObjects are saved to the scene.](../uploads/Main/timeline_cinematic_example.png)

For each cut-scene, cinematic, or game-play sequence, the Timeline Editor window saves the following:

* __Timeline Asset__: stores the tracks, clips, and recorded animations without links to the specific GameObjects being animated. The Timeline Asset is saved to the project.

* __Timeline instance__: stores links to the specific GameObjects being animated by the Timeline Asset. These links, referred to as __bindings__, are saved to the scene.

## Timeline Asset

The Timeline Editor window saves track and clip definitions as a __Timeline Asset__. If you record key animations while creating your cinematic, cut-scene, or game-play sequence, the Timeline Editor window saves the recorded animation as children of the Timeline Asset.

![The Timeline Asset saves tracks and clips (red). If your record key animation, the recorded clips are saved as children of the Timeline Asset (blue).](../uploads/Main/timeline_overview_asset.png)

## Timeline instance

Although a Timeline Asset defines the tracks and clips for a cut-scene, cinematic, or game-play sequence, you cannot add a Timeline Asset directly to a scene. To animate GameObjects in your scene with a Timeline Asset, you must create a __Timeline instance__.

The Timeline Editor window provides an automated method of creating a Timeline instance while [creating a Timeline Asset](TimelineWorkflowCreatingAssetInstance).

If you select a GameObject in the scene that has a Playable Director component associated with a Timeline Asset, the bindings appear in the Timeline Editor window and in the Playable Director component (Inspector window).

![The Playable Director component shows the Timeline Asset (blue) with its bound GameObjects (red). The Timeline Editor window shows the same bindings (red) in the Track list.](../uploads/Main/timeline_overview_instance.png)

## Reusing Timeline Assets

Since Timeline Assets and Timeline instances are separate, it is possible to reuse the same Timeline Asset with many Timeline instances.

For example, you can create a Timeline Asset named VictoryTimeline with the animation, music, and particle effects that play when the main game character (Player) is victorious. To reuse the VictoryTimeline Timeline Asset to animate another game character (Enemy) in the same scene, you can create another Timeline instance for the secondary game character.

![The Player GameObject (red) is attached to the VictoryTimeline Timeline Asset](../uploads/Main/timeline_overview_player.png)

![The Enemy GameObject (blue) is also attached to the VictoryTimeline Timeline Asset](../uploads/Main/timeline_overview_enemy.png)

Since the Timeline Asset is being reused, any modification to the Timeline Asset in the Timeline Editor window results in changes to all Timeline instances. 

For example, in the previous example, if you delete the Fireworks Control track in the Timeline Editor window while modifying the Player Timeline instance, the track is removed from the VictoryTimeline Timeline Asset. This also removes the Fireworks control track from all instances of the VictoryTimeline Timeline Asset, including the Enemy Timeline instance.

---


<!--include AnimationAndTimelineWindowsDifference -->

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>
