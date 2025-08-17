------
[`Back to Home`](en.md)    [`Previous`](recaptcha.md)    [`Next`](hcaptcha.md)    [`中文文档`](../zh-CN/recaptcha_app.md)

## ReCaptcha

### Request URL (POST):

| Version           | Interface URL                                                |
|-------------------|----------------------------------------------------------|
| `app`             | `http://api.nocaptcha.io/api/wanda/recaptcha/app`      |

### Request Headers:

| Parameter Name    | Description                                                                                                                     | Required |
|----------------|----------------------------------------------------------------------------------------------------------------------|---------|
| `User-Token`   | `User key, obtain from homepage`                                                                                                   | `Yes`   |
| `Content-Type` | `application/json`                                                                                                           | `Yes`   |
| `Developer-Id` | `Developer ID, used by developer users, the string from the homepage invitation link (e.g., xxx/register?c=abcdef, then abcdef is the Developer ID)` | `No`    |

### POST Data (JSON):

| Parameter Name  | Type      | Description                                                                                                                                                           | Required |
|----------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| `sitekey`      | `String` | `Google verification docking key (k value of the anchor/reload interface)`                                                                                                     | `Yes`   |
| `apk`          | `String` | `apk package name of the app`                                                                                                                                         | `Yes`   |
| `action`       | `String` | `Value of action in the captcha trigger page search grecaptcha.execute(client, {action: action}), needed only for v3`                                                        | `No`    |
| `user_agent`   | `String` | `User agent used in the request process. Some websites require consistency throughout. Please send the captured mobile ua.`                     | `No`    |
| `internal`     | `Boolean`| `Whether to use domestic proxies during the verification process. Default is true (It's suggested to try false first to use foreign proxies for a smoother experience)` | `No`    |

#### json example

```
{
    sitekey: '6Le7yQ4jAAAAAJKn2hbQu_ydG6Hw2-27yvkfKdVJ',
    apk: 'com.viber.voip',
    action: "custom_Registration",
    user_agent: 'Mozilla/5.0 (Linux; Android 7.1; Pixel XL Build/NDE63H; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/103.0.5060.129 Mobile Safari/537.36',
}
```

### Response Data (JSON)

| Parameter Name  | Type      | Description                                         |
|----------------|----------|----------------------------------------------------|
| `status`       | `Integer`| `Whether the call was successful. 1 for success, 0 for failure. Use this value for judgment.` |
| `msg`          | `String` | `Explanation for the call result in English`          |
| `id`           | `String` | `ID for this request (Unique, can be used for subsequent record queries)`           |
| `data.token`   | `String` | `Returned token after successful verification`          |
| `cost`         | `String` | `Verification time taken (in milliseconds)`               |

