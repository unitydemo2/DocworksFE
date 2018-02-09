#3D formats

Unity supports importing [Meshes](class-Mesh) from two different types of files:

1. **Exported 3D file formats**, such as .fbx or .obj. You can export files from 3D modeling software in generic formats that can be imported and edited by a wide variety of different software. 
1. **Proprietary 3D or DCC (Digital Content Creation) application files**, such as .max and .blend file formats from [3D Studio Max](http://www.autodesk.co.uk/products/3ds-max/overview) or [Blender](https://www.blender.org/), for example. You can only edit proprietary files in the software that created them. Proprietary files are generally not directly editable by other software without first being converted and imported. An exception to this is [SketchUp](https://www.sketchup.com/) .skp files, which both by SketchUp and Unity can read.

Unity can import and use both types of files, and each come with their own advantages and disadvantages.

Exported 3D files
-----------------

Unity can read [.fbx](HOWTO-exportFBX), .dae ([Collada](https://www.khronos.org/collada/)), .3ds, .dxf, .obj, and .skp files. Refer to your 3D modeling software documentation for information about exporting 3D files.

**Advantages:**

* Instead of importing the whole model into Unity, you can import only the parts of the model you need.
* Exported generic files are often smaller than the proprietary equivalent.
* Using exported generic files encourages a modular approach (for example, using different components for collision types or interactivity).
* You can import these files from software that Unity does not directly support.
* Exported 3D files (.fbx, .obj) can be reimported into 3D modeling software after exporting, to ensure that all of the information has been exported correctly.

**Disadvantages:**

* Models must be re-exported manually if changes are made to the original file.
* Extra care must be taken to keep track of versions between the source file and the files imported into Unity.

Proprietary 3D application files
--------------------------------


Unity can import proprietary files from the following DCC software: **Max**, **Maya**, **Blender**, **Cinema4D**, **Modo**, **Lightwave** & **Cheetah3D**. Files imported this way are converted into .fbx files by Unity during the import process.

**Advantages:**

* Updates made to the original model are automatically imported into Unity.
* This is initially simple - but it can become more complex later in development.

**Disadvantages:**

* A licensed copy of the software used must be installed on all machines using the Unity project.
* Software versions should be the same on each machine using the Unity project. Using a different software version can cause errors or unexpected behavior when importing 3D models.
* Files can become bloated with unnecessary data.
* Big files can slow down Unity project imports or Asset re-imports, because you have to run the DCC software you use as a background process when you import the model into Unity.
* Unity exports proprietary files to .fbx internally, during the import process. This makes it difficult to verify the .fbx data and troubleshoot problems.

**Note**: Assets saved as .ma, .mb, .max, .c4d, or .blend files fail to import unless you have the corresponding DCC software installed in your computer. This means that everybody working on your Unity project must have the correct software installed. For  example, if you use [Maya](http://www.autodesk.com/education/free-software/maya) to create *ExampleModel.mb* and copy it into your project, anyone else opening that project also needs to have Maya installed on their computer. 
