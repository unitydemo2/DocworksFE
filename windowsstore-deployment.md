Windows Store Apps: Deployment
=========================


###How to deploy Windows Store Application



* Go to Build Settings, choose SDK version and build your project to a folder
* Visual Studio solution will be generated


* Running on **local machine**:
    * Make sure, that selected solution platform is x86 and **Debug target** is set to **"Local machine"**
    * Press F5 or go to **Debug** -&gt; **Start debugging**


* Running on **remote machine (handheld device)**:
    * First time you'll have to install remote debugging tools (see [http://msdn.microsoft.com/en-us/library/bt727f1t.aspx](http://msdn.microsoft.com/en-us/library/bt727f1t.aspx) for more information) on a remote machine (**Note:** for ARM tablets you'll need ARM remote debugging tools, for ex., rtools_setup_arm.exe)
    * If you are deploying to ARM architecture device, make sure that ARM is selected as **Solution Platform**
    * Start **Visual Studio Remote debugger** on a remote machine
    * Go to Visual Studio **project settings** -&gt; **Debug**
    * Set target device to **"Remote machine"**
    * Find a remote machine in the list and select it
    * Press **F5** or go to **Debug** -&gt; **Start debugging**
    * **Note:** If you cannot connect to a remote machine, make sure that Firewal does not block it


* Running in **simulator**:
    * Set **Debug Target** to **"Simulator"**
    * Press F5 or go to **Debug** -&gt; **Start debugging**
