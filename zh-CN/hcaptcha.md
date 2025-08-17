---

[`返回首页`](../README.md) [`上一页`](recaptcha_app.md) [`下一页`](incapsula.md) [`English Version`](../en-US/hcaptcha.md)

## hCaptcha

### 如何判断是否是企业版

🚨🚨🚨 如果你获取到值 但网站校验不通过 这说明该网站使用的是企业版 你可以先尝试使用下方文档标注的  **_Enterprise_** 字段 如果不行也可以联系管理员

### referer 参数说明

🚨🚨🚨 触发页面地址，✅ 请复制浏览器上显示的完整地址 ✅，不要改动，更不要去开发者工具 ❌ 里去找。
或者找到下图的包, host 参数的值, referer 填写为 http://{host} 如下图所示, 例如: http://democaptcha.com
![hcaptcha](/images/hcaptcha/img.png)

### Request URL（POST）:

| 版本                  | 接口地址                                               |
| --------------------- | ------------------------------------------------------ |
| `通用版（universal）` | `http://api.nocaptcha.io/api/wanda/hcaptcha/universal` |

### Request Headers:

| 参数名         | 说明                                                                                                   | 必须 |
| -------------- | ------------------------------------------------------------------------------------------------------ | ---- |
| `User-Token`   | `用户密钥, 主页获取`                                                                                   | `是` |
| `Content-Type` | `application/json`                                                                                     | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)` | `否` |

### POST Data（JSON）:

| 参数名           | 类型      | 说明                                                                                                                  | 必须 |
| ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------- | ---- |
| `sitekey`        | `String`  | `hcaptcha 对接 key`                                                                                                   | `是` |
| `referer`        | `String`  | `见上文参数说明`                                                                                                      | `是` |
| `rqdata`         | `String`  | (_Enterprise_) `验证码配置接口有返回 captcha_rqdata、captcha_rqtoken 的请携带该值(如 discord 加频道)`                 | `否` |
| `proxy`          | `String`  | `如需要请传 ip:port 或 usr:pwd@ip:port 或 socks5://ip:port (如果有问题联系管理员)`                                    | `否` |
| `region`         | `String`  | `当传入 proxy 参数时, 请传入代理的地区, 如: hk, sg`                                                                   | `否` |
| `invisible`      | `Boolean` | `触发验证码时是否能看见点击框（或 是否无感验证码）, 默认 false`                                                       | `否` |
| `need_ekey`      | `Boolean` | `是否需要返回 `E0_ey...`, 默认 false`                                                                                 | `否` |
| `preflight_uuid` | `String`  | (_Enterprise_) `预请求ID, 用于保持与业务的上下文代理地区, UserAgent等数据相同` [#预请求接口](./hcaptcha_preflight.md) | `否` |

### Response Data（JSON）:

| 参数名                     | 类型      | 说明                                                          |
| -------------------------- | --------- | ------------------------------------------------------------- |
| `status`                   | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断`                |
| `msg`                      | `String`  | `调用结果中文说明`                                            |
| `id`                       | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`                     |
| `data.generated_pass_UUID` | `String`  | `验证通过返回的 uuid(P1_xxx/F1_xxx) 凭证, 可用于后续验证接口` |
| `data.ekey`                | `String`  | `验证通过返回的 key(E0_xxx), 可用于后续验证接口`              |
| `cost`                     | `String`  | `验证耗时（毫秒）`                                            |

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

### 调用示例

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
