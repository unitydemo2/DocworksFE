# Using Unity with Perforce Source Control

[Perforce](https://www.perforce.com/) is a version control tool. See documentation on [Version control integration](http://versioncontrolintegration) for more information on what this means for your project. This page details how to implement version control for your project.

Open your project in Unity and go to __Edit__ > __Project Settings __> __Editor__. Under __Version Control__, change __Mode__ to __Perforce__.

Extra fields appear in the Inspector window to allow you to configure Perforce. Complete all fields, then click the __Connect __button to connect to your chosen repository.

![](../uploads/Main/UsingUnityWithPerforce1.png)

| Property| Function |
|:---|:---| 
| __Username__| Your login user name for the Perforce repository you wish to use. If you have signed up for a Perforce Helix account, this should have been emailed to you. Alternatively, you might need to contact your systems administrator. |
| __Password__| Your login password for the Perforce repository you wish to use. If you have signed up for a Perforce Helix account, this should have been emailed to you. Alternatively, you might need to contact your system administrator. |
| __Workspace__| This is your own personal copy of the particular Perforce repository you’re working with. If you don’t know where this is, or you have yet to create your own Workspace, download and run the [Perforce P4V Visual Client](https://www.perforce.com/product/components/perforce-visual-client). See [Creating a Perforce Workspace](#CreateWorkspace), below, for more information. |
| __Server__| In the Perforce P4 Administration Tool, the __Server__ address is in the __Connections__ list. See the red box in image A, below, to find this. If the Connections list is empty, contact your system administrator.
| __Host__| In the [Perforce P4 Administration Tool](https://www.perforce.com/product/components/perforce-administration-tool), go to __Server Info__ > __Host__ to obtain the Host address. This is usually "localhost". See the green box in image A, below, to find this. |
| __Log Level__| __Log Level__ allows you to see more or less logging output from Perforce as it operates. They are ordered from verbose (highest level) to fatal (lowest level). All higher levels includes lower level log messages. The default is __Info__. |
| &nbsp;&nbsp;&nbsp;&nbsp;Verbose| Logs all protocol messages between Unity and the Perforce plugin, and other extra messages regarding the activity of both. Also logs information outlined by __Info__, __Notice__, and __Fatal__. |
| &nbsp;&nbsp;&nbsp;&nbsp;Info| Logs the commands Unity sends to the Perforce server, and their outcome. Also logs information outlined by __Notice__ and __Fatal__. |
| &nbsp;&nbsp;&nbsp;&nbsp;Notice| Logs when something might need attention (for example, if a file the process needs to use is read-only). Also logs information outlined by __Fatal__. |
| &nbsp;&nbsp;&nbsp;&nbsp;Fatal| Only logs when something goes wrong and Unity cannot fulfill the request. |

![__Image A:__ The Perforce P4Admin tool. The __Server__ address is in the red box, and the __Host__ address is in the green box.](../uploads/Main/UsingUnityWithPerforce2.png)

<a name="CreateWorkspace"> </a>

## Creating a Perforce Workspace

To create your own Workspace in Perforce, download and run the [Perforce P4V Visual Client](https://www.perforce.com/product/components/perforce-visual-client) on your computer. Upon startup, a dialog box prompts you to open a connection to your Perforce repository.

![](../uploads/Main/UsingUnityWithPerforce3.png)

Note the __Workspace __identifier, highlighted in red. If this field is blank, click __New…__ to create a new Workspace, or click __Browse...__ to select an existing one, as shown in the image below.

![](../uploads/Main/UsingUnityWithPerforce4.png)