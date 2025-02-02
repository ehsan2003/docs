# upload.GetFile

Returns content of a whole file or its part.

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
    new Api.upload.GetFile({
      location: new Api.InputFileLocation({
        volumeId: BigInt("-4156887774564"),
        localId: 43,
        secret: BigInt("-4156887774564"),
        fileReference: Buffer.from("arbitrary data here"),
      }),
      offset: 43,
      limit: 100,
      precise: true,
      cdnSupported: true,
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

  const result: Api.upload.File = await client.invoke(
    new Api.upload.GetFile({
      location: new Api.InputFileLocation({
        volumeId: BigInt("-4156887774564"),
        localId: 43,
        secret: BigInt("-4156887774564"),
        fileReference: Buffer.from("arbitrary data here"),
      }),
      offset: 43,
      limit: 100,
      precise: true,
      cdnSupported: true,
    })
  );
  console.log(result); // prints the result
})();
```

:::
::::

## Parameters

|       Name       | Type                                                                                                                              | Description                                                                                             |
| :--------------: | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
|    **flags**     | [#](https://core.telegram.org/type/%23)                                                                                           | Flags, see [TL conditional fields](https://core.telegram.org/mtproto/TL-combinators#conditional-fields) |
|   **precise**    | [flags](https://core.telegram.org/mtproto/TL-combinators#conditional-fields).0?[true](https://core.telegram.org/constructor/true) | Disable some checks on limit and offset values, useful for example to stream videos by keyframes        |
| **cdnSupported** | [flags](https://core.telegram.org/mtproto/TL-combinators#conditional-fields).1?[true](https://core.telegram.org/constructor/true) | Whether the current client supports [CDN downloads](https://core.telegram.org/cdn)                      |
|   **location**   | [InputFileLocation](https://core.telegram.org/type/InputFileLocation)                                                             | File location                                                                                           |
|    **offset**    | [int](https://core.telegram.org/type/int)                                                                                         | Number of bytes to be skipped                                                                           |
|    **limit**     | [int](https://core.telegram.org/type/int)                                                                                         | Number of bytes to be returned                                                                          |

## Result

[upload.File](https://core.telegram.org/type/upload.File)

## Possible errors

| Code | Type                   | Description                                                                                                      |
| :--: | ---------------------- | ---------------------------------------------------------------------------------------------------------------- |
| 401  | AUTH_KEY_PERM_EMPTY    | The temporary auth key must be binded to the permanent auth key to use these methods.                            |
| 400  | CHANNEL_INVALID        | The provided channel is invalid                                                                                  |
| 400  | CHANNEL_PRIVATE        | You haven't joined this channel/supergroup                                                                       |
| 406  | FILEREF_UPGRADE_NEEDED | The client has to be updated in order to support [file references](https://core.telegram.org/api/file_reference) |
| 400  | FILE_ID_INVALID        | The provided file id is invalid                                                                                  |
| 400  | FILE_REFERENCE\_`*`    | The file reference expired, it [must be refreshed](https://core.telegram.org/api/file_reference)                 |
| 400  | FILE_REFERENCE_EXPIRED | File reference expired, it must be refetched as described in <https://core.telegram.org/api/file_reference>      |
| 400  | LIMIT_INVALID          | The provided limit is invalid                                                                                    |
| 400  | LOCATION_INVALID       | The provided location is invalid                                                                                 |
| 400  | MSG_ID_INVALID         | Invalid message ID provided                                                                                      |
| 400  | OFFSET_INVALID         | The provided offset is invalid                                                                                   |
| 400  | PEER_ID_INVALID        | The provided peer id is invalid                                                                                  |

## Can bots use this method?

Yes

## Related pages

#### [Encrypted CDNs for Speed and Security](https://core.telegram.org/cdn)

How to handle file references.

#### [File references](https://core.telegram.org/api/file_reference)

How to handle file references.
