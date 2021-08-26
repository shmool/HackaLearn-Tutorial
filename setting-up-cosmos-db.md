# Setting up Cosmos DB

Cosmos DB is a No-SQL database on Azure. It works with several APIs, meaning you can choose one of five popular database languages \(syntaxes\) to access it, for instance SQL \(yes, even though it's No-SQL\) and MongoDB. Within a DB you can create  up to 20 containers, each with its own partition key. 

When working with Cosmos DB it's useful to think ahead of time how to model the data, specifically which partition key will be used in each container. Here are some resources to learn about the No-SQL structure and partition key considerations:

{% embed url="https://docs.microsoft.com/en-us/azure/cosmos-db/how-to-model-partition-example" %}

{% embed url="https://www.youtube.com/watch?v=utdxvAhIlcY&t=1722s" %}

## Opening a Cosmos DB account

In the Azure Portal, click on "New Resource" and search for "Cosmos DB". Select it and hit "create".

Fill in the details:

* You can choose the same resource group you created for the Static Web App resource, since they belong to the same application.
* Give a name to the Cosmos DB account.
* Choose the location closest to you. There's an option to create replicas or distribute the data in several locations globally, which you can set up at a later stage.
* Select a plan. 
  * With the provisioned throughput plan you can set up one Azure account with a free tier.
  * With the Serverless plan there's a generous free amount of requests and data storage included. It you pass it, your account will be charged by throughput. 
  * Learn more about [Cosmos DB pricing plans](https://azure.microsoft.com/pricing/details/cosmos-db/?WT.mc_id=javascript-11627-shjacobs).



