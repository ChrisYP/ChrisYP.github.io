[`Back to Home`](en.md)    [`Next`](recaptcha_app.md)    [`中文文档`](../zh-CN/recaptcha.md)

## ReCaptcha

### Frequently Asked Questions

* How to distinguish between `v2` and `v3`?
    * Unlike other platforms, we only differentiate between the regular version and the enterprise version. The
      differences between `v2` and `v3` are:
        * `v3` ends at the `reload` interface, and its `size` parameter is typically `invisible` (please refer to the
          web interface). It also requires the `action` parameter. Open `f12`, search for `grecaptcha.execute` and find
          the `action` value in the argument object of this function. Input it into the `action` parameter.
        * After the `v2` `reload` interface, you need to request the `userverify` interface. Its `size` is
          usually `normal` (please refer to the web interface), and there's no need to pass the `action` parameter.
        * The regular and enterprise versions have identical interface parameters. The only difference is the request
          route.

* How to differentiate between the `Regular Version` and the `Enterprise Version`?
    * Regular Version: `anchor` interface route: `/recaptcha/api2/anchor`
    * Enterprise Version: `anchor` interface route: `/recaptcha/enterprise/anchor`

* For enterprise versions with an `s` value (like `steam`), why doesn't the token obtained from the interface work?
    * It's related to the quality of the proxy you're using. Please try using your local IP or switch the proxy. If it
      still doesn't work, contact customer service.

### Why Choose Us

* Universality: Currently known websites can pass the verification (including enterprise versions with an `s` value that
  other platforms can't handle, like `steam`). The interface is unified for `v2` and `v3`.
* Ultimate speed: Most interfaces on the market are asynchronous. You need to first create a task, then obtain the task
  ID, and constantly poll to get the verification result. Sometimes, this can take up to 1 minute, which is
  unacceptable. Our interface uses `pure algorithm` calculations, `protocol submissions`, and
  provides `synchronous returns`. The average return for `v3 invisible` and `v2 nocaptcha` is `1s`, while `v2` other
  image-click types are fastest at `2s` and will not exceed `10s` (this also depends on the speed of the proxy).
* High Availability: The `v3` score is high. For most high-risk control sites (such as various enterprise versions),
  the `token` value produced by our interface can successfully pass risk control and obtain target data.
* Stability: Timely updates (no more than two hours) to better support your business.

### Request URL (POST):

|       Version        |                      Interface URL                       |
|:--------------------:|:--------------------------------------------------------:|
| `Universal Version`  | `http://api.nocaptcha.io/api/wanda/recaptcha/universal`  |
| `Enterprise Version` | `http://api.nocaptcha.io/api/wanda/recaptcha/enterprise` |
|       `Steam`        |   `http://api.nocaptcha.io/api/wanda/recaptcha/steam`    |

### Request Headers:

| Parameter Name |                                                                       Description                                                                       | Required |
|:--------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|
|  `User-Token`  |                                                         `User key, obtained from the homepage`                                                          |  `Yes`   |
| `Content-Type` |                                                                   `application/json`                                                                    |  `Yes`   |
| `Developer-Id` | `Developer ID, used by developer users. The string in the user homepage invitation link (e.g., xxx/register?c=abcdef, then abcdef is the developer ID)` |   `No`   |

### POST Data (JSON):

| Parameter Name |   Type    |                                                                                       Description                                                                                        | Required |
|:--------------:|:---------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|
|   `sitekey`    | `String`  |                                                        `Google verification docking key (k value of the anchor/reload interface)`                                                        |  `Yes`   |
|   `referer`    | `String`  |             `🚨🚨🚨 Trigger page address. ✅Please copy the full address displayed on the browser✅. Do not alter it, and definitely don't search for it in developer tools❌.`             |  `Yes`   |
|     `size`     | `String`  |             `Validation type (e.g. invisible/normal, usually there are only these two choices, specifically check the size value of the anchor interface, they must match).`             |  `Yes`   |
|    `title`     | `String`  |                                                     `Trigger the page's title (open the console with F12, type in document.title).`                                                      |  `Yes`   |
|    `action`    | `String`  |                      `For the verification code trigger page, search grecaptcha.execute(client, {action: action}), where the action value is only required for v3.`                      |   `No`   |
|     `ubd`      | `Boolean` |                                                 `Check whether the verification route is the special 'ubd' type. The default is false.`                                                  |   `No`   |
|      `s`       | `String`  |                          `Steam project's 's' value. It's generally not required to be filled in.  Currently, only the Steam project needs it to be filled in.`                          |   `No`   |
|      `sa`      | `String`  |              `some website anchor interface route has 'sa'. It's generally not required to be filled in. Currently. only some Enterprise Version needs it to be filled in.`              |   `No`   |

#### Parameter Lookup Steps

1. ### Method 1 [`【🔥Highly Recommended🔥】 Get All Parameters Using the Plugin`](plugin.md)

2. ### Method 2, Get Parameters Inside the Developer Tools.

- Search for the `anchor` interface and obtain the `k`, `size`, and `hl` parameters. The `k` value is the `sitekey`.
  Fill in the corresponding field accordingly. If `hl` is `zh-CN`, you can leave it blank, as shown in the picture
  below:
    * ![步骤1](/images/recaptcha/arg1.png)


- Switch to the `console`, type in `document.title`, and fill the output value into the title field.

    * ![步骤3](/images/recaptcha/arg3.png)


- If, according to the aforementioned `v2`/`v3` differentiation method, you determine that the verification is `v3`, you
  will also need to find and fill in the `action` parameter. The method to find it is as follows:

    - Method 1: Press `F12`, search for `.execute(` in the standard version or `.enterprise.execute(` for the enterprise
      version. Look for the `action` parameter in the code, as shown in the picture below. If you can't find it, please
      use Method 2.
        * ![步骤5](/images/recaptcha/arg5.png)

    - Method 2: Press `F12`, enter `debug(grecaptcha.execute)` for the standard version
      or `debug(grecaptcha.enterprise.execute)` for the enterprise version. Click on login or complete the verification,
      and wait for the breakpoint to trigger. Copy the value of `action` from the `Scope`, as shown in the picture
      below:
        * ![步骤6](/images/recaptcha/arg6.png)
        * ![步骤7](/images/recaptcha/arg7.png)


- Check if the verification route is of the `ubd` type (currently only seen in the `enterprise version` of one website).
  If it is `ubd`, please fill in the `ubd` parameter as `true`. Otherwise, fill in `false` or leave it blank:
    * ![步骤8](/images/recaptcha/arg8.png)

#### anchor Example

[![anchor Example](/images/recaptcha/anchor.jpg)])