```
{
  "cost": "1380.01ms",
  "data": {
    "token": "03AFY_a8UL3OTinrQHai6iE4c9l--oZAtVsDsAGBtijmv3QgBWmeOWWvbJvZ_DPT8p2ttvUlr4FmE5gDSTON0f4mPpYqxwPdVYxRbC0nmLuZJ0k9UmOjiK4HgUShuFu4RL7w1hyoFQ1YbUpLtW-KuAqC1KSs4GGBrI3k4Cx4u7e57DQPhVdzzpVGqQjGq9ZnI5YY9546_jRybKrIv2FMLeIkvcOJnCPUTnUREewSn7VO1bCvpdAP3Wj8DoH8jtv-RXij9aypLnFcpLGMTwrJOCE9z2U7As7AzAxcMnVEr9AWyKipKj4t-A2m77uNvHv-f1XhSMNI_Dk4bIYLe5n0N-STCLUc5tFfPc5rtuNQdoTRxdl6ie9gOpzpUyg6dwcA3tEiERya9Tej-6FMpwo4G4F61u8buUAMgCVn-4OoAB9AfH5mjN3GapQf3Yc_mK2u99xErSwEgwuhVsBsMzC22JiVaqHWO8EOzDRso6AMpUmuZw27b3Kl8IhFH1OiIL9WdfMfEXtEDgUFZxL085MxyS_mv5iGDbcxLkXN5PupgT2ieoQ8grbHsbHWF1-9Un0cxF5MVfmIilzbSUtItZ7i2SZcJZlPOG86D1CKby2T7nnprtoVd7hAN4r5yTnQ52f_8oShEKd3n0ArHsfti4TXPuVgafP8jp4uIkgK3YDlF2QvnnuGeEq58dZ91nllOQOBnzc_GiNLvd1h8XrZxexZ2eI_LDueF2p4uSWQBDLXloHV_2lmDf5QsDcUJy46JyhlehLK-MOzLt-BDJ9wVJdtHhY_GT-IymY757nYurqWCLdY7k7ofeIcd51I35Hz88VADyp_EYtRzmd5CIRX_sHx4rlw7Yw1khFG6Ktw-7bRd1nSw1rNZlwFIxvLk4Bgp9WGZS8rqRCKIJgAMAJOzt872i1P9GQ3k6Ee5nn8qTs0CmpckzrvqJLzexQfM69G-A1O0s99PMn0Hr5ruUU_jsj3rtzWu1zXr0soPtArvN2tvTLsRSARIL1G5unTeX7YpURkbVVkmaa08oqpR7eIFVO7I7SZ99jk-DJdXSL5uUs3ZcIe8fzIp_hGtCkSQIrHrB0F5anyER7ZdBH1ynT7aFltOlikAWB_s4lTIYZk7VDUrrwKOSMI3SMHus7BxKZNanhTO34c_9s62t9FRrLaiQfTXy4ZUlCgVAkWt1f_6lrRwj9VZDQRiplJQwIIDpT2jhXrgGLdqIjOBtJ2Doy3Gx4dkpPCuquqhnzyvFCEJdyG-QKaONu4tbFjbUWB7TwIgREUVdrR5k3YN21sVTY2yvNZjc8YVCw-YXIYygZE6OpPJUIhxxXtB55xpxQ2THITBlkIu5QmBtQ4lXi3GBbq_UKB_Lxn5SVjK88yTZ3TD3m8nfH4WDdb4c36Ff4lpGEEIsZtS7U11FqTGu_xv-dgIYN0-t1tK8TKhJLHDG8nRwady2Xiq190yBXI3sDDcumMpCYqf2wE6Hmu2gnLRGlqPYdsnlC0JQMoeUTHhdEBslQb4iPV_0azLHp_kCEZvYZYalmyIibmmI2O9qY9gROUHt7NRLl_-T3mxr7cdRP2kG801i8Y87nY6PVllAs5JCVcRcMu3UXxvgianbXX_VVsuEf3Y-uxoRV7LKHYesm7tsxxcDwUtZiWzjY0PTCMUXgAjWrJDs-w9VUQGGeOWxqebTx-Mg_fTEXvqkmChhFTyBRDF0yQnMx0KaCnOogEK2XxI_ts_M-DWrXFBHUZa9a9a09T-73kpJqlVCcwgQjV-LhyaeQxUIT02_diqL-xM00AWhJmqwnojmmP6cXU34"
  },
  "id": "bc174976-81b2-418e-a6e3-9f7c0bbd41ae",
  "msg": "Verification successful",
  "status": 1
}
```

### CURL command

```
curl -L 'http://api.nocaptcha.io/api/wanda/recaptcha/app' \
 -H 'User-Token: xxx' \
 -H 'Content-Type: application/json' \
 --data-raw '{"sitekey": "6Lcxp2UaAAAAABkIC5izuDmTEeXYfgfaoQ9v69Q4", "apk": "com.viber.voip", "action": "custom_Registration", "internal": false}' 
```

### Usage example

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import ReCaptchaAppCracker

cracker = ReCaptchaAppCracker(
    user_token="xxx",
    sitekey='6Le7yQ4jAAAAAJKn2hbQu_ydG6Hw2-27yvkfKdVJ',
    apk='com.viber.voip',
    action="custom_Registration",
    user_agent='Mozilla/5.0 (Linux; Android 7.1; Pixel XL Build/NDE63H; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/103.0.5060.129 Mobile Safari/537.36',
    debug=True,
    internal=False,
)
ret = cracker.crack()
print(ret)
```

I've translated the markdown as requested. If you have further adjustments or questions, let me know!
