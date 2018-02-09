Reporting crash bugs on iOS
===========================

Before submitting a bug report, please check the [iOS Troubleshooting](TroubleShootingIPhone) page, where you will find solutions to common crashes and other problems.

If your application crashes in the Xcode debugger then you can add valuable information to your bug report as follows:-

1. Click Continue (__Run-&gt;Continue__) twice
1. Open the debugger console (__Run-&gt;Console__) and enter (in the console): **thread apply all bt**
1. Copy **all** console output and send it together with your bugreport.

If your application crashes on the iOS device then you should retrieve the crash report as described [here](http://developer.apple.com/iphone/library/technotes/tn2008/tn2151.html#ACQUIRING_CRASH_REPORTS) on Apple's website. Please attach the crash report, your built application and console log to your bug report before submitting.
