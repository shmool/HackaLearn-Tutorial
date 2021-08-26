# Add API

## Why Serverless Functions?

Many operations should be performed on the server side, as opposed to the client side. These are the main use cases:

* The operation is "heavy" and may overload the user's device.
* The logic is a secret, and the user should get only the result.
* The operation involves accessing the DB or other services that shouldn't be accessed directly by the users.
* The received data should be validated.
* The operation is not specific to a user or an instance of the application.

> Remember, any code and assets that are being served to the client side cannot be fully protected. The users can see it, download it, share it. Server-side code is not exposed to the clients.

With Serverless Functions we don't have to manage a whole server. We can just write the needed functions. They're managed by the Cloud: triggered, run, scaled and protected. 

Static Web Apps come with a built-in integration with API functions. These are endpoints that can perform operations or call other functions. The API functions reside within the Static Web App project \(and thus are exposed to whoever has access to the project on GitHub\). In addition to the integrated API you can set up a Functions App with separate functions that can be triggered in different ways. 

> Remember, endpoints exposed to the users can be used directly with HTTP requests with whatever payload the user sends. The function should be protected by authorizing the caller prior to running, and validating the received data.

## Setting up a Functions project

There are great integrations of Functions with VS-Code. However, the instructions below do not rely on VS-Code nor on Azure CLI.

We'll use the Functions Core Tools to create and develop the Functions app. First, install the package globally, giving it administrator permissions by default:

```text
npm install -g azure-functions-core-tools@3 --unsafe-perm true
```

Then, enter the project's folder and create a Functions app called `api` by running:

```text
func init api
```

You can give it a different name. Just make sure that it aligns with the value of `api_location` in the Static Web App workflow file and update if needed.

You'll be presented with a list of languages that are supported by Functions. You can work with the language you're most comfortable with. In this tutorial we'll use TypeScript. Select `3 - node` and then `2 - typescript`. 

The project is created. Enter its folder to continue working:

```text
cd api
```

You can explore the project and see it includes the same files that we have in other NodeJS / TypeScript projects, such as `package.json` and `tsconfig.json`. Install the requires dependencies by running:

```text
npm i
```

where `i` is a shorthand of `install`. This command installs the libraries stated in `package.json`.

## Creating an HTTP-triggered function

Create a new function by running:

```text
func new
```

You'll be presented with a list of triggers for the function. The one relevant for Static Web Apps is `10 - HTTP trigger`.

Give a name to the function - preferably describe what the function does. For example, `GetUserDetails`. By default, this will also be the route to call the API, but you can configure a different route. 

A folder is created with the name of the function, and inside it two files: `index.ts` and `function.json`. In `function.json` you can see the function configuration - for instance the methods it allows \(defaults are GET and POST\). Here you can configure a different route for the API by adding a `route` configuration. `index.ts` is the function itself and is created with a boilerplate that may receive parameters either as query params \(GET request\) or in the body, and returns text.

## Running the function

To test this function, first run:

```text
npm start
```

from within the `api` folder. This starts the Functions local server. In the terminal you'll see a list of the available endpoints and the methods they support. You can keep this process running while developing your functions and adding new ones. Only if you change the configuration of the functions app itself \(for instance, `local.settings.json`\) you'll need to restart the process \(kill it with `Ctrl+C` and run `npm start` again\). 

Since the function we have just created supports GET requests, you can call it directly from the browser. Browse to `http://localhost:7071/api/GetUserInfo`. You will see the message that is returned by the function. You can add a name as a query param, which will return a different message: `http://localhost:7071/api/GetUserInfo?name=HackaLearn`. 

### The boilerplate function

Explore the boilerplate function in `index.ts`. The arguments you get that you can work with are `(context: Context, req: HttpRequest)`.The function looks for query parameters in case it was a GET request with `req.query.name` and then in the body with `(req.body && req.body.name)`​​​​​​​ . The response is set as `context.res` where you can set up the body, status code, and more. 

With `context.log()`​​​​​​​ you can log messages at run time and see them in the terminal where the Functions local server is running or at Application Insights in the Portal.

The boilerplate sets a string \(text\) as the response body \(`context.res`\). If you call this API as is from within the application you'll need to configure the response type since it is not the default JSON. We'll show below how to do that. You can change it to return an object or any other type of a valid HTTP response.

## Calling the API from the app

When deploying the application with SWA, the API becomes available in the app's URL \(whether it's the URL given by Azure or your custom domain, just like with `/.auth` routes\). You can access it in `https://<your-domain>/api/<API-route>`. For instance, `http://hackalearn.shmool.me/api/GetUserInfo`. Just like the authentication feature, this is available on the deployed application, and can be emulated locally with the SWA CLI.

Since the API and the Client run on different ports, if you want to call it directly from the app you'll need to configure CORS for the Functions app. However, since we're using the SWA CLI which emulates the features that we get when the app is deployed, we can use direct routes without the need to configure CORS. 

We'll cover first how to work with the SWA CLI which is simpler, then what happens if you don't use the SWA CLI.

### With the SWA CLI

Whenever using the API from within the front-end app, you just need to point to `/api/<API-route>`. For instance, to perform a GET request to `GetUserInfo` with Angular, use the `HttpClient` this way:

```typescript
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  userInfo$ = this.http.get(`/api/GetUserInfo`);
  
  // injecting the HttpClient service
  // note: you may need to import HttpClientModule in your AppModule
  constructor(private http: HttpClient) { }
}
```

You'll need to subscribe to the observable or use the async pipe to extract the data.

Restart the SWA CLI with the following command to serve as a proxy both for the Angular CLI and the Function Core Tools server \(when both `ng serve` and the API's `npm start` are running in other terminals\):

```text
swa start http://localhost:4200 --api http://localhost:7071
```

Any request from within the front-end application should work now. Also, as long as the API supports GET requests, you can access it directly from the browser at `http://localhost:4280/api/<API-route>`. 



### Without the SWA CLI

Within the front-end code you need to call the full path of the API. For instance, `http://localhost:7071/api/GetUserInfo`. However, in production the path would be only the route: `/api/GetUserInfo`. Usually, front-end frameworks come with an environment-management system, where you can configure different values for different environments. In this case, you can configure `endpoint` with the value `http://localhost:7071` for development and an empty string `''` for production. Then use it within the code.

Angular projects come with two environment files by default. You can configure the endpoint within the `environment` object within these files. Then, when calling the endpoint, use for example: 

```text
`${environment.enpoint}/api/GetUserInfo`
```

Angular's build command will import the correct environment file.

Another thing you'll need to do is to configure CORS, since you're accessing the endpoint from a different port. Add `"Host"` configuration with `"CORS": "*"` in `local.settings.json` this way:

```text
{​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
  "IsEncrypted": false,
  "Values": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "AzureWebJobsStorage": ""
  }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​,
  "Host": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "CORS": "*"
  }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```



