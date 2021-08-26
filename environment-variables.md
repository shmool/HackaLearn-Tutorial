# Environment Variables

Environment variables \(env vars\) are useful and important for several reasons:

* You can set up a different value for different environments without touching the code.
* You can keep secrets safe and not share them within the repository.
* If you need to change the value - it's in one place \(per environment\).

In Angular there are different `environment.ts` files for each environment \(two by default\). They're used for different values in the front-end app in development and production. \(You can set up additional environments.\) Don't use them to hold secrets, since they belong to the client-side application, where everything is eventually exposed to the users. 

With the API of Azure Static Web Apps, there are environments for local development, production \(deployed app\) and staging.  

## Development Env Vars

The file `api/local.settings.json` holds the local environment variables. By default, it's opted-out of git \(see `api/.gitignore`\) . There are already two variables in this file under `"Values"` and you can add more. The keys and values must be strings with further restrictions as described in the docs:

> **Values** must be **strings** and not JSON objects or arrays. **Setting names** can't include a colon \(`:`\) or a double underline \(`__`\). Double underline characters are reserved by the runtime, and the colon is reserved to support [dependency injection](https://docs.microsoft.com/azure/azure-functions/functions-dotnet-dependency-injection?WT.mc_id=javascript-35337-shjacobs#working-with-options-and-settings).

Read more about the [local settings file](https://docs.microsoft.com/azure/azure-functions/functions-run-local?tabs=macos%2Cts%2Cbash&WT.mc_id=javascript-35337-shjacobs#local-settings-file). For example, we set up a variable called `SECRET_NAME` with the value `HackaLearn Dev` in `api/local.settings.json`: 

```text
{​​​​​​​
  "IsEncrypted": false,
  "Values": {​​​​​​​
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "AzureWebJobsStorage": "",
    "SECRET_NAME": "HackaLearn Dev",
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​,
  "Host": {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "CORS": "*"
  }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```

 To access the environment variables from within the API functions project, use `process.env.<env_var>`, for example, this way:

```typescript
const secretName = process.env.SECRET_NAME;
```

## Production and Staging Env Vars 

To set up the variable in production, in the Azure Portal at the Static Web App resource, go to "Configuration" in the menu on the left \(below "Settings"\). Click on "Add", enter the name and value, and click OK. You can add several variables this way. When finished, **hit "Save"**.  If you have an active staging environment you can choose it in the dropdown to set up different values. By default the production variables are copied to staging. 

