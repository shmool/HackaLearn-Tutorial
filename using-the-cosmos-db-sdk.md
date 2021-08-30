# Using the Cosmos DB SDK

The Cosmos DB SDK for JavaScript is suitable for TypeScript as well. It enables you to quickly connect to the database and perform common operations. It's responsible to all the connectivity management behind the scenes.

Even though the SDK can work from within the Front-end application, this is not a good practice. In that case the connection URI and secret key will be available to the client-side users, and they may be able to connect and use the database directly. To solve this, we're using Serverless Functions - our API.

To use the SDK, first install it in the API project. **From within the api folder**, run:

```text
npm i @azure/cosmos -S
```

This will download the library, install it under `node_modules` and add it to `dependencies` in `package.json`. 

## Connect to the Cosmos DB account

To set up a connection to a container within a database in Cosmos DB, first we need to create a `CosmosClient` . For this we need the endpoint and the key, or a connection string which includes both. You can find all the values in the Cosmos DB account in the **Keys** tab.

Make use of [environment variables](environment-variables.md) to store the necessary values. Don't forget to set them up in the configuration of the Static Web App as well.

For example,  we'll use a URI and key here. We'll add them to `local.settings.json` as `COSMOS_URI`  and `COSMOS_KEY`. Then, in the function body we'll create the Cosmos DB Client.

```text
import { AzureFunction, Context, HttpRequest } from "@azure/functions"
import { CosmosClient } from "@azure/cosmos"

const httpTrigger: AzureFunction = async function (context: Context, req: HttpRequest): Promise<void> {
  const endpoint = process.env.COSMOS_ENDPOINT;
  const key = process.env.COSMOS_KEY;

  const client = new CosmosClient({ endpoint, key });
  
  ...
```

## Connect to the DB and container

Now, by passing the database and container name, we can access the data in the container. You can store these names as environment variables as well.

```text
...

  const client = new CosmosClient({ endpoint, key });

  const databaseName = 'hackalearn-db';
  const containerName = 'users';

  const database = client.database(databaseName);
  const container = database.container(containerName);
  
...
```

Now you can use the container for CRUD operations \(create, read, update, delete\), either by direct SDK calls or with queries. Note the usage of `.read()`, `.fetch()`, `fetchAll()` etc. The response has either a `resource` or `resources` member which holds the actual result.

The following methods are just some of the options available with the SDK.

## Get items

### Get all items

```text
  const itemsRes = await container.items.readAll().fetchAll();
  const items = itemsRes.resources;
```

### Get a single item by ID

To get a specific item, you must provide its ID and the value of the partition key.

```text
const itemRes = await container.item(itemId, partitionKeyValue).read();
const item = itemRes.resource;
```

### Query for items

Use any SQL query that should work on the data. You can test the queries and save them in the data explorer tab in the Portal.

```text
const groupId = req.query.groupId;
const query = `SELECT * FROM c WHERE c.groupId = "${groupId}"`;

const groupData = await container.items.query(query).fetchAll();
// no need to extract 'resources' here
```

## Create an item

```text
const item = { ... } // if no id is provided it will be generated
const itemRes = await container.items.create(item);
const createdItem = itemRes.resource;
```

Update an item



