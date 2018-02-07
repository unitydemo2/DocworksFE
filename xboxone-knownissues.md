Known Issues
============


Current Build
-------------

###Certification Submission Considerations
* Unity does not produce 100% deterministic builds.  If you build your project and then build again without making any changes to the project or any of the content, there can be a large difference between these two builds when compared byte for byte.  To avoid large patches for title updates, you should perform a clean build every time you make a build for submission.  Please see the **Proper Settings For Certification Submission** section in [Packaging](xboxone-packaging) for more details. 

###Editor
* Product Name & Company Name cannot contain leading or trailing spaces.
* Known issues related to Pull Deployment:
    * The Pull deploy method will explicitly terminate your game before deploying.  This is done because auditioning the files often fails while the game is running
    * Changing the output directory will cause pull deploy to fail.
        * Workaround: shutdown existing pull sessions by running "xbdeploy shutdown" before building with the new output directory
    * xbrdevicesrv.exe remains running after Unity.exe is shutdown.  This is beneficial because you can continue to use the same pull session for your game even after closing the Unity Editor, which will speed up iteration time.  However, be aware that this program continues running, but it can be stopped by running "xbdeploy shutdown" if needed
    * Pull deployment may not work if you use a custom appxmainfest.xml file, see following section for details
        * If you set the Package Identity Name to a string other than the one used in the auto-generated manifest, pull deployment and the Get Log button will not work for your game
        * Changes to the manifest are not reflected immediately if you are using Pull deploy.  You have to shutdown the current pull deploy session (run "xbdeploy shutdown") in order for changes to take effect

###Installation
* The VC2010 Redistributable package is needed to build XboxOne projects.

###Networking
* Unity networking does not work properly on exclusive IPv6 networks.  This prevents the Unity Profiler and Mono Develop from communicating with your game.

###Profiler
* On some machines the profiler may not see the XB1 process.  This is due to a complication of IPV4/IPV6 networking and is being looked into.
* The profiler is disabled for several threads at the moment because it chews up a lot of memory and eventually runs out.  If you're a source customer, you can enable the profiler on specific threads by calling profiler_initialize_thread on those threads.  Just be aware that it will eventually fall over with OOM because the profiler keeps all samples.

###Script Debugging / Mono
* MonoDevelop does not work with IPv6 addresses.  If you have a network that uses IPv6 exclusively, you will not be able to debug scripts.
