# Ignore files

Your Unity Project is a collection of files and folders. To exclude files and folders in your Project from [Collaborate](UnityCollaborate), edit the _.collabignore_ file in the Project folder on your computer. If you have [set up your Project in Collaborate](UnityCollaborateSettingUp), this file is in the root of the Project folder, and lists the files and folders excluded by default in Collaborate.

To add your own exclude rules to _.collabignore_:

1. Familiarise yourself with the [GitIgnore documentation on Git-SCM.com](https://git-scm.com/docs/gitignore).

2. Edit the _.collabignore_ file to add your new rules.

3. Start the Unity Editor (or restart the Editor if it is already running). Unity now takes note of the exclusions you added to the _.collabignore_ file.

4. Publish your _.collabignore_ changes in Collaborate to share your exclusions with the rest of your team.

## Notes

* For local edits to the _.collabignore_ file to take effect, you need to restart the Unity Editor.

* If you exclude a file already tracked in Collaborate, its existing file history is erased.

There are certain Project files and directories that you can never exclude from Collaborate using _.collabignore_. These are:

* The _.collabignore_ file itself

* The [_Assets_](AssetWorkflow) folder (although you can exclude specific files or folders within the _Assets_ folder)

* The _Project Settings_ folder

* Any _.asset_ file inside the _Project Settings_ folder

* _ProjectVersion.txt_ within the *Project Settings* folder
