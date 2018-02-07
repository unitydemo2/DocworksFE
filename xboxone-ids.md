# IDs

Xbox One has a large number of IDs. Many new developers feel somewhat overwhelmed the first time they encounter the full set of IDs they need to keep straight.

## AUMID and PFN

The first two IDs you will be faced with are related to how applications are named on an Xbox One. These are the AUMID and the PFN.  Most of the operations using the XDK tools require one or the other as input.  You can find more information about these IDs in the XDK documentation. 

### AUMID
The **A**pplication **U**ser **M**odel **ID**.  This identifies a single application or executable in your package.  

### PFN
The **P**ackage **F**ull **N**ame.  This identifies the entire grouping of files that you produce and install on the Xbox One.  A PFN can contain multiple AUMIDs, though this won't happen in the normal Unity workflow. 

## Core IDs
While your application has a Unique ID in the form of the AUMID, these are not the IDs that Microsoft uses to identify your title on the store, to Live, and during development.
The most important of the IDs you will need to know about are the following:

![](../uploads/Main/XboxOne_IDsTrifecta.png)

The SandboxID is like an instance of partner net from 360 days, specific to your company. It hosts all your games configurations. This is assigned to you when setting up your service configuration on the Xbox Developers Portal (XDP). You set the console to use a particular sandbox in your console developer settings. This will force your console to reboot.

The Service Configuration ID (SCID) defines a set of services, an event / analytics schema and other configurations specific to this family of titles. Different flavours of your game share a service configuration, this might happen if you have regional SKUs or different title offerings such as an anniversary edition or other special editions.
Your TitleID is a unique SKU specific ID that identifies this game vs other offerings of this game.
These IDs live in your application manifest and can be used when building your application package when submitting your build to Microsoft.

There are a number of other IDs you will encounter. The first you are likely to need to understand include the following:

![](../uploads/Main/XboxOne_IDsOptional.png)

Your title's ProductID, like its SCID, can be shared between multiple flavors of the title. It is primarily used when submitting Downloadable Content but is attached to your title when building your title's package. Downloadable Content, when shipped, indicates that it can be loaded by products with a particular product ID in its Manifest.

Downloadable Content also has the equivalent of a TitleID known as a ContentID.