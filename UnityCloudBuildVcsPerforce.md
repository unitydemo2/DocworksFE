# Using Perforce with Unity Cloud Build

Unity Cloud Build supports projects hosted in Perforce (see [www.perforce.com](https://www.perforce.com)).

**Username and password**

In your Perforce server, create a new user for Unity Cloud Build, along with a secure password. If your Perforce host supports it, make this a read-only user account.

**Ticket authentication**

Using your Perforce administration tools, create a new user. When authenticating against Perforce, Cloud Build retrieves and uses the assigned ticket during the login process.

**Unicode-enabled servers**

Unity Cloud Build does not support unicode-enabled Perforce servers.
