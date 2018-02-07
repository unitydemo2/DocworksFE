#Creating UnityWebRequests

WebRequests can be instantiated like any other object. Two constructors are available:

* The standard, parameter-less constructor creates a new UnityWebRequest with all settings blank or default. The target URL is not set, no custom headers are set, and the redirect limit is set to 32.
* The second constructor takes a string argument. It assigns the UnityWebRequest's target URL to the value of the string argument, and is otherwise identical to the parameter-less constructor.

Multiple other properties are available for setting up, tracking status and checking result or UnityWebRequest.

##Example

````
UnityWebRequest wr = new UnityWebRequest(); // Completely blank
UnityWebRequest wr2 = new UnityWebRequest("http://www.mysite.com"); // Target URL is set

// the following two are required to web requests to work
wr.url = "http://www.mysite.com";
wr.method = UnityWebRequest.kHttpVerbGET;   // can be set to any custom method, common constants privided

wr.useHttpContinue = false;
wr.chunkedTransfer = false;
wr.redirectLimit = 0;  // disable redirects
wr.timeout = 60;       // don't make this small, web requests do take some time
````