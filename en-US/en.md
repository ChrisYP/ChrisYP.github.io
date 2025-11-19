## 🚫Attention!🚫 For the latest documents, please proceed to https://www.nocaptcha.io/user/documents
## Overview

**👉[中文文档](../README.md)👈**

### Currently Supported APIs

|                 Type                  |                                                             Description                                                              | Synchronous Result Retrieval | Points Deduction | Discount for Input Proxy | Running Status | Exclusive/Monthly (Contact Support) |
|:-------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------:|:----------------:|:------------------------:|:--------------:|:-----------------------------------:|
|  [recaptcha:universal](recaptcha.md)  |                                          `ReCaptcha (v2/v3 Universal), Direct token return`                                          |              ✅               |      `300`       |          `150`           |       ✅        |                  ❌                  |
| [recaptcha:enterprise](recaptcha.md)  |                                         `ReCaptcha (v2/v3 Enterprise), Direct token return`                                          |              ✅               |      `300`       |          `150`           |       ✅        |                  ❌                  |
|   [recaptcha:app](recaptcha_app.md)   |                                            `ReCaptcha (App Version), Direct token return`                                            |              ✅               | `❌Discontinued❌` |          `250`           |       ❌        |                  ❌                  |
|   [hcaptcha:universal](hcaptcha.md)   |                                      `Hcaptcha Universal, Direct return of generated_pass_UUID`                                      |              ✅               |      `300`       |          `150`           |       ✅        |                  ❌                  |
|   [incapsula:reese84](incapsula.md)   |                                   `Incapsula Shield reese84 Universal, Returns solution parameter`                                   |              ✅               |      `210`       |            ❌             |       ✅        |                  ❌                  |
| [incapsula:utmvc](incapsula_utmvc.md) |                     `Incapsula Shield __utmvc Universal, Direct server seamless verification or __utmvc cookie`                      |              ✅               |      `150`       |            ❌             |       ✅        |                  ❌                  |
| [incapsula:rbzid](incapsula_rbzid.md) |             `Incapsula Shield rbzid Universal, Returns verification parameter`             |              ✅               |      `100`       |            ❌             |       ✅        |                  ❌                  |
|        [akamai:v2](akamai.md)         |                                                 `Akamai v2/v3, Direct return of _abck`                                                 |              ✅               |      `1000`      |            ❌             |       ✅        |                  ✅                  |
|           [tls:v1](tls.md)            |           `tls forwarding interface, targeting ja3, http2 fingerprint verification interfaces (such as akamai/cloudflare)`           |              ✅               |      `100`       |            ❌             |       ✅        |                  ❌                  |
| [cloudflare:universal](cloudflare.md) | `CloudFlare Shield Universal, Returns cookies or captcha submission parameters (turnstile 300 points)` |              ✅              | `1000/300` | `1000/150` |       ✅        |                  ✅                  |
| [aws:universal](aws.md) | `Aws Waf Shield, Returns aws-waf-token (only seamless 150 points)` |              ✅              | `500/150`  | `250/150`  |       ✅        |                  ❌                  |
| [perimeterx:universal](perimeterx.md) | `Perimeterx Shield Universal, Returns _px2, _px3` |              ✅              |   `1000`   |     ❌      |       ✅        |                  ✅                  |
| [kasada:ct](kasada.md) | `Kasada Shield, Returns x-kpsdk-ct` |              ✅              |   `1000`   |     ❌      |       ✅        |                  ✅                  |
| [kasada:cd](kasada.md) | `Kasada Shield, Returns x-kpsdk-cd` |              ✅              |    `50`    |     ❌      |       ✅        |                  ❌                  |
| [datadome:universal](datadome.md) | `Datadome Shield, Returns datadome cookie` |              ✅              |   `1000`   |     ❌      |       ✅        |                  ✅                  |
| [shape:v1](shape.md) | `Shape Shield v1, Returns request header or form encryption parameters` |              ✅              |   `1000`   |     ❌      |       ✅        |                  ✅                  |
| [shape:v2](shape.md) | `Shape Shield v2, Returns request header or form encryption parameters` |              ✅              |   `1000`   |     ❌      |       ✅        |                  ✅                  |
| [vercel:universal](vercel.md) | `Vercel Shield Universal, Returns _vcrcs cookie` |              ✅              |   `150`    |     ❌      |       ✅        |                  ❌                  |
| [discord:join_channel](discord_join_channel.md) | `Discord Join Channel` |              ✅              |   `500`    |     ❌      |       ✅        |                  ❌                  |

### Proxy Usage Instructions

* Use proxies with account/password authentication or those that do not require whitelist authentication. Format: ip:port or usr:pwd@ip:port
* Use sticky/session proxies (i.e., IP remains unchanged for n minutes)
* Pay attention to proxy usage frequency, do not use a fixed proxy repeatedly

![proxy](/images/proxy.png)

### Definitions

* `Points`: Points consumed by the service, `1 dollar = 66,000 points` (`$1 = 66,000 points`)
* `User-Token`: User token, this parameter is required when calling the service, viewable on the user's homepage.
* `Developer-ID`: Developer ID, used by developer users. If the invite link on a user's homepage is something like
  xxx/register?c=abcdef, then `abcdef` is the Developer ID.

### Level Explanation

| Points Spent  | Level   | Discount | Description                                  |
|---------------|---------|----------|----------------------------------------------|
| `100,000,000` | `VIP 1` | `90%`    | Actual spend of `300` points is `270` points |
| `250,000,000` | `VIP 2` | `80%`    | Actual spend of `300` points is `240` points |
| `600,000,000` | `VIP 3` | `70%`    | Actual spend of `300` points is `210` points |

> !!! VIP discounts and proxy discounts cannot be enjoyed simultaneously.

### Rebate Description

* Invitation Rebate: When the directly invited user consumes, you get a `20%` rebate (i.e., `A` invites `B`, for
  every `300` points `B` consumes, `A` gets `60` points as rebate).
* Developer Rebate: When a user consumes and calls the service interface with a developer ID, the developer gets a `20%`
  rebate (no rebate for the inviter in this case).
* Developer rebate has priority over invitation rebate (i.e., if `A` invites `B`, and `B` enters `C's` developer ID, `C`
  gets `20%` rebate, and `A` gets nothing).
* When calling, if the developer ID is set to oneself, no rebate can be obtained.

### Rebate Use

* Convert to Balance: Convert `1:1` to balance for service consumption.
* Cash Out: Currently supports cash out in denominations of `10U`, `20U`, `50U`, `100U`. Withdrawals are only
  to `BSC chain (BEP20)` addresses.

### Wallet Data Query API

```text
http://api.nocaptcha.io/api/get_user_balance?user_token={User-Token}&nickname={nickname}
```

| Parameter Name | Type     | Description                       | Required |
|----------------|----------|-----------------------------------|----------|
| `User-Token`   | `String` | `User token xxxx-xxx...`          | `Yes`    |
| `nickname`     | `String` | `Username for login. abc@xxx.com` | `Yes`    |

`http://api.nocaptcha.io/api/get_user_balance?user_token=40201fad-6666-3333-9999-b9f658666666&nickname=admin@nocaptcha.io`

### Response Data（JSON）:

```
{
    "code": 200,
    "msg": "success",
    "data": {
        "money_data": {
            "balance": "9112475",
            "profit": "3471240",
            "used_profit": "0",
            "consume": "887524",
            "today_consume": "0"
        }
    }
}
```
