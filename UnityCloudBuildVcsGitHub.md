# Using GitHub with Unity Cloud Build

Unity Cloud Build can connect to Git and Git Large File Storage (LFS) repositories hosted on GitHub ([github.com](https://github.com)). When connecting to GitHub, Unity Cloud Build automatically detects whether your repository is public or private.

##Using public GitHub repositories

Unity Cloud Build can automatically connect to public repositories on GitHub. Paste in the repository’s URL when setting up a project in Cloud Build.

##Using private GitHub repositories

If your GitHub repository is private, find the SSH key provided by Unity during the project’s setup for Cloud Build, and follow the instructions below to add it to your GitHub account.


![](../uploads/Main/UnityCloudBuild-SSHGitHub.png)

1. Log in to your GitHub account

2. Click on __Account Settings__ (the button depicting a screwdriver and spanner) 

3. Choose __SSH Keys__ from the menu

4. Click __Add SSH Key__ and give it a name (such as __Unity Cloud Build__)

5. Paste the Unity Cloud Build SSH key into the __GitHub Key__ field

6. Click __Add Key__
