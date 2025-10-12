[`Back to Home`](en.md)    [`Previous`](kasada.md)    [`Next`](shape.md)    [`中文文档`](../zh-CN/datadome.md)

## Datadome

### Description
* Parameter invocation is very complex, strongly recommend using `pynocaptcha` directly, see the python example below!!!

* When you see `datadome` in `cookies`, it means `datadome` verification exists, with three cases, for example:
  * When you want to access `https://www.vinted.com/`, use proxy to request `https://www.vinted.com/`:
    * Status code is not `403` (`seamless mode`): 
      * Open f12 and check if there are URLs ending with `/js/` and API response similar to:
      ```json
      {
        "status": 200,
        "cookie": "datadome=66wPBABk21P4x28BLuVse__8_z141EPJEjbgi1HBvNGBcHmX91OT1Z9Z63G4x_suPlRPQ_tgwljYmI5mWxpmkMJ3pKrcnAVKHZs2ymS_2O4nM5wEblvP~~nK3orSol0W; Max-Age=31536000; Domain=.soundcloud.com; Path=/; Secure; SameSite=Lax"
      }
      ```
      For `seamless` verification type, you must pass `js_url` (the URL ending with `/js`). This mode will return a `did` parameter in the `extra` field of our API response, which is very important for subsequent `datadome` verifications on this page!!!
      * If the homepage is `seamless mode`, then subsequent key data APIs (such as `login`, `query`, etc.) will carry the `datadome` cookie and return a response similar to:
      ```json
      {
        "url": "https://geo.captcha-delivery.com/captcha/?initialCid=AHrlqAAAAAMAqpOrr0GfIWgAudQ9Vg==&cid=w9vlJ4Xaf117hm82ORPnno7AnVvPPCoZ2gCDLj~Nch09ENObNXSzDWFekvMpp8ScynMSrB3~jsXcFtU9Y8mhOUscfnu1k_a~4_GMyGRE29_Gy~skFDqfX8tQJv1Va5Fv&referer=http%3A%2F%2Fapi-auth.soundcloud.com%2Fweb-auth%2Fidentifier%3Fq%3Desbiya1%2540gmail.com%26client_id%3D1q3v4x1lu3DpcWb4fAz0urivByipMEMK&hash=7FC6D561817844F25B65CDD97F28A1&t=fe&s=48134&e=faa8c1fb03676ac05d3bbe1d876a2d60168a7a2bab3adb5366483fc829465498"
      }
      ```
      To bypass this captcha, you need to pass `href` (current browser page URL), `captcha_url` (the URL in the response), as well as the `did` parameter returned by seamless mode, and `cookies: {"datadome": 'datadome from seamless mode'}`. This means if you use the `datadome` cookie from seamless mode to access your target data API and get slider or device captcha mode again, you need to pass `href`, `captcha_url`, `did`, `cookies`.
    ![Seamless captcha example](/images/datadome/js.png)
    * Status code `403` (`device verification mode`): 
      * If entering the target page directly redirects to device verification page or after bypassing slider captcha you are redirected to this verification, then it's `interstitial` device verification mode, please pass parameter `interstitial: true`
    ![Device verification example](/images/datadome/interstitial.png)
    * Status code `403` (`slider captcha`):
      * If entering the target page directly redirects to slider captcha page, then it's `captcha` slider captcha mode
    ![Slider captcha example](/images/datadome/captcha.png)

  * In short, first request your target page URL, if status code is `200` use seamless mode, if `403` use captcha mode, similar to the following pseudo-code:

  ```python
  # Request target page href
  resp = session.get(href, headers=headers)
  
  # Status code 200 is seamless verification mode
  if resp.status_code == 200:
      res = DatadomeCracker(
          user_token=USER_TOKEN,
          href=href,
          user_agent=user_agent,
          js_url="https://dd.vinted.lt/js",
          js_key=js_key,
          proxy=proxy,
      ).crack()
  # Status code 403, specify interstitial as true to ensure bypassing all datadome captcha modes encountered, get final valid datadome
  elif resp.status_code == 403:
      res = DatadomeCracker(
        user_token=USER_TOKEN,
          href=href,
          user_agent=user_agent,
          interstitial=True,
          proxy=proxy,
      ).crack()
  ```

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `Universal` | `http://api.nocaptcha.io/api/wanda/datadome/universal` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Page URL that triggers datadome verification`    | `Yes` |
| `proxy`    | `String`  | `No need to keep proxy consistent, if passing proxy please use overseas proxy, format: ip:port or usr:pwd@ip:port (contact admin if issues)` | `Yes` |
| `js_url`    | `String`  | `Required for js mode, API ending with /js/ that returns datadome cookie, e.g.: https://dwt.soundcloud.com/js/`    | `No` |
| `js_key`    | `String`  | `Required for js mode, search for ddjskey value in f12, e.g.: E6EAF460AA2A8322D66B42C85B62F9`    | `No` |
| `captcha_url`    | `String`  | `"url": "/captcha?initCid=xxx" triggered by post(xhr) API`    | `No` |
| `interstitial`    | `Boolean`  | `Whether interstitial device verification mode will be triggered, default false`    | `No` |
| `user_agent` | `String`  | `Custom user_agent, must keep user-agent consistent`       | `No` |
| `did` | `String`  | `Fingerprint ID returned by js mode (in extra property), pass this parameter for subsequent slider captcha from xhr APIs`       | `No` |
| `cookies` | `String`  | `Current page cookies`       | `No` |
| `timeout` | `Integer`  | `Verification timeout`       | `No` |

