# Using Apache Subversion (SVN) with Unity Cloud Build

Unity Cloud Build supports projects hosted in Apache Subversion (SVN) repositories (see [subversion.apache.org](https://subversion.apache.org/)).

**Username and Password**

In your SVN server, create a new user just for Unity Cloud Build, along with a secure password. If your SVN host supports it, make this a read-only user account.

**Public SSH Keys **

Unity Cloud Build does not support connecting to your SVN repository using a public SSH Key. Use a username and password instead.

**SSL Certificates**

Self-signed SSL certificates are not supported. Unity Cloud Build does not SSL handshake with a server whose certificate is self-signed. The hostname in the certificate must match the hostname being accessed by Unity Cloud Build.
