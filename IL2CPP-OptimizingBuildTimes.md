## Optimizing IL2CPP build times

Project build times can be much longer when building a project with [IL2CPP](IL2CPP). However, there are several ways to reduce the build time significantly:

**Use incremental building**

When using incremental building, the C++ compiler only recompiles files that have changed since the last build. To use incremental building, build your project to a previous build location (without deleting the target directory).

**Exclude project and target build folders from anti-malware software scans**

You can improve build times by disabling anti-malware software before building your project. (Testing by Unity Technologies found that build times decreased by 50 – 66% after disabling Windows Defender on a fresh Windows 10 installation.)

**Store your project and target build folder on a Solid State Drive (SSD)** 

Solid State Drives (SSDs) have faster read/write speed, when compared to traditional Hard Disk Drives (HDD). Converting IL code to C++ and compiling it involves a large number of read/write operations. A faster storage device speeds up this process.