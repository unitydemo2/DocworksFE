#Creating UnityWebRequests

WebRequests can be instantiated like any other object. Two constructors are available:

* The standard, parameter-less constructor creates a new UnityWebRequest with all settings blank or default. The target URL is not set, no custom headers are set, and the redirect limit is set to 32.
* The second constructor takes a string argument. It assigns the UnityWebRequest's target URL to the value of the string argument, and is otherwise identical to the parameter-less constructor.

##Example

````
UnityWebRequest wr = new UnityWebRequest(); // Completely blank
UnityWebRequest wr2 = new UnityWebRequest("http://www.mysite.com"); // Target URL is set
````