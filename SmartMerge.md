#Smart Merge

Unity incorporates a tool called **UnityYAMLMerge** that can merge scene and prefab files in a semantically correct way. The tool can be accessed from the command line and is also available to third party version control software.

##Setting Up Smart Merging in Unity

In the __Editor Settings__ (menu: __Edit &gt; Project Settings &gt; Editor__), you have the option to select a third party version control tool (Perforce or PlasticSCM, for example). When one of these tools is enabled, you will see a _Smart Merge_ menu under the _Version Control_ heading. The menu has four options:

* **Off**: use only the default merge tool set in the preferences with no smart merging.
* **Premerge**: enable smart merging, accept clean merges. Unclean merges will create premerged versions of base, theirs and mine versions of the file. Then, use these with the default merge tool. 
* **Ask**: enable smart merging but when a conflict occurs, show a dialog to let the user resolve it (this is the default setting).


##Setting up UnityYAMLMerge for Use with Third Party Tools

The UnityYAMLMerge tool is shipped with the Unity editor; assuming Unity is installed in the standard location, the path to UnityYAMLMerge will be:

````
C:\Program Files\Unity\Editor\Data\Tools\UnityYAMLMerge.exe

or

C:\Program Files (x86)\Unity\Editor\Data\Tools\UnityYAMLMerge.exe
````

...on Windows and 


````
/Applications/Unity/Unity.app/Contents/Tools/UnityYAMLMerge
````

...on Mac OSX (use the _Show Package Contents_ command from the Finder to access this folder).

UnityYAMLMerge is shipped with a default fallback file (called mergespecfile.txt, also in the Tools folder) that specifies how it should proceed with unresolved conflicts or unknown files. This also allows you to use it as the main merge tool for version control systems (such as git) that don't automatically select merge tools based on file extensions. The most common tools are already listed by default in mergespecfile.txt but you can edit this file to add new tools or change options.

You can run UnityYAMLMerge as a standalone tool from the command line (you can see full usage instructions by running it without any arguments). Set-up instructions for common version control systems are given below.


###P4V
* Go to Preferences &gt; Merge.
* Select _Other application_.
* Click the _Add_ button.
* In the extension field, type `.unity`.
* In the Application field, type the path to the UnityYAMLMerge tool (see above).
* In the Arguments field, type `merge -p %b %1 %2 %r`
* Click Save.

Then, follow the same procedure to add the `.prefab` extension.


###Git
Add the following text to your `.git` or `.gitconfig` file:

````
	[merge]
	tool = unityyamlmerge

	[mergetool "unityyamlmerge"]
	trustExitCode = false
	cmd = '<path to UnityYAMLMerge>' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
````

###Mercurial
Add the following text to your `.hgrc` file:

````
	[merge-patterns]
	**.unity = unityyamlmerge
	**.prefab = unityyamlmerge

	[merge-tools]
	unityyamlmerge.executable = <path to UnityYAMLMerge>
	unityyamlmerge.args = merge -p --force $base $other $local $output
	unityyamlmerge.checkprompt = True
	unityyamlmerge.premerge = False
	unityyamlmerge.binary = False
````


###SVN
Add the following to your `~/.subversion/config` file:

````
	[helpers]
	merge-tool-cmd = <path to UnityYAMLMerge>
````


###TortoiseGit
* Go to Preferences &gt; Diff Viewer &gt; Merge Tool and click the _Advanced_ button. 
* In the popup, type `.unity` in the extension field.
* In the External Program field type:

````
	<path to UnityYAMLMerge> merge -p %base %theirs %mine %merged
````

Then, follow the same procedure to add the `.prefab` extension.


###PlasticSCM
* Go to Preferences &gt; Merge Tools and click the _Add_ button.
* Select _External_ merge tool.
* Select _Use with files that match the following pattern_.
* Add the `.unity` extension.
* Enter the command:

````
	<path to UnityYAMLMerge> merge -p "@basefile" "@sourcefile"  "@destinationfile" "@output"
````

Then, follow the same procedure to add the `.prefab` extension.


###SourceTree
* Go to Tools &gt; Options &gt; Diff.
* Select _Custom_ in the Merge Tool dropdown.
* Type the path to UnityYAMLMerge in the _Merge Command_ text field.
* Type `merge -p $BASE $REMOTE $LOCAL $MERGED` in the _Arguments_ text field.

