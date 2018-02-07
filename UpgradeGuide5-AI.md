##AI in Unity 5.0

These are notes to be aware of when upgrading projects from Unity 4 to Unity 5, if your project uses the AI/Navmesh features.

- Navmesh contour may look different due to changed partitioning - in cases with narrow corridor/doorways or similar - this can lead to a difference in connectivity. Solve the issue by tweaking the voxel size for navmesh building.
     
- Setting the destination for a NavMeshAgent doesn't resume the agent after calling 'Stop' - call 'Resume' explicitly to resume the agent.
 
- NavMeshAgent.updatePosition: When updatePosition is false and the agent transform is moved the agent position doesn't change. Previously the agent position would be reset to the  transform position - constrained to the nearby navmesh.

- NavMeshObstacle component: The default shape for newly created NavMeshObstacle components is a box. The selected shape (box or capsule) now applies to both carving and avoidance.

- Navmesh built with earlier versions of Unity is not supported. You must rebuild with Unity 5. You can use the following script as an example how to rebuild NavMesh data for all of you scenes.

###Rebake script example

````
#if UNITY_EDITOR
using System.Collections.Generic;
using System.Collections;
using System.IO;
using UnityEditor;
using UnityEngine;
using UnityEngine.AI;
public class RebakeAllScenesEditorScript
{
	[MenuItem ("Upgrade helper/Bake All Scenes")]
	public static void Bake()
	{
		List<string> sceneNames = SearchFiles (Application.dataPath, "*.unity");
		foreach (string f in sceneNames)
		{
			EditorApplication.OpenScene(f);
 
			// Rebake navmesh data
			NavMeshBuilder.BuildNavMesh ();
 
			EditorApplication.SaveScene ();
		}
	}
	static List<string> SearchFiles(string dir, string pattern)
	{
		List <string> sceneNames = new List <string>();
		foreach (string f in Directory.GetFiles(dir, pattern, SearchOption.AllDirectories))
		{
			sceneNames.Add (f);
		}
		return sceneNames;
	}
}
#endif
````
