------

[`Back to homepage`](en.md)    [`中文文档`](../zh-CN/discord_join_channel.md)

### 🚨🚨🚨  
Before calling this API, ensure that the Discord account token and channel name are correct and exist. **Except for error code `10008`, all other cases will incur charges.**  

## Discord Join Channel (beta)

### Request URL (POST):

| Version            | API Endpoint                                                       |
|-------------------|--------------------------------------------------------------------|
| `Universal`       | `http://api.nocaptcha.io/api/wanda/discord/join_channel`           |

### Request Headers:

| Parameter Name   | Description                                                             | Required |
|-----------------|-----------------------------------------------------------------------|--------|
| `User-Token`    | `User secret key, obtained from the homepage`                           | Yes    |
| `Content-Type`  | `application/json`                                                      | Yes    |
| `Developer-Id`  | `Developer ID, used by developer users. It's the string from the user's homepage invite link (e.g., if it's xxx/register?c=abcdef, then abcdef is the developer ID)` | No |

### POST Data (JSON):

| Parameter Name  | Type      | Description                                                                                                                                    | Required |
|----------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------|--------|
| `token`      | `String` | `discord user token`                                                                                                                   | Yes    |
| `channel_name`      | `String` | `e.g. rust (https://discord.com/invite/{channel_name}) `            | Yes    |

### Response Data (JSON):

| Parameter Name              | Type      | Description                                                                      |
|---------------------------|---------|---------------------------------------------------------------------------------|
| `status`                   | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`                      | `String`  | `Chinese description of the result`                                              |
| `id`                       | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)` |
| `data.result` | `String`  | `{"type":0,"code":"rust"...` |
| `cost`                     | `String`  | `Verification time taken (in milliseconds)`                                       |

