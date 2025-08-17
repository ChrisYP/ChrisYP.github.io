[`Back to Home`](en.md)    [`Previous`](shape.md)    [`Next`](discord_join_channel.md)    [`中文文档`](../zh-CN/vercel.md)

## Vercel

### Pricing
* Consumes `150` points, requires `proxy`

### Description
* When you open the target page and see the following prompt, and the packet capture shows a request to `/.well-known/vercel/security/request-challenge`, and `_vcrcs` exists in `cookies`, it means `vercel` verification is present
    ![Verification style](/images/vercel/img1.png)

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `Universal` | `http://api.nocaptcha.io/api/wanda/vercel/universal` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Page URL that triggers vercel verification`    | `Yes` |
| `proxy`    | `String`  | `Proxy must be consistent, use overseas proxy, format: ip:port or usr:pwd@ip:port (contact admin if issues)` | `No` |
| `user_agent` | `String`  | `Custom user_agent`       | `No` |
| `timeout` | `Integer`  | `Verification timeout`       | `No` |

#### json example

```
{
    "href": "https://faucet.story.foundation/",
    "proxy": "user:pass@ip:port"
}
```

### Response Data (JSON):

#### Submit verification (submit=true)

| Parameter Name            | Type        | Description                            |
|----------------|--------------------|------------------------------------|
| `status`            | `String`   | `Submission status, success or fail`         |
| `message`           | `String`   | `Status description`                  |
| `verify_token`      | `String`   | `Token for verification, use in subsequent requests`        |
