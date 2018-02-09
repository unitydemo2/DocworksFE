Perforce Integration
====================


For more information on Perforce you can visit [www.perforce.com](https://www.perforce.com/downloads/helix).

Setting up Perforce
-------------------


Refer to [perforce documentation](https://www.perforce.com/perforce/doc.current/manuals/p4v/) if you encounter any problems with the setup process on the [version control page](Versioncontrolintegration).

Working Offline with Perforce
-----------------------------


Only use this if you know how to work offline in Perforce without a Sandbox. Refer to the [Perforce documentation](https://www.perforce.com/perforce/doc.current/manuals/p4v/using.offline.html) for further information.


Troubleshooting
---------------


If Unity for some reason cannot commit your changes to Perforce, e.g. if server is down, license issues etc., your changes will be stored in a separate changeset. If the console doesn't list any info about the issue you can use the P4V client for Perforce to submit this changeset to see the exact error message.

Automatic revert of unchanged files on submit
---------------------------------------------


It's possible to configure Perforce to revert unchanged files on submit, which is done in P4V by selecting **Connection->Edit Current Workspace...,** viewing the Advanced tab and setting the value of On submit to **Revert unchanged files**:

![](../uploads/Main/VersionControl_P4V_RevertUnchangedFilesSetting.png)