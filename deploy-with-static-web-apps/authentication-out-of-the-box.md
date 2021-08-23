---
description: Authenticate your users with third party providers
---

# Authentication Out of the Box

Once your application is deployed, it gets a service of user authentication with several third party providers. Just append the following routes to your application's URL to use it:

* Get the user details or null if they're not authenticated \("Client Principal"\): `/.auth/me` .
* Let the user log in with different providers:
  * GitHub: `/.auth/login/github` .
  * Twitter: `/.auth/login/twitter` .
  * AAD \(Azure Active Directory\): `/.auth/login/aad` .
* Let the user log out: `/.auth/logout` .

Later on we'll learn how to securely authenticate the user from within the API and how to use authorization with routing rules. 

