# Vanilla JavaScript

It is less likely that you will use MTKruto this way. This guide is mainly to
demonstrate how simple it is to get started with MTKruto.

## Prequisites

- A modern web browser
- A text editor

## Setup

Create a file called `ping.html` with the following contents:

```html
<!DOCTYPE html>
<html>
    <head>
        <script type="module" defer>
            import { Client } from "https://esm.sh/@mtkruto/browser";
        </script>
    </head>
    <body>
    </body>    
</html>
```

## Starting the Client

Before we can invoke functions, we first initialize and start a client.

Starting the client for the first time will take a little amount of time
regardless of the connection speed. It might even take more if you are
connecting to a test server. In this guide, our client will always take a little
to start since we don’t have a persistency layer for the sake of staying simple.

Extend the contents of the `<script>` tag with this snippet:

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
import { Client, functions } from "https://esm.sh/@mtkruto/browser";
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

File name: ping.html

```html
<!DOCTYPE html>
<html>
    <head>
        <script type="module" defer>
            import { Client, functions } from "https://esm.sh/@mtkruto/browser";

            const client = new Client();

            console.log("Starting client...");
            await client.connect();
            console.log("Client started.");

            const before = Date.now();
            await client.invoke(new functions.Ping({ pingId: 1n }));
            const diff = Math.floor(Date.now() - before);
            console.log("Ping took", `${diff}ms.`);
        </script>
    </head>
    <body>
    </body>    
</html>
```

To run it, simply open that file with your browser. After opening the file, open
the developer tools, and navigate to the tab called Console.

You should see something like this:

```ts
Starting client...
Client started.
Ping took 215ms.
```
