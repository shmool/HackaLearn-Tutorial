# Configuration

Docs: [Configure Azure Static Web Apps](https://docs.microsoft.com/azure/static-web-apps/configuration?WT.mc_id=javascript-35337-shjacobs)

In a single page application, the app serving starts from index.html. It loads the script files which include the client-side routes configuration. The router looks at the route given in the URL, applies rules \( `CanActivate` , etc.\) and loads the components accordingly. It also changes the URL and browser history when navigating within the app. 

When deploying the application, the Static Web App host \(the server\) where the app is stored and served from responds to the first request. If the given URL is the root, it serves index.html. For any other route it searches for a file in that location, as if it were a file system. This works good for assets \(usually, you can access the images of a website directly, for example\). But it doesn't work well with routes.  

There may be routes where you have HTML files to serve directly. You may have created several HTML files apart from the application, or used a static site generator \(scully.io\) which turned all or most of your application into standalone HTML files. However, if you do rely on the client-side router, you may need to configure the Static Web App host to serve the correct files.  

The SWA host can also deny accessing routes directly, using authorization rules and redirects. These rules will work when the routing request reaches the server, meaning when the user entered the URL in the address bar or clicked a link from an external location. When the user tries to navigate to these locations from within the application, the client-side router should apply the same rules. 

To configure the routes and authorization, create a new file named `staticwebapp.config.json` in the root project folder.Notice that if this file is empty, the deployment will fail.  Take a look at the example below.

The `navigationFallback` section configures serving a default file \(index.html\) in case no file was found in the requested route. 

Within `routes` you can configure authorization and redirects. Since `/admin` is only allowed for users who are authenticated, an anonymous user will receive a `401` - unauthorized. Instead of displaying the default "unauthorized" page from the server, by setting up `responseOverrides` for this case the user will be redirected to the login route. \(By the way, you may configure a new role for administrators.\) 

It's also highly recommended to protect api routes with allowed roles. This means that the protected function will not even be called unless the user is authorized. 

This is the configuration in the demo app: 

```text
{​​​​
  "routes": [
    {​​​​​​​​​​​
      "route": "/admin",
      "allowedRoles": ["authenticated"]
     }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
  ],
  "navigationFallback": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "rewrite": "index.html"
  }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​,
  "responseOverrides": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "401": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
      "redirect": "/login",
      "statusCode": 302
    }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
  }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```

