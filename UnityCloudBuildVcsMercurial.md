# Using Mercurial with Unity Cloud Build

Unity Cloud Build requires a username and password to connect to your Mercurial repository (see [www.mercurial-scm.org](https://www.mercurial-scm.org/)). This applies to Mercurial repositories hosted on Bitbucket or elsewhere.

**Username and password**

In your Mercurial server, create a user just for Unity Cloud Build, along with a secure password. If your Mercurial host supports it, make this a read-only user account.

**Branches**

When you configure your project in Unity Cloud Build, you are prompted to specify which branch to build from.

**Project subfolder**

You may need to define which folder contains your Unity project; specifically the __Assets__ and __ProjectSettings__ folders. This is usually the root folder in your repository: If this is the case, you can leave this field blank. However, if your Unity project lives in a subdirectory, you need to enter the path to the __Assets__ and __ProjectSettings__ folders during setup of a build target in Unity Cloud Build. It looks something like: _NewGameProject/Src/UnityProject/_ (please note that this is an example only).