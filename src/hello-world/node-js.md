# Node.js

MTKruto is available for Node.js on npm as
[`@mtkruto/node`](https://npm.im/@mtkruto/node). Here you will learn how you can
use MTKruto in your Node.js project.

## Prequisites

- [Node.js](https://nodejs.org)

## Setup

First, create a directory for our project, initialize package.json, and install
MTKruto:

```ts
mkdir ping
cd ping
npm init -y
npm install @mtkruto/node
```

> We’re using npm here, but you can also use pnpm, yarn, or anything else you
> prefer.

Create a file called `ping.js` and import the `Client` class from MTKruto:

```ts
const { Client } = require("@mtkruto/node");
```

> We’re using the CJS syntax here, but ESM is also supported by `@mtkruto/node`.

## Starting the Client

Before we can invoke functions, we first initialize and start a client.

Starting the client for the first time will take a little amount of time
regardless of the connection speed. It might even take more if you are
connecting to a test server. In this guide, our client will always take a little
to start since we don’t have a persistency layer for the sake of staying simple.

```ts
const client = new Client();

async function main() {
  console.log("Starting client...");
  await client.connect();
  console.log("Client started.");
}

main();
```

The above code initializes a client with the default parameters and no API
credentials. After that, it initiates a connection with Telegram’s test servers.

## Invoking Functions

You can make calls directly to the Telegram API using the `invoke()` method of
the client. The argument you pass to it should be an instance of a call
definition from the `functions` namespace.

Update your import declaration to look like this:

```ts
const { Client, functions } = require("@mtkruto/node");
```

And invoke a `ping` call:

```ts
const before = Date.now();
await client.invoke(new functions.Ping({ pingId: 1n }));
const diff = Math.floor(Date.now() - before);
console.log("Ping took", `${diff}ms.`);
```

## Conclusion

Your final code should look like this:

File name: ping.js

```ts
const { Client, functions } = require("@mtkruto/node");

const client = new Client();

async function main() {
  console.log("Starting client...");
  await client.connect();
  console.log("Client started.");

  const before = Date.now();
  await client.invoke(new functions.Ping({ pingId: 1n }));
  const diff = Math.floor(Date.now() - before);
  console.log("Ping took", `${diff}ms.`);
}

main();
```

Use the following command to run it:

```bash
node ping.js
```

You should get a result like this:

```ts
Starting client...
Client started.
Ping took 215ms.
```
