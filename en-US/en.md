## Overview

**👉[中文文档](/)👈**

### Currently Supported APIs

|                 Type                  |                                                             Description                                                              | Synchronous Result Retrieval | Points Deduction | Discount for Input Proxy | Running Status | Exclusive/Monthly (Contact Support) |
|:-------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------:|:----------------:|:------------------------:|:--------------:|:-----------------------------------:|
|  [recaptcha:universal](recaptcha.md)  |                                          `ReCaptcha (v2/v3 Universal), Direct token return`                                          |              ✅               |      `300`       |          `150`           |       ✅        |                  ❌                  |
| [recaptcha:enterprise](recaptcha.md)  |                                         `ReCaptcha (v2/v3 Enterprise), Direct token return`                                          |              ✅               |      `500`       |          `250`           |       ✅        |                  ❌                  |
|    [recaptcha:steam](recaptcha.md)    |                                               `ReCaptcha (Steam), Direct token return`                                               |              ✅               |      `600`       |          `300`           |       ✅        |                  ❌                  |
|   [recaptcha:app](recaptcha_app.md)   |                                            `ReCaptcha (App Version), Direct token return`                                            |              ✅               |      `500`       |          `250`           |       ❌        |                  ❌                  |
|   [hcaptcha:universal](hcaptcha.md)   |                                      `Hcaptcha Universal, Direct return of generated_pass_UUID`                                      |              ✅               |      `300`       |          `150`           |       ✅        |                  ❌                  |
|   [incapsula:reese84](incapsula.md)   |                                   `Incapsula Shield reese84 Universal, Returns solution parameter`                                   |              ✅               |      `210`       |            ❌             |       ❌        |                  ❌                  |
| [incapsula:utmvc](incapsula_utmvc.md) |                     `Incapsula Shield __utmvc Universal, Direct server seamless verification or __utmvc cookie`                      |              ✅               |      `150`       |            ❌             |       ✅        |                  ❌                  |
|        [akamai:v2](akamai.md)         |                                                 `Akamai v2, Direct return of _abck`                                                  |              ✅               |      `1000`      |            ❌             |       ✅        |                  ❌                  |
|           [tls:v1](tls.md)            |           `tls forwarding interface, targeting ja3, http2 fingerprint verification interfaces (such as akamai/cloudflare)`           |              ✅               |      `100`       |            ❌             |       ✅        |                  ✅                  |


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

