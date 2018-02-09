# Using Git with Unity Cloud Build

Unity Cloud Build supports projects hosted in Git repositories ([git-scm.com](https://git-scm.com/])).

**URL syntax**

In order for Unity Cloud Build to connect to your repository, you need to provide the URL to your GIT server. This URL can be in one of several formats (the following are examples using [GitHub](https://github.com) or [bitbucket](https://bitbucket.org)): 

* https://github.com/youraccount/yourrepo

* git://github.com/youraccount/yourrepo.git

* git@bitbucket.org:youraccount/yourrepo.git

Use whichever format is most convenient for you; Unity Cloud Build automatically re-writes the URL into the format it needs.

**Branches**

When you configure your project in Unity Cloud Build, you need to specify which branch to build from. The default branch in most Git repositories is "master", but you can configure a different branch for each build target.

**Project subfolder**

You also need to tell Unity Cloud Build which folder (or "directory") in your project contains your Unity project; specifically the __Assets__ and __ProjectSettings__ folders. Depending on how you've arranged your project files, this might be the root folder in your repository. If it isn't, then you need to provide Unity Cloud Build with the path to those folders. It looks something like: _NewGameProject/Src/UnityProject/_

**Git submodules**

If your project is using private Git submodules, make sure that the URLs present in your .gitmodules file are using the "git@" syntax instead of “https://” or “git://”. 

For example: 

* git@github.com:youraccount/yourrepo.git (for GitHub)


* git@bitbucket.org:youraccount/yourrepo.git (for Bitbucket)

**Common Git hosts**

Two common places to host your Git project’s Unity Cloud Build are:

* [GitHub](UnityCloudBuildVcsGitHub)

* [Bitbucket](UnityCloudBuildVcsBitBucket)
