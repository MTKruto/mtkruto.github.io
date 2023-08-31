# Welcome to MTKruto

MTKruto is a library that lets you interact with the
[Telegram API](https://core.telegram.org/#telegram-api). It can be used from
JavaScript or TypeScript, and can run on Deno, browsers, and Node.js.

## The Telegram API vs. the Bot API

[Bot API](https://core.telegram.org/bots/api) is a high-level HTTP interface to
the Telegram API that makes it easy to develop bots and lets you focus on being
more productive. We highly recommend it if you’re planning to develop complex
bots.

On the other hand, the Telegram API is the main API for building Telegram
clients. It uses the [MTProto](https://core.telegram.org/mtproto) protocol which
makes it a little more difficult to consume than the Bot API. Telegram clients
can be a GUI application on an end user’s device, or a process running
continuously in a server.

While the Bot API can only be used to work with bot accounts, the Telegram API
can be used to work with both bot and user accounts. As mentioned previously,
the Bot API is simply an interface to work with bot accounts using the Telegram
API.

## When to Use the Telegram API

- If you want to bypass the limits of the main instance of the Bot API without
  hosting your own instance (e.g., work with large files).
- If you want to develop your own Telegram app (e.g., alternative to
  [Telegram Web](https://web.telegram.org/a)).
- If you want to automate user accounts.
- If you have your own reasons.

## Things to Consider

- You can’t interact with the Telegram API using webhooks. You have to maintain
  a connection with Telegram servers.
