[`Back to Home`](en.md)    [`Previous`](cloudflare.md)    [`Next`](perimeterx.md)    [`中文文档`](../zh-CN/aws.md)

## Aws Waf

### Pricing
* Only seamless mode consumes 150 points, requires challenge_url, only_sense
* Inputting proxy gets half price discount (not applicable for seamless mode)

### Description
* AWS WAF verification, usually does not require ua/proxy consistency
* When you see aws-waf-token in cookies, it means AWS WAF verification exists, usually in the following cases:
    * 1. Status code 405 triggers captcha (direct GET request triggers captcha, you can directly pass href; for POST or other cases, please submit the HTML that triggers the verification)
    ![Captcha Example](/images/aws/img.png)
    * 2. Seamless verification, but challenge.js in HTML and aws-waf-token in cookies (pass challenge_url (redirected address contains .token or challenge.compact.js), only_sense gets discount)
    ![Seamless Verification Example](/images/aws/img2.png)
    * 3. Not triggered by direct homepage request, but appears after clicking a button, and api_key is present in parameters; pass challenge_url (address contains .token), api_key
    ![Captcha Example 2](/images/aws/img3.png)
    * 4. For www.amazon.com, captcha is triggered but aws-waf-token is not needed, requires captcha-voucher; pass challenge_url containing captcha.js, and captcha_type (problem API problem parameter)
    ![Captcha Example 3](/images/aws/img4.png)
    ![Captcha Example 4](/images/aws/img5.png)

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `Universal` | `http://api.nocaptcha.io/api/wanda/aws/universal` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`       | `String`  | `Page URL that triggers AWS WAF verification`    | `Yes` |
| `html`     | `String` | `For non-default request triggers, you can pass the captcha page HTML`       | `No` |
| `user_agent` | `String`  | `Custom user_agent`       | `No` |
| `challenge_url` | `String`  | `For seamless verification, pass (redirected address contains .token), gets discount`       | `No` |
| `only_sense` | `Boolean`  | `For seamless verification, pass, gets discount`       | `No` |
| `api_key` | `String`  | `See case 3 above, required`       | `No` |
| `captcha_type` | `String`  | `See case 4 above, required`       | `No` |

#### json example

```json
{
    "href": "https://example.com",
    "challenge_url": "https://example.com/.token...",
    "only_sense": true,
    "user_agent": "Mozilla/5.0 ...",
    "api_key": "xxxx",
    "captcha_type": "problem"
}
```

```json
{
    "href": "https://nft.porsche.com/onboarding@6"
}
```

```json
{
    "href": "https://www.amazon.com/ap/cvf/request?arb=769b3899-80eb-4224-b47b-8af60b009d37&language=zh",
    "challenge_url": "https://ait.2608283a.us-east-1.captcha.awswaf.com/ait/ait/ait/captcha.js",
    "captcha_type": "toycarcity"
}
```

### Response Data (JSON):

#### Submit Verification (submit=true)

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data.aws-waf-token`   | `String`  | `The available aws-waf-token cookie returned after successful verification, can be used for subsequent verification APIs`    |
| `data.captcha-voucher` | `String`  | `The captcha voucher returned during captcha verification, can be used for subsequent verification APIs`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "aws-waf-token": "xxxx"
  }
}
```

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "captcha-voucher": "xxxx"
  }
}
```

### Call Example

#### Nodejs

```javascript
const axios = require('axios');

async function verifyAWSWAF() {
    const response = await axios.post('http://api.nocaptcha.io/api/wanda/aws/universal', {
        href: 'https://example.com',
        challenge_url: 'https://example.com/.token...',
        only_sense: true,
        user_agent: 'Mozilla/5.0 ...',
        api_key: 'xxxx',
        captcha_type: 'problem'
    }, {
        headers: {
            'User-Token': 'your_user_token',
            'Content-Type': 'application/json',
            'Developer-Id': 'your_developer_id' // optional
        }
    });

    console.log(response.data);
}

verifyAWSWAF();
```

#### Python

```python
import requests

url = "http://api.nocaptcha.io/api/wanda/aws/universal"
payload = {
    "href": "https://example.com",
    "challenge_url": "https://example.com/.token...",
    "only_sense": True,
    "user_agent": "Mozilla/5.0 ...",
    "api_key": "xxxx",
    "captcha_type": "problem"
}
headers = {
    "User-Token": "your_user_token",
    "Content-Type": "application/json",
    "Developer-Id": "your_developer_id" # optional
}

response = requests.post(url, json=payload, headers=headers)
print(response.json())
```