#### JSON Example

```
{
  "referer": "https://www.trustpilot.com/",
  "sitekey": "6Lcxp2UaAAAAABkIC5izuDmTEeXYfgfaoQ9v69Q4",
  "size": "invisible",
  "title": "Login",
  "action": "login",
}
```

### Response Data (JSON)

| Parameter Name | Type      | Description                                                                    |
|----------------|-----------|--------------------------------------------------------------------------------|
| `status`       | `Integer` | `Call success: 1 for success, 0 for failure. Please use this value to judge.`  |
| `msg`          | `String`  | `Description of the call result in Chinese`                                    |
| `id`           | `String`  | `Request ID for this call (unique, can be used for subsequent record queries)` |
| `data.token`   | `String`  | `Token returned upon successful verification`                                  |
| `cost`         | `String`  | `Verification duration (in milliseconds)`                                      |

```json
{
  "cost": "1380.01ms",
  "data": {
    "token": "03AFY_a8UL3OTinrQHai6iE4c9l--oZAtVsDsAGBtijmv3QgBWmeOWWvbJvZ_DPT8p2ttvUlr4FmE5gDSTON0f4mPpYqxwPdVYxRbC0nmLuZJ0k9UmOjiK4HgUShuFu4RL7w1hyoFQ1YbUpLtW-KuAqC1KSs4GGBrI3k4Cx4u7e57DQPhVdzzpVGqQjGq9ZnI5YY9546_jRybKrIv2FMLeIkvcOJnCPUTnUREewSn7VO1bCvpdAP3Wj8DoH8jtv-RXij9aypLnFcpLGMTwrJOCE9z2U7As7AzAxcMnVEr9AWyKipKj4t-A2m77uNvHv-f1XhSMNI_Dk4bIYLe5n0N-STCLUc5tFfPc5rtuNQdoTRxdl6ie9gOpzpUyg6dwcA3tEiERya9Tej-6FMpwo4G4F61u8buUAMgCVn-4OoAB9AfH5mjN3GapQf3Yc_mK2u99xErSwEgwuhVsBsMzC22JiVaqHWO8EOzDRso6AMpUmuZw27b3Kl8IhFH1OiIL9WdfMfEXtEDgUFZxL085MxyS_mv5iGDbcxLkXN5PupgT2ieoQ8grbHsbHWF1-9Un0cxF5MVfmIilzbSUtItZ7i2SZcJZlPOG86D1CKby2T7nnprtoVd7hAN4r5yTnQ52f_8oShEKd3n0ArHsfti4TXPuVgafP8jp4uIkgK3YDlF2QvnnuGeEq58dZ91nllOQOBnzc_GiNLvd1h8XrZxexZ2eI_LDueF2p4uSWQBDLXloHV_2lmDf5QsDcUJy46JyhlehLK-MOzLt-BDJ9wVJdtHhY_GT-IymY757nYurqWCLdY7k7ofeIcd51I35Hz88VADyp_EYtRzmd5CIRX_sHx4rlw7Yw1khFG6Ktw-7bRd1nSw1rNZlwFIxvLk4Bgp9WGZS8rqRCKIJgAMAJOzt872i1P9GQ3k6Ee5nn8qTs0CmpckzrvqJLzexQfM69G-A1O0s99PMn0Hr5ruUU_jsj3rtzWu1zXr0soPtArvN2tvTLsRSARIL1G5unTeX7YpURkbVVkmaa08oqpR7eIFVO7I7SZ99jk-DJdXSL5uUs3ZcIe8fzIp_hGtCkSQIrHrB0F5anyER7ZdBH1ynT7aFltOlikAWB_s4lTIYZk7VDUrrwKOSMI3SMHus7BxKZNanhTO34c_9s62t9FRrLaiQfTXy4ZUlCgVAkWt1f_6lrRwj9VZDQRiplJQwIIDpT2jhXrgGLdqIjOBtJ2Doy3Gx4dkpPCuquqhnzyvFCEJdyG-QKaONu4tbFjbUWB7TwIgREUVdrR5k3YN21sVTY2yvNZjc8YVCw-YXIYygZE6OpPJUIhxxXtB55xpxQ2THITBlkIu5QmBtQ4lXi3GBbq_UKB_Lxn5SVjK88yTZ3TD3m8nfH4WDdb4c36Ff4lpGEEIsZtS7U11FqTGu_xv-dgIYN0-t1tK8TKhJLHDG8nRwady2Xiq190yBXI3sDDcumMpCYqf2wE6Hmu2gnLRGlqPYdsnlC0JQMoeUTHhdEBslQb4iPV_0azLHp_kCEZvYZYalmyIibmmI2O9qY9gROUHt7NRLl_-T3mxr7cdRP2kG801i8Y87nY6PVllAs5JCVcRcMu3UXxvgianbXX_VVsuEf3Y-uxoRV7LKHYesm7tsxxcDwUtZiWzjY0PTCMUXgAjWrJDs-w9VUQGGeOWxqebTx-Mg_fTEXvqkmChhFTyBRDF0yQnMx0KaCnOogEK2XxI_ts_M-DWrXFBHUZa9a9a09T-73kpJqlVCcwgQjV-LhyaeQxUIT02_diqL-xM00AWhJmqwnojmmP6cXU34"
  },
  "id": "bc174976-81b2-418e-a6e3-9f7c0bbd41ae",
  "msg": "验证成功",
  "status": 1
}
```

