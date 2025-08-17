[`Back to Home`](en.md)    [`Previous`](tls.md)    [`Next`](aws.md)    [`中文文档`](../zh-CN/cloudflare.md)

## CloudFlare

### Service Description

* Online is only for testing service. For stable/large volume/exclusive/monthly/discount, please contact the administrator.

### Type Description

* Type 1: cookies (normal mode: `cf_clearance`, `__cf_bm`)
* When no redirect page appears but `cf_clearance` exists, you can set parameter alpha=true for seamless verification (or consult administrator), proxy is required
![cookies example](/images/cloudflare/cookies.png)

* Type 2: captcha mode (turnstile: `cf_turnstile-response`) (this type consumes 300 points, input proxy 150 points), proxy is optional
* ps: Usually embedded in login box, captcha parameter is `captcha_api_key` or similar key (just an example, not necessarily this), parameter value starts with `0.`

![captcha example](/images/cloudflare/captcha.png)

### Parameter Lookup

* cookies type: just input the trigger page URL

* turnstile type: need to input sitekey parameter additionally
![sitekey](/images/cloudflare/sitekey.png)

### Result Description

* Cloudflare cookies mode requires IP and UA consistency
* Cloudflare cookies mode checks TLS fingerprint, please use TLS request library or TLS forwarding service
* Cloudflare turnstile mode result can usually be used directly, input proxy only needs 150 points

### Request URL (POST):

| Version                | API URL                                                     |
|-------------------|----------------------------------------------------------|
| `Universal`  | `http://api.nocaptcha.io/api/wanda/cloudflare/universal`  |

### Request Headers:

| Parameter Name            | Description                                                                         | Required  |
|----------------|----------------------------------------------------------------------------|-----|
| `User-Token`   | `User secret, get from homepage`                                                               | `Yes` |
| `Content-Type` | `application/json`                                                         | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)` | `No` |

### POST Data (JSON):

| Parameter Name        | Type        | Description                                                                             | Required  |
|------------|-----------|--------------------------------------------------------------------------------|-----|
| `href`  | `String`  | `URL that triggers verification`                                           | `Yes` |
| `proxy`    | `String`  | `Required for cookies mode, optional for turnstile` | `Yes` |
| `sitekey`       | `String`  | `Required for turnstile type (costs 300 points)`                                         | `No` |
| `explicit`       | `Bool`  | `Required for turnstile type, check f12 for https://challenges.cloudflare.com/turnstile/v0/api.js?onload=cf__reactTurnstileOnLoad&render=explicit if js link contains render=explicit parameter, set to true, otherwise don't pass, default false`                                         | `No` |
| `action`       | `String`   | `Pass for turnstile type, see explanation below`                                         | `No` |
| `cdata`       | `String`  | `Pass for turnstile type, only pass if turnstile.render parameters contain cdata`                                         | `No` |
| `user_agent` | `String` | `Custom request header, don't pass if returns unsupported custom header`                            | `No` |
| `alpha` | `Boolean` | `Whether it's seamless cookies`                            | `No` |

#### action / cdata Lookup (not required, contact admin if questions)

When verification type is `turnstile`, and you find `render=explicit` parameter in the target website's `*turnstile/v0/api.js` link, then pass `explicit=true`, `action`, `cdata` lookup steps:

* Open f12 and search for `window.turnstile.render`
![render](/images/cloudflare/render.png)

* Set breakpoint here, clear cookie cache and refresh page, when it breaks here, check the `action` value and input it
![action](/images/cloudflare/action.png)

### Parameter Examples

#### cookies type

```json
{
    "href": "https://nowsecure.nl/",
    "proxy": "usr:pwd@ip:port"
}
```

#### turnstile type
```json
{
    "href": "https://visa.vfsglobal.com/chn/zh/deu/login",
    "proxy": "usr:pwd@ip:port",
    "sitekey": "0x4AAAAAAACYaM3U_Dz-4DN1"
}
```

#### turnstile action type
```json
{
    "href": "https://app.ogcom.xyz/signup?step=first",
    "proxy": "usr:pwd@ip:port",
    "sitekey": "0x4AAAAAAASTIy9n6lEJjrIE",
    "action": "verification_code",
    "explicit": true
}
```

### Response Data (JSON)

| Parameter Name          | Type        | Description                            |
|--------------|-----------|-------------------------------|
| `status`     | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`        | `String`  | `Chinese description of the result`                    |
| `id`         | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data.cookies` | `String`  | `Cookies returned after successful verification`          |
| `data.token` | `String`  | `Token returned after successful verification (used for turnstile)`               |
| `cost`       | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
"cost": "3380.01ms",
"data": {
"token": "xxx",
"cookies": "xxx=xxx;"
},
"id": "bc174976-81b2-418e-a6e3-9f7c0bbd41ae",
"msg": "验证成功",
"status": 1
}
```

### Call Example

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import CloudFlareCracker

cracker = CloudFlareCracker(
user_token="xxx",
sitekey="0x4AAAAAAACYaM3U_Dz-4DN1",
href="https://visa.vfsglobal.com/chn/zh/deu/login",
proxy="usr:pwd@ip:port",
debug=True,
)
ret = cracker.crack()
print(ret)
```
