---
[`Back to Home`](en.md)    [`中文文档`](../zh-CN/hcaptcha_preflight.md)

## hCaptcha Preflight API (Enterprise)

### When to Use

Use when a website has noticeable score detection to improve verification pass rates.

### Description

Used to maintain consistent contextual proxy region, UserAgent, and other data with the business context.

### 🚨🚨🚨

After obtaining the `region` (e.g., `hk`, `gb`, `us`), **the proxy used must correspond to that region**. **The region obtained through this interface MUST be applied to your proxy; otherwise, this process becomes meaningless** (e.g. region=gb, user-**gb**:pwd@ip:port).

### Request URL (POST):

| API Endpoint                                                |
| ----------------------------------------------------------- |
| `http://api.nocaptcha.io/api/wanda/hcaptcha/preflight` |

### Request Headers:

| Header          | Description               | Required |
| --------------- | ------------------------- | -------- |
| `Content-Type`  | `application/json`        | Yes      |

### POST Data (JSON):

| Parameter | Type     | Description                 | Required |
| --------- | -------- | --------------------------- | -------- |
| `sitekey` | `String` | `hCaptcha integration key`  | Yes      |

### Response Data (JSON):

| Parameter                     | Type      | Description                          |
| ----------------------------- | --------- | ------------------------------------ |
| `success`                     | `Boolean` | `Whether the call succeeded`         |
| `data.data`                   | `Object`  | `Preflight response data`            |
| `data.data.preflight_uuid`    | `String`  | `Preflight request ID`               |
| `data.data.region`            | `String`  | `Country abbreviation for preflight` |
| `cost`                        | `String`  | `Verification time (ms)`             |

#### JSON Example
```
{
    "success": true,
    "data": {
        "preflight_uuid": "b5e404b6-55ca-4672-a83f-9a5f3e2e9882",
        "data": {
            "region": "ca",
            "navigator": {
                "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36"
            },
            ...
        }
    }
}
```
