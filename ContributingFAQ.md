FAQ
===

Here, we've compiled some frequently asked questions:

**Q: Why Bitbucket instead of GitHub or self-hosted?**

**A:** At Unity, we are fans of both Bitbucket and GitHub. We also self-host and use a third-party hosting solution called [Kallithea](https://kallithea-scm.org/) internally. Ultimately, we chose Bitbucket for our open-source components because:

1. It allows us to let someone else worry about hosting (which lets us focus on what we're good at)
1. It supports both Mercurial and Git instead of only Git (we are [heavy users of Mercurial internally](http://blogs.unity3d.com/2011/10/21/build-engineering-and-infrastructure-how-unity-does-it/), but also have some Git-based forks of open-source tools we use, so being able to store everything in one place makes more sense)

**Q: What license are Unity's open-source components released under?**

**A:** Unity's open-source components are generally released under an [MIT/X11](http://opensource.org/licenses/MIT) license. Some projects, like Unity Test Tools, use 3rd-party components that are released under a different license. You can see the license information for each project by looking at the LICENSE file in the top-level of the source directory. Information about third-party tools (if any) that are used in the project are described in an __acknowlegements.markdown__ file.

**Q: Will Unity accept patches? What about licensing?**

**A:** We will absolutely accept patches. The type of patches we will accept depend on the project because different components are in different stages of development by the Unity devleopers. Bug fixes are great candidates for patches. As for new features or large refactorings, it will depend largely on the system in question.

You should be aware that we will only accept contributions that are licensed under an MIT/X11 license. We will also assume the MIT/X11 license applies to the changes in your pull request unless otherwise stated.

**Q: What coding standards does Unity use? How do I make sure my pull request isn't rejected due to bad formatting changes?**

**A:** The best rule of thumb is to make sure to follow the formatting and conventions that already exist in the code you are modifying. Most of the repositories use a coding standard that is similar to Microsoft's C#.