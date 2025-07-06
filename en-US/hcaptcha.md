---

[`Back to Home`](../README.md) [`Previous`](recaptcha.md) [`Next`](incapsula.md) [`中文文档`](../zh-CN/hcaptcha.md)

## Hcaptcha

### Score Explanation

🚨🚨🚨
If you get a value but website validation fails, contact admin

### referer Parameter Explanation

🚨🚨🚨
Trigger page URL, ✅Copy the complete address displayed in browser✅, do not modify it, and especially do not use developer tools❌ to find it.
Alternatively, find the package as shown below, take the value of host parameter, set referer as http://{host} as shown in image. Example: http://democaptcha.com
![hcaptcha](/images/hcaptcha/img.png)

### Request URL (POST):

| Version     | Endpoint                                               |
| ----------- | ------------------------------------------------------ |
| `Universal` | `http://api.nocaptcha.io/api/wanda/hcaptcha/universal` |

### Request Headers:

| Header         | Description                                                                                                           | Required |
| -------------- | --------------------------------------------------------------------------------------------------------------------- | -------- |
| `User-Token`   | `User key, get from homepage`                                                                                         | `Yes`    |
| `Content-Type` | `application/json`                                                                                                    | `Yes`    |
| `Developer-Id` | `Developer ID, for developer users. String from invitation link (e.g. xxx/register?c=abcdef, abcdef is Developer ID)` | `No`     |

### POST Data (JSON):

| Parameter        | Type      | Description                                                                                                              | Required |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------------ | -------- |
| `sitekey`        | `String`  | `hCaptcha integration key`                                                                                               | `Yes`    |
| `referer`        | `String`  | `See parameter explanation above`                                                                                        | `Yes`    |
| `rqdata`         | `String`  | (_Enterprise_) `Pass this value if captcha config returns captcha_rqdata/captcha_rqtoken (e.g. Discord channel join)`    | `No`     |
| `proxy`          | `String`  | `Format: ip:port or usr:pwd@ip:port or socks5://ip:port (contact admin if issues)`                                       | `No`     |
| `region`         | `String`  | `When using proxy, pass proxy region e.g. hk, sg`                                                                        | `No`     |
| `invisible`      | `Boolean` | `Whether verification is invisible (default false)`                                                                      | `No`     |
| `need_ekey`      | `Boolean` | `Whether to return E0_ey... (default false)`                                                                             | `No`     |
| `preflight_uuid` | `String`  | (_Enterprise_) `Preflight ID for maintaining context (proxy region, UA, etc.) `[#Preflight API](./hcaptcha_preflight.md) | `No`     |

### Response Data (JSON):

| Parameter                  | Type      | Description                                                           |
| -------------------------- | --------- | --------------------------------------------------------------------- |
| `status`                   | `Integer` | `Success status: 1=success, 0=failure (use this to determine status)` |
| `msg`                      | `String`  | `Result message in Chinese`                                           |
| `id`                       | `String`  | `Unique request ID (for logging/querying)`                            |
| `data.generated_pass_UUID` | `String`  | `Verification pass UUID (P1_xxx/F1_xxx) for subsequent validation`    |
| `data.ekey`                | `String`  | `Verification key (E0_xxx) for subsequent validation`                 |
| `cost`                     | `String`  | `Verification time (milliseconds)`                                    |

```
{
  "cost": "9187.84ms",
  "data": {
    "generated_pass_UUID": "P1_eyxxx",
    "user_agent": "..."
  },
  "id": "c5b976bd-4c01-4378-bb44-324c76e9fe0f",
  "msg": "验证成功",
  "status": 1
}
```

### Sample

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import HcaptchaCracker


cracker = HcaptchaCracker(
    user_token="xxx",
    sitekey='a9b5fb07-92ff-493f-86fe-352a2803b3df',
    referer="https://discord.com/channels/253581140072464384/357581480110850049",
    rqdata="RRZ5RNoOL4uNPvEp0yB+bMPkBe2lUiM7p4u5lMAVUC9UBmzxJqdDDpGMrcDNApg/DDAQNIIlwEn2dLr7dZMg32I2bi523ZRfkAKpKxxg1sqnVW0xR9Y9ZCcwv54EiHeEqQ+iipixAVozAb6LjtwzNm2H9L15iSN8QfVrcp0Z",
    debug=True,
)
ret = cracker.crack()
print(ret)
```
