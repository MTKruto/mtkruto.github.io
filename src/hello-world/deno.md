# Deno

MTKruto is available for Deno at <https://deno.land/x/mtkruto>. Here’s how you
can initialize a client, connect it, and invoke a ping request.

## Prerequisites

- [Deno](https://deno.land)

## Setup

For this guide, we will have only a single file and we won’t persist any data
since we won’t reuse the connection. For most projects, we recommend having a
directory with a Deno configuration file.

Create a file called `ping.ts` and import the `Client` class from MTKruto:

```ts
import { Client } from "https://deno.land/x/mtkruto/mod.ts";
```

> Remember to replace the import specifier to explicitly specify a specific
> version of MTKruto. We have omitted it here to stay simple.

## Starting the Client

Before we can invoke functions, we first initialize and start a client.

Starting the client for the first time will take a little amount of time
regardless of the connection speed. It might even take more if you are
connecting to a test server. In this guide, our client will always take a little
to start since we don’t have a persistency layer for the sake of staying simple.

```ts
const client = new Client();

console.log("Starting client...");
await client.connect();
console.log("Client started.");
```

The above code initializes a client with the default parameters and no API
credentials. After that, it initiates a connection with Telegram’s test servers.

## Invoking Functions

You can make calls directly to the Telegram API using the `invoke()` method of
the client. The argument you pass to it should be an instance of a call
definition from the `functions` namespace.

Update your import declaration to look like this:

```ts
import { Client, functions } from "https://deno.land/x/mtkruto/mod.ts";
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

File name: ping.ts

```ts
import { Client, functions } from "https://deno.land/x/mtkruto/mod.ts";

const client = new Client();

console.log("Starting client...");
await client.connect();
console.log("Client started.");

const before = Date.now();
await client.invoke(new functions.Ping({ pingId: 1n }));
const diff = Math.floor(Date.now() - before);
console.log("Ping took", `${diff}ms.`);
```

Use the following command to run it:

```bash
deno run --allow-net ping.ts
```

You should get a result like this:

```ts
Starting client...
Client started.
Ping took 215ms.
```
