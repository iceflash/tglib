## tglib

TDLib (Telegram Database library) bindings for Node.js

[![npm](https://img.shields.io/npm/v/tglib.svg)](https://www.npmjs.com/package/tglib)

-----

### Getting started

1. Build the binary (https://github.com/tdlib/td#building)
2. `npm i -S tglib`

-----

### APIs

tglib provide some useful methods that makes your Telegram app development easier.

#### Authorizing an user

```js
const client = new Client({
  apiId: 'YOUR_API_ID',
  apiHash: 'YOUR_API_HASH',
  auth: {
    type: 'user',
    value: 'YOUR_PHONE_NUMBER',
  },
})
```

#### Authorizing a bot

```js
const client = new Client({
  apiId: 'YOUR_API_ID',
  apiHash: 'YOUR_API_HASH',
  auth: {
    type: 'bot',
    value: 'YOUR_BOT_TOKEN',
  },
})
```

#### ![](https://placehold.it/12/efcf39/000?text=+) Low Level APIs


##### `client.ready`


This promise is used for initializing tglib client and connect with Telegram.

```js
await client.ready
```


##### `client.on(event, callback)` -> Void


<details>
<summary>Expand</summary>
<p>

This API is provided by tglib, you can use this API to attach an event listener for iterating updates.

```js
client.on('_update', console.log.bind(console))
client.on('_error', console.error.bind(console))
```
</p>
</details>


##### `client._send(query)` -> Promise -> Object


<details>
<summary>Expand</summary>
<p>

This API is provided by TDLib, you can use this API to send asynchronous message to Telegram.

```js
await client._send({
  '@type': 'sendMessage',
  'chat_id': -123456789,
  'input_message_content': {
    '@type': 'inputMessageText',
    'text': {
      '@type': 'formattedText',
      'text': '👻',
    },
  },
})
```
</p>
</details>


##### `client._execute(query)` -> Promise -> Object


<details>
<summary>Expand</summary>
<p>

This API is provided by TDLib, you can use this API to execute synchronous action to Telegram.

```js
await client._execute({
  '@type': 'getTextEntities',
  'text': '@telegram /test_command https://telegram.org telegram.me',
})
```
</p>
</details>


##### `client._destroy()` -> Promise -> Void


<details>
<summary>Expand</summary>
<p>

This API is provided by TDLib, you can use this API to destroy the client.

```js
await client._destroy()
```
</p>
</details>


##### `client.fetch(query)` -> Promise -> Object


<details>
<summary>Expand</summary>
<p>

This API is provided by tglib, you can use this API to send asynchronous message to Telegram and receive response.

```js
const chats = await client.fetch({
  '@type': 'getChats',
  'offset_order': '9223372036854775807',
  'offset_chat_id': 0,
  'limit': 100,
})
```
</p>
</details>


#### ![](https://placehold.it/12/3abc64/000?text=+) High Level APIs


tglib provides a collection of APIs that designed for ease of use and handiness. These APIs are located under `client.tg` property.


##### `client.tg.sendTextMessage(chatId, text, options = {})` -> Promise -> Void


<details>
<summary>Expand</summary>
<p>

This API is provided by tglib, you can use this API to send message to a chat. If the `options` argument is specified, the function will combine your options with its default.

```js
await client.sendTextMessage('123456789', 'Hello *World*', {
  'parse_mode': 'markdown',
  'disable_notification': true,
  'clear_draft': false,
})
```
</p>
</details>

-----

### Requirements

- TDLib binary
> If you planning to build TDLib for Windows, please see [here](https://github.com/c0re100/F9TelegramUtils#compile-tdlib-on-windows) for more information.
- Node.js 10 preferred (minimum >= 9.0.0)
> Note: If you are using Node.js 9.x, you may encounter a warning message `Warning: N-API is an experimental feature and could change at any time.`, this can be suppressed by upgrading to version 10.

-----

### License

tglib uses the same license as TDLib. See [tdlib/td](https://github.com/tdlib/td) for more information.
