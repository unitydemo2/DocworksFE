Universal Windows Platform: Deployment
=========================


###How to deploy Universal Windows Application



* Go to Build Settings and build your project to a folder
* Visual Studio solution will be generated


* Running on **local machine**:
    * Make sure, that selected solution platform is x86 or x64 and **Debug target** is set to **"Local machine"**
    * Press F5 or go to **Debug** -&gt; **Start debugging**


* Running on **remote machine**:
    * If you are deploying to ARM architecture device, make sure that ARM is selected as **Solution Platform**
    * Start **Visual Studio Remote debugger** on a remote machine
    * Go to Visual Studio **project settings** -&gt; **Debug**
    * Set target device to **"Remote machine"**
    * Find a remote machine in the list and select "Universal" authentication method
    * Press **F5** or go to **Debug** -&gt; **Start debugging**
    * **Note:** If you cannot connect to a remote machine, make sure that Firewall does not block it


* Running in **simulator**:
    * Set **Debug Target** to **"Simulator"**
    * Press F5 or go to **Debug** -&gt; **Start debugging**

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>