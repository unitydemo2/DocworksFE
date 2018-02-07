# WindowsLowIntegrity

Windows Standalone player can detect if it's running at Low Integrity Level (see Microsoft's documentation on [Designing Applications to Run at a Low Integrity Level](https://msdn.microsoft.com/en-us/library/bb625960.aspx) for more information). In this case, several things happen:

* The log file is written to %USER PROFILE%\AppData\LocalLow\\__CompanyName__\\__ProductName__
* PlayerPrefs is saved to HKCU\Software\AppDataLow\Software\\__CompanyName__\\__ProductName__