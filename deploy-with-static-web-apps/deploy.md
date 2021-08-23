# Create your Static Web App

If you don't have an Azure account, go to [Essential Prerequisites](../preparation-1/essential-prerequisites.md). 

Go to the [Azure Portal](https://portal.azure.com/?WT.mc_id=javascript-38439-shjacobs). Select "Create new resource".

![](../.gitbook/assets/image%20%281%29%20%281%29.png)



In the search box \(which is above the list of services\) search for "Static web app" and select it from the dropdown menu.

![](../.gitbook/assets/image%20%282%29.png)

Click "Create". 

Fill out the details:

1. Create a new resource group with the name of your app \(or anything else you'd like to call it\).
2. Give a name to the SWA resource.
3. Select the closest location to you.
4. Connect to your GitHub account and select the repository of your app.
5. Select the framework you're using, then fill out the location of the code.
   1. For Angular: 
      1. api: "api", 
      2. build: "dist/&lt;project name&gt;"
6. Hit "Review & Create" 
7. Hit "Create"
8. Wait for the SWA resource to be ready \(few seconds\), then enter it \(click on the message\).

## That's it!!!

The SWA resource is ready on Azure. It has added a workflow \(action\) file to your repository. Now the action is taking place - it's building and deploying the application. This may take several minutes. You can see the action running on GitHub. Once it's done, click on the URL given to you on the SWA resource in the Portal and you should see your application.

