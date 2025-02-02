# messages.DeleteChatUser

Deletes a user from a chat and sends a service message on it.

## Example

::::tabs
:::tab{title="JavaScript"}

```js
const { Api, TelegramClient } = require("telegram");
const { StringSession } = require("telegram/sessions");

const session = new StringSession(""); // You should put your string session here
const client = new TelegramClient(session, apiId, apiHash, {});

(async function run() {
  await client.connect(); // This assumes you have already authenticated with .start()

  const result = await client.invoke(
    new Api.messages.DeleteChatUser({
      chatId: 43,
      userId: "username",
      revokeHistory: true,
    })
  );
  console.log(result); // prints the result
})();
```

:::

:::tab{title="TypeScript"}

```ts
import { Api, TelegramClient } from "telegram";
import { StringSession } from "telegram/sessions";

const session = new StringSession(""); // You should put your string session here
const client = new TelegramClient(session, apiId, apiHash, {});

(async function run() {
  await client.connect(); // This assumes you have already authenticated with .start()

  const result: Api.Updates = await client.invoke(
    new Api.messages.DeleteChatUser({
      chatId: 43,
      userId: "username",
      revokeHistory: true,
    })
  );
  console.log(result); // prints the result
})();
```

:::
::::

## Parameters

|    Name    | Type                                                  | Description           |
| :--------: | ----------------------------------------------------- | --------------------- |
| **chatId** | [int](https://core.telegram.org/type/int)             | Chat ID               |
| **userId** | [InputUser](https://core.telegram.org/type/InputUser) | User ID to be deleted |

## Result

[Updates](https://core.telegram.org/type/Updates)

## Possible errors

| Code | Type                 | Description                                    |
| :--: | -------------------- | ---------------------------------------------- |
| 400  | CHAT_ADMIN_REQUIRED  | You must be an admin in this chat to do this   |
| 400  | CHAT_ID_INVALID      | The provided chat id is invalid                |
| 400  | PEER_ID_INVALID      | The provided peer id is invalid                |
| 400  | USER_ID_INVALID      | The provided user ID is invalid                |
| 400  | USER_NOT_PARTICIPANT | You're not a member of this supergroup/channel |

## Can bots use this method?

Yes

## Related pages
