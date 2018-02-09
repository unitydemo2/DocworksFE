Deploying Projects
======================
[Build Settings]: wiiu-buildsettings.md

The build procedure is the same as with all the other platforms. Open [Build Settings](wiiu-buildsettings), configure your desired build
and press *Build* or *Build and Run*. Once the building process is complete a folder will open with several **batch** files in it.

1. *run.cmd* - run the application.
2. *runDbg.cmd* - run the application with MULTI debugger attached.
3. *stop.cmd* - stop the running application.
4. *createMaster.cmd* - create a master build package (wumad) or a downloadable package.  



































You need to be sure that in Build Settings, WiiU Platform is selected.

Then you need to click Build or Build and Run. If you use "Build", Unity will generate all the necessary files and 
you will find Run.cmd and Stop.cmd. To run just open **Run.cmd**.

