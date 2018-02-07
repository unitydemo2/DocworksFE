#PS Vita: Debugging a crash

### Explicit null checks

Enabling explicit null checks results in some extra code being injected into your compiled scripts that checks for any NULL pointer references and throws a `NULLReference` exception if one occurs instead of the rather less helpful crash that would occur without the NULL checks. This option is always enabled for development builds but it can be useful to enable it for production code; the overhead it adds is small and usually not noticeable.

### TTY stack trace

If a crash occurs that cannot be caught by explicit NULL checks then your app stops running and a stack trace is dumped out to the PS Vita console (TTY). Unfortunately the trace does not contain any symbol information so is of limited use; however, you can use Visual Studio to get a lot more information about a crash.

### Debugging a crash with Visual Studio

If your application crashes on a dev-kit connected to your computer then you can attach to it using Visual Studio 2010 Professional to get more information about the crash. These instructions refer to Visual Studio 2010 which is the version we build Unity for PS Vita with but you should also be able to use Visual Studio 2012.

Before attaching to the application you need to tell Visual Studio where it can find the symbols for the application. Open Visual Studio 2010 and follow these steps:

1. Select the menu item __Tools__ > __Options__.

1. Select __Debugging__ > __Symbols__ in the list of options.

1. Add the path to the folder containing the symbol files that were written by the editor when you built your project; the required symbol files are written to __[your project's build folder]/SymbolFiles__.

Once you have set the symbol file location you can attach to the crashed application:

1. In the __Debu__ menu select __Attach To Process__.

1. Select __Transport = PS Vita Target__ and __Qualifier = [your dev-kit ID]__

1. Then in the process window, double-click on the PS Vita executable. This launches the debugger and allows you to inspect various properties including the call stack, thread states and registers. Note that you may need to switch the currently displayed thread to see the call stack for the code that actually caused the crash.

### How does this help?

If the crash happened in your script code, the top of call stack should show the script function where the crash happened. If the crash occurred in the Unity run time, you should be able to look at the call stack to see the script function which originated the call, or to investigate which system has a problem. This should help you diagnose any problems in your scripts. If the problem is a bug in the Unity run time, then the call-stack is a valuable piece of information which should be included in any bug report to Unity.

### Debugging core dumps

Debugging core dumps is similar to the above, but instead of attaching to the application, open the __.psp2dump__ file in Visual Studio, set the symbol file path and start debugging.
