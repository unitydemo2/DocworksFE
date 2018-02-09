PSM Reporting Bugs
===

This document describes how bugs are reported, both using the built-in Unity Bug Reporter and the PS Vita on-device crash reporter.

## The Unity Bug Reporter

The Unity editor has a simple mechanism for reporting bugs. Under the "Help" menu in the editor there is an option "Report a Bug".

You can even attach a sample project that highlights the issue, to help us reproduce the problem.
When reporting a bug it's always good to clearly state what kind of problem you're experiencing.

To minimize confusion here is a list of different categories:

### Editor side problem
Since Unity for PSM is based on the regular Unity 4.3.4, it's quite possible that we've "inherited" bugs present in the normal Unity version.
That means that an editor side bug might already have been fixed and scheduled to be released in an upcoming Unity version.
On the other hand it's also quite possible there is something related to the "Unity for PSM" support that triggers the problem.
Reporting the issue will make us aware that there is a potential problem.

### Unimplemented feature
There could be reasons why something is missing from the "Unity for PSM" support, when compared with other platforms.
Maybe it doesn't apply well within the PSM framework. Maybe there is a hardware difference making it impossible to support.
Or maybe it's simply an oversight, and something we just need to be made aware of.
In any case - reporting it will make sure we at least will consider it for a future version of Unity for PSM (or properly explain why it's not possible to support).

### Unexpected behavior
This is when the Unity for PSM runtime on the PS Vita behaves differently to what is expected - for example when comparing with the Editor or when running on another platform (Android, iOS, etc).
Usually means that a subsystem (rendering, physics, audio or similar) doesn't produce the expected result.
There could be reasons why the behavior is different, but if it's not mentioned in this documentation, chances are that this is a bug of some sort.

### Crash, hang or other loss of application control
This is the most severe problem.
There could be reasons why this is a legitimate (an out-of-memory crash is one example). But most of the time it's a bug in the Unity runtime (or any of its subsystems).
Internally these bugs usually have the highest priority, since the cause the most grief among developers.
See below how you can help us track down and fix these problems.

## When the DevAssistant crashes

Even though we try our best to fix all the nastiest bugs in Unity for PSM, there is still the possibility that the Unity runtime or the DevAssistant contains some critical problem.

Most of the time we can recover from a problem, and display some kind of error message in the console log output. But sometimes the problem is just too severe.

### The C2-12828-1 error code
When this happens the PS Vita will display an error message ; usually with the C2-12828-1 error code. C2-12828-1 simply means that the Unity Runtime (or sometime else) has crashed.

There could be many reasons why the runtime crashes ; for example :

* Crash bug in the Unity source code (or in one of its subsystems).
* Failed to allocate memory (i.e an out-of-memory error).
* Unimplemented code path in Mono / runtime class libraries.
* Some kind of internal Mono error.

In essence - this error code only indicates that a crash happened - **not** _what_ caused the crash.

In some cases there are clues in the device console log to what went wrong - have a look at [PsmDeviceForUnity.exe](PSMPsmDevice) for information how to retrieve the device log.

### Submit the crash report
The good thing is that the PS Vita will try to help, by providing the possibility to submit a crash report.
So, when you see runtime error causing a crash please help us (and you) out by sending the crash report to us.
It would also help us if you could add a note to the crash report (anything that you think might have caused the crash to happen) 
 - or if you've already submitted a bug report / repro project you can {+quote the case number+} in the notes.
This is an excellent way to covering all bases, and will help us cross reference the crash report with the case number.