### Response Data (JSON):

#### Successful Response

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data.datadome`   | `String`  | `The available datadome cookie returned after successful verification, can be used for subsequent verification APIs`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "4635.12ms",
  "data": {
    "datadome": "HYvnTVSxppxMMrSk_Z_MOHoSKkQRd2ppQr~pOeo2nDlL7Lg7QBwb2ew5OYQxSSSH1CR9NzO78A25KHM7kLV6OydtvwvJZ773Jil1mPC7ZoFSQQDrDYVeHZtjq_BWUai6"
  }
}
```

### Call Example

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
import re
from utils import USER_TOKEN, get_idea_proxy
from pynocaptcha import magneto, crack_datadome


def checkbalance(session: magneto.Session, extra):
    """
    Subsequent target API request to be performed
    """
    data = {
        'language': 'en-ca',
        'csrfmiddlewaretoken': extra['csrfmiddlewaretoken'],
        'card_number': '98082560015032626594919',
        'pin': '4632',
        'g-recaptcha-response': 'true',
    }
    
    headers = {
        'accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
        'accept-language': extra['accept-language'],
        'content-type': 'application/x-www-form-urlencoded',
        'origin': 'https://homedepot-ca.cashstar.com',
        'priority': 'u=0, i',
        'referer': 'https://homedepot-ca.cashstar.com/reload/',
        'sec-ch-ua': extra['sec-ch-ua'],
        'sec-ch-ua-mobile': '?0',
        'sec-ch-ua-platform': extra['sec-ch-ua-platform'],
        'sec-fetch-dest': 'document',
        'sec-fetch-mode': 'navigate',
        'sec-fetch-site': 'same-origin',
        'sec-fetch-user': '?1',
        'upgrade-insecure-requests': '1',
        'user-agent': extra['user-agent']
    }
    return session.post(
        'https://homedepot-ca.cashstar.com/reload/',
        headers=headers,
        data=data, 
    )


def parse_index(resp, extra):
    """
    Parse data obtained from href homepage response source code
    """
    token = re.search(r'name="csrfmiddlewaretoken" value="(.*?)"', resp.text)[1]
    extra['csrfmiddlewaretoken'] = token


session, resp, extra = crack_datadome(
    user_token=USER_TOKEN,
    href='https://homedepot-ca.cashstar.com/reload/',
    verifiers=[
        checkbalance
    ],
    parse_index=parse_index,
    proxy=get_idea_proxy("hk"),
    debug=True
)

print(resp.text)
```