### CURL command

```
curl -L 'http://api.nocaptcha.io/api/wanda/recaptcha/universal' \
 -H 'User-Token: xxx' \
 -H 'Content-Type: application/json' \
 --data-raw '{"sitekey": "6Lcxp2UaAAAAABkIC5izuDmTEeXYfgfaoQ9v69Q4", "referer": "https://www.trustpilot.com/", "size": "invisible", "title": "Login", "action": "login", "internal": false}' 
```

### Sample Calls

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import ReCaptchaUniversalCracker, ReCaptchaEnterpriseCracker, ReCaptchaSteamCracker

cracker = ReCaptchaUniversalCracker(
    user_token="xxx",
    sitekey="6Le6xNgUAAAAAHDXXUgcrCYACaq_K-iUTa-BIm4h",
    referer="https://visa-fr.tlscontact.com/gb/lon/login.php",
    size="invisible",
    action="login_form",
    title="Login",
    debug=True,
)
ret = cracker.crack()
print(ret)

cracker = ReCaptchaEnterpriseCracker(
    user_token="xxx",
    sitekey="6LcTV7IcAAAAAI1CwwRBm58wKn1n6vwyV1QFaoxr",
    referer="https://login.coinbase.com/",
    size="invisible",
    debug=True,
)

ret = cracker.crack()
print(ret)

cracker = ReCaptchaSteamCracker(
    user_token="xxx",
    sitekey="6LfNGb0ZAAAAAI_j6L2y1eXXWAoSbtjvccEcEq2P",
    referer="https://help.steampowered.com/zh-cn/wizard/HelpWithLoginInfo?issueid=406",
    size="normal",
    title="Steam 客服 - 我忘了我的 Steam 帐户登录名称或密码",
    debug=True,
    s=s,  # The 's' value returned by the Steam website API.
)

ret = cracker.crack()
print(ret)
```
