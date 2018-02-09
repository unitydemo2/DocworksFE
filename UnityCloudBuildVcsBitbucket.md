# Using Bitbucket with Unity Cloud Build

Unity Cloud Build can connect to Git and Mercurial repositories hosted on Bitbucket ([bitbucket.org](https://bitbucket.org)).

##Using public Git repositories on Bitbucket

Unity Cloud Build can automatically connect to public repositories on Bitbucket. Copy and paste in the repository’s URL when you set up a project in Cloud Build.

##Using private Git repositories on Bitbucket

If your Bitbucket repository is private, find the SSH key provided by Unity during the project’s setup for Cloud Build, and follow the instructions below to add it to your Bitbucket account.

![](../uploads/Main/UnityCloudBuild-SSHBitbucket.png)


1. Log in to your Bitbucket account on [bitbucket.org](https://bitbucket.org)

2. Open the user menu and click __Manage Account__

3. Choose __SSH Keys__ from the left column menu

4. Click __Add Key__, and give it a label (such as "Unity Cloud Build")

5. Paste the Unity Cloud Build SSH key into the __Bitbucket Key__ field

6. Click __Add Key__ 

##Using Mercurial repositories on Bitbucket

See documentation on [Using Mercurial with Unity Cloud Build](UnityCloudBuildVcsMercurial) for details.