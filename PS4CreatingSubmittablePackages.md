PS4 Creating submittable packages
=====

Here are some steps to follow to create packages. 
Packages can be installed on PlayStation4 testkits, or devkits and tested in Release check mode. There are also required to be used for submission to Sony for final testing and mastering. 
A similar procedure is used if you are generating a packages for digital download or for installing from disk.

1. Build a non-development build of your game into a folder
1. Open orbis-pub-gen (publishing tools can be accessed from the start menu) and goto ``Command->Project Setting->Package``.
1. Enter your content ID (or the default one from Unity 'PublishingSettings' if you don't yet have one)
1. Enter a passcode (or click the button the generate a random one)
1. Change the storage type to ``Digital Only, Max 50GB``
1. 'OK' that screen and go into the "Image Setting" screen (click on the ``Image0`` filename entry)
1. Drag the contents of your build folder into the empty "filename" section
1. Save the ``.gp4`` configuration data (file->save), and quit the ``imagesetting`` section (``file->close``)
1. Build the package by going to ``Command->Build Image``.