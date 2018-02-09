Plastic SCM Integration
=======================

For more information on Plastic SCM you can visit their [website](http://www.plasticscm.com).

Setting up Plastic SCM
----------------------


Refer to the [Plastic SCM documentation](http://www.plasticscm.com/infocenter.aspx) if you encounter any problems with the set up process on the [version control page](Versioncontrolintegration).

Checking Files Out with Plastic SCM
-----------------------------------

Plastic SCM automatically checks files out if they have been modified, this makes it more convenient for you. The only files that require specific checking out instructions are Project Settings files otherwise you can't change them.

Resolving Conflicts and Merging with Plastic SCM
------------------------------------------------


A merge is likely to happen when you have edited something in your project locally which has also been edited remotely (a conflict). This means you will need to review the changes before the merge can be performed. If Unity recognises that a merge must be completed before changes can be submitted then you will be prompted by Unity to complete the merge, this will take you to the Plastic SCM client. 

If incoming changes conflict with local changes then a question mark icon will appear on conflicting files in the incoming changes window. Here is a quick guide to resolving conflicts and merging with Plastic SCM:

* In the Version Control window click on the'Apply all incoming changes' button, this will automatically take you to the Plastic SCM GUI client.
* Within the client window you will be able to click 'Explain merge' for a more visual understanding of the changes. Now click 'Process all merges' and another window will display. 
* Here you will be shown the individual conflicts and given the option to choose what changes you want to keep or discard.
* Once you have solved the conflicts click on save and exit, this will have completed the merge operation.
* You now have to push the changes like normal through Unity's version control window.

Locking Files with Plastic SCM
------------------------------

In order to lock files using Plastic SCM there are a few steps to follow:

* The first thing you must do is create a lock.conf file and make sure it is placed within your server directory. You can find your server directory from "../PlasticSCM/server".

* In your lock.conf file you must specify the repository you are working on and the server that will complete the lock checks. Here is an example:

````
rep:default lockserver:localhost:8087
*.unity
*.unity.meta
````
In this case all .unity and .unity.meta files are going to be locked for checkout on repository 'default'.

* You may want to restart your server at this point, you can do this by opening a terminal/command line window and locating the server directory. Once in the directory you can restart the server by typing:

````
./plasticsd restart
````
* Now go back to Unity and check out a file that you expect to be locked, then go back to the terminal/command line and type:

````
cm listlocks
````
If the steps have been followed correctly the terminal/command line window should now display a list of locked files. You can also test if this has worked by trying to check out the same file using a different user, an error will appear in Unity's console saying the file is already checked out by another user.

For more information you can visit the [Plastic SCM lock file]( http://plasticscm.com/documentation/administration/plastic-scm-version-control-administrator-guide.shtml#C6_Checkout_Lock) documentation.

Distributed and offline work with Plastic SCM
---------------------------------------------

To find more about working in distributed mode (DVCS) and offline with Plastic SCM check the [Distributed Version Control Guide](http://plasticscm.com/documentation/distributed/plastic-scm-version-control-distributed-guide.shtml).
