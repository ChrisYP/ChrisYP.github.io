---

[`Back to Home`](en.md)    [`Previous`](vercel.md)   [`Next`](unlocker.md)    [`中文文档`](../zh-CN/discord_join_channel.md)

## Discord Join Channel (Beta)

### 🚨🚨🚨

Before calling this API, **please** ensure that the account token and channel name are correct and exist. **All calls will be charged except for returns with `code:10008`**

### Request URL (POST):

| Version              | API Endpoint                                             |
| -------------------- | -------------------------------------------------------- |
| `Universal` | `http://api.nocaptcha.io/api/wanda/discord/join_channel` |

### Request Headers:

| Parameter Name | Description                                                                                                                          | Required |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| `User-Token`   | `User secret key, obtained from homepage`                                                                                           | Yes      |
| `Content-Type` | `application/json`                                                                                                                   | Yes      |
| `Developer-Id` | `Developer ID, for developer users. String from user homepage invitation link (e.g., if link is xxx/register?c=abcdef, then abcdef is Developer ID)` | No       |

### POST Data (JSON):

| Parameter Name | Type     | Description                                                                                   | Required |
| -------------- | -------- | --------------------------------------------------------------------------------------------- | -------- |
| `token`        | `String` | `Discord user token`                                                                          | Yes      |
| `channel_name` | `String` | `Channel name, e.g.: rust (corresponding channel invite link format: https://discord.com/invite/{channel_name})` | Yes      |

### Response Data (JSON):

| Parameter Name | Type      | Description                                                    |
| -------------- | --------- | -------------------------------------------------------------- |
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge the result` |
| `msg`          | `String`  | `Chinese description of the result`                            |
| `id`           | `String`  | `Unique ID for this request (can be used for subsequent record queries)` |
| `data.result`  | `String`  | `Result data string, example: {"type":0,"code":"rust"...`      |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

### Why does join failure occur (i.e., `10008`)?

1. The group does not allow low-quality registered accounts to join, which is basically determined at registration time
2. The interface captcha score may be lower than Discord's set threshold, but it's available most of the time and can basically be ruled out
