------

[`返回首页`](../README.md)    [`上一页`](cloudflare.md)   [`下一页`](perimeterx.md)    [`English Version`](../en-US/aws.md)

## Aws Waf

### 价格说明
* 仅无感模式仅消耗 150 点, 需要传入 challenge_url, only_sense
* 传入代理半价折扣(无感模式不适用)

### 说明
* aws waf 验证, 通常不需要 ua/proxy 一致
* 当看到 cookies 中有 aws-waf-token 时, 代表存在 aws waf 验证, 通常以下两种情况
    * 1. 状态码 405 出现验证码(直接get请求触发验证码可以直接传入href, post或其他情况请将触发验证的html提交)
    ![验证码样例](/images/aws/img.png)
    * 2. 无感验证, 但是 html 中有 challenge.js, cookies 中有 aws-waf-token(此时传入 challenge_url(重定向后地址中有 .token 的链接或者包含 challenge.compact.js 的链接), only_sense 享折扣)
    ![无感验证样例](/images/aws/img2.png)
    * 3. 不是直接请求首页后触发, 而且点击按钮后出现验证码, 且参数中有 api_key, 此时需要传入 challenge_url(地址中有 .token 的链接), api_key
    ![验证码样例2](/images/aws/img3.png)
    * 4. 如 www.amazon.com 触发验证码但不需要 aws-waf-token, 需要 captcha-voucher, 此时 challenge_url 传入包含 captcha.js 的地址, 并传入 captcha_type( problem 接口 problem 参数)
    ![验证码样例3](/images/aws/img4.png)
    ![验证码样例4](/images/aws/img5.png)

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `通用版（universal）` | `http://api.nocaptcha.io/api/wanda/aws/universal` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`       | `String`  | `触发 aws waf 验证的页面地址`    | `是` |
| `html`     | `String` | `非默认请求触发的情况可以将验证码页面html传入`       | `否` |
| `user_agent` | `String`  | `自定义 user_agent`       | `否` |
| `challenge_url` | `String`  | `无感验证时传入(重定向后地址中有 .token 的链接), 享折扣`       | `否` |
| `only_sense` | `Boolean`  | `无感验证时传入, 享折扣`       | `否` |
| `api_key` | `String`  | `见上述情况3时, 需要传入`       | `否` |
| `captcha_type` | `String`  | `见上述情况4时, 需要传入`       | `否` |

#### json 示例

```
{
    "href": "https://nft.porsche.com/onboarding@6",
}

{
    "href": "https://www.amazon.com/ap/cvf/request?arb=769b3899-80eb-4224-b47b-8af60b009d37&language=zh",
    "challenge_url": "https://ait.2608283a.us-east-1.captcha.awswaf.com/ait/ait/ait/captcha.js",
    "captcha_type": "toycarcity",
}
```


### Response Data（JSON）:

#### 提交验证（submit=true）

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.aws-waf-token`   | `String`  | `验证通过返回的可用的 aws-waf-token cookie, 可用于后续验证接口`    |
| `data.captcha-voucher` | `String`  | `验证码验证时返回的验证码凭证, 可用于后续验证接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "aws-waf-token": "xxxx"
  }
}

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

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import AwsUniversalCracker


crack = AwsUniversalCracker(
    user_token="xxx,
    href="https://www.cityline.com/Events.html",
    only_sense=True,
    challenge_url="https://9175c2fd4189.2430aa90.ap-southeast-1.token.awswaf.com/9175c2fd4189/6e83bc7a594c/challenge.js",
    debug=True
)
```

```python
from pynocaptcha import AwsUniversalCracker


cracker = AwsUniversalCracker(
    user_token="xxx",
    href="https://nft.porsche.com/onboarding@6",
    debug=True,
)
ret = cracker.crack()
print(ret)
```
