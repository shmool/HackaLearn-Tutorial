# Working locally

The authentication feature works only on the deployed app. Yet, it's essential to emulate it to develop the relevant components and features within our application. 

Wassim Chegam, Cloud Advocate at Microsoft, has led the development of the Static Web Apps CLI, a command-line tool that enables you to work with Static Web Apps locally. It emulates authentication, serves as a proxy to the API and helps connecting the app to Azure.

Read about [local development with the SWA CLI](https://docs.microsoft.com/azure/static-web-apps/local-development?WT.mc_id=javascript-11627-shjacobs).

1. If you haven't yet, install the CLI globally: `npm install -g @azure/static-web-apps-cli` \(You can [see the package and check for updates](https://www.npmjs.com/package/@azure/static-web-apps-cli)\)
2. Enter the project folder in the terminal
3. Angular:
   1. If you only have the Angular app, run `ng serve` in one terminal and `swa start` [`http://localhost:4200/`](http://localhost:4200/)
   2. If you have also an API running \(Functions local server\), run: `swa start` [`http://localhost:4200/`](http://localhost:4200/) `--api ./api/dist`

