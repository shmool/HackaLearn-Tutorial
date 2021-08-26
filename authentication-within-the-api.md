# Authentication within the API

[SWA Authentication and Authorization](https://docs.microsoft.com/azure/static-web-apps/authentication-authorization?WT.mc_id=javascript-35337-shjacobs)

In many cases we'd like to identify the user in the API. For instance, to create and retrieve the user data from the DB. Although the user information \(clientPrincipal\) can be accessed at the client-side through your-domain/.auth/me, sending it over to the API is not a good idea. The client can be bypassed when calling the API with a direct HTTP request, and the caller can send any payload in the body.  

This is also a reason to validate data that is received in the API, especially if it's saved in the DB.  

Since Azure controls the connection between the client and the API, it can securely attach the user details directly from the session to the header of the API request. To retrieve it, use the following code or a variation of it:

```typescript
const header = req.headers['x-ms-client-principal'];
let clientPrincipal = null;
if (header) {​​​​​
  const encoded = Buffer.from(header, 'base64');
  const decoded = encoded.toString('ascii');
  clientPrincipal = JSON.parse(decoded);
}​​​​​
```

 Note: The code example in the docs is similar, and returns the user information as the response body.

