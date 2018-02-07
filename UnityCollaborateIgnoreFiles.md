# Excluding Assets from publishing to Collaborate

In some cases, you might want to exclude certain Assets in your Project from publishing to the cloud. Collaborate uses a [gitignore](https://help.github.com/articles/ignoring-files/) file to exclude files from publish. To exclude Assets from publish, add them to the provided _.collabignore_ file in the root of your Project folder. This lists the files and folders to exclude during a publish to Collaborate.

To add your own exclude rules to the _.collabignore_ file:

1. Read the [GitIgnore documentation on Git-SCM.com](https://git-scm.com/docs/gitignore).
2. Edit the _.collabignore_ file to add your new rules.
3. Start the Unity Editor (or restart the Editor if it is already running).
4. Publish your _.collabignore_ file changes in Collaborate to share your exclusions with the rest of your team.

**Note**: For local edits to the *.collabignore* file to take effect, you must restart the Unity Editor.

**Note**: If you exclude a file that is already tracked in Collaborate, its existing file history is preserved.

There are Project files and folders that you can never exclude from Collaborate using the *.collabignore* file. These are:

* The *.collabignore* file.
* The [Assets](AssetWorkflow) folder (although you can exclude specific files or folders within the *Assets* folder.)
* The *Project Settings* folder.
* Any *.asset* file inside the *Project Settings* folder.
* *ProjectVersion.txt* within the *Project Settings* folder.

## See also

 [Setting up Unity Collaborate](UnityCollaborateSettingUp)