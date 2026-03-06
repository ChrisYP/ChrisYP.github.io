## Overview

**👉[For English](/en-US/en.md)👈**

### 目前支持的接口

|                           类型                           |                           说明                            | 支持同步获取结果 |    消耗点数    | 传入代理IP优惠 | 运行状态 | 独享/包月（请联系客服） |
|:------------------------------------------------------:|:-------------------------------------------------------:|:--------:|:----------:|:--------:|:----:|:------------:|
|       [recaptcha:universal](/zh-CN/recaptcha.md)       |           `ReCaptcha（v2/v3 通用版）, 直接返回 token`            |    ✅     |   `300`    |    ✅     |  ✅   |      ❌       |
|      [recaptcha:enterprise](/zh-CN/recaptcha.md)       |           `ReCaptcha（v2/v3 企业版）, 直接返回 token`            |    ✅     |   `300`    |    ✅     |  ✅   |      ❌       |
|        [recaptcha:app](/zh-CN/recaptcha_app.md)        |             `ReCaptcha（app 版本）, 直接返回 token`             |    ✅     |  `❌停止维护❌`  |    ✅     |  ❌   |      ❌       |
|        [hcaptcha:universal](/zh-CN/hcaptcha.md)        |        `Hcaptcha 通用版, 直接返回 generated_pass_UUID`         |    ✅     |   `300`    |    ✅     |  ✅   |      ❌       |
|        [incapsula:reese84](/zh-CN/incapsula.md)        |        `Incapsula 盾 reese84 通用版, 返回 solution 参数`        |    ✅     |   `210`    |    ❌     |  ✅   |      ❌       |
|      [incapsula:utmvc](/zh-CN/incapsula_utmvc.md)      |  `Incapsula 盾 __utmvc 通用版, 服务器直接无感验证 或 __utmvc cookie`  |    ✅     |   `150`    |    ❌     |  ✅   |      ❌       |
|      [incapsula:rbzid](/zh-CN/incapsula_rbzid.md)      |             `Incapsula 盾 rbzid 通用版, 返回验证参数`             |    ✅     |   `100`    |    ❌     |  ✅   |      ❌       |
|             [akamai:v2](/zh-CN/akamai.md)              |               `Akamai v2/v3, 直接返回 _abck`                |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|                [tls:v1](/zh-CN/tls.md)                 |  `tls 转发接口, 针对校验 ja3、http2 等指纹（akamai/cloudflare）的接口`   |    ✅     |   `100`    |    ❌     |  ✅   |      ❌       |
|      [cloudflare:universal](/zh-CN/cloudflare.md)      | `CloudFlare 盾通用版, 返回 cookies 或验证码提交参数(turnstile 300 点)` |    ✅     | `1000/300` |    ✅     |  ✅   |      ✅       |
|             [aws:universal](/zh-CN/aws.md)             |        `Aws Waf 盾, 返回 aws-waf-token(仅无感 150 点)`         |    ✅     | `300/150`  |    ✅     |  ✅   |      ❌       |
|      [perimeterx:universal](/zh-CN/perimeterx.md)      |             `Perimeterx 盾通用版, 返回 _px2、_px3`             |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|             [kasada:ct](/zh-CN/kasada.md)              |                `Kasada 盾, 返回 x-kpsdk-ct`                |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|             [kasada:cd](/zh-CN/kasada.md)              |                `Kasada 盾, 返回 x-kpsdk-cd`                |    ✅     |    `50`    |    ❌     |  ✅   |      ❌       |
|        [datadome:universal](/zh-CN/datadome.md)        |            `Datadome 盾, 返回 datadome cookie`             |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|              [shape:v1](/zh-CN/shape.md)               |              `Shape 盾 v1 版本, 返回请求头或表单加密参数`              |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|              [shape:v2](/zh-CN/shape.md)               |              `Shape 盾 v2 版本, 返回请求头或表单加密参数`              |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|          [vercel:universal](/zh-CN/vercel.md)          |            `Vercel 盾通用版本, 返回 _vcrcs cookie`             |    ✅     |   `150`    |    ❌     |  ✅   |      ❌       |
| [discord:join_channel](/zh-CN/discord_join_channel.md) |                      `discord 加频道`                      |    ✅     |   `500`    |    ❌     |  ✅   |      ❌       |
|          [site:unlocker](/zh-CN/unlocker.md)           |                         `网站解锁器`                         |    ✅     |   `1000`   |    ❌     |  ✅   |      ✅       |
|        [funcaptcha:sense](/zh-CN/funcaptcha.md)         |                `Funcaptcha 无感`                |    ✅     |   `500`    |     ❌     |  ✅   |      ✅       |
|        [castle:universal](/zh-CN/castle.md)         |                `Castle`                |    ✅     |   `500`    |     ❌     |  ✅   |      ✅       |

### 传入代理说明

* 使用账密认证或者无需白名单认证的代理, 格式请传 ip:port 或 usr:pwd@ip:port
* 使用粘性/会话代理(即 n 分钟内 ip 保持不变的类型)
* 注意代理使用次数, 不要固定一个代理

![proxy](/images/proxy.png)

### 名词说明

* `点数`: 服务消耗的点数, `1美金 = 66,000 点` (`$1 = 66,000 points`)
* `User-Token`: 用户令牌, 调用服务需要传入该参数, 在用户主页可以查看
* `Developer-ID`: 开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 `abcdef` 为开发者 ID)

### 传入代理折扣说明

代理折扣每个服务为一个固定值（通常为服务价格的 `20%` 如 `1000点` 代理折扣 `200点` 实际消费为 `800点`）

### 等级说明

|   等级    | 消费点数            |  消费($)   |   折扣   | 折扣示例(1000点实际消费) | 代理折扣示例(如支持)(1000点实际消费) |
|:-------:|:----------------|:--------:|:------:|:---------------:|:----------------------:|
| `VIP 0` | `0`             |   `0`    | `100%` |     `1000`      |         `800`          |
| `VIP 1` | `99,000,000`    |  `1500`  | `90%`  |      `900`      |         `700`          |
| `VIP 2` | `247,500,000`   |  `3750`  | `80%`  |      `800`      |         `600`          |
| `VIP 3` | `594,000,000`   |  `9000`  | `70%`  |      `700`      |         `500`          |
| `VIP 4` | `990,000,000`   | `15000`  | `60%`  |      `600`      |         `400`          |
| `VIP 5` | `1,980,000,000` | `30000`  | `50%`  |      `500`      |         `300`          |
| `VIP 6` | `3,300,000,000` | `50000`  | `40%`  |      `400`      |         `200`          |
| `VIP 7` | `6,600,000,000` | `100000` | `30%`  |      `300`      |         `100`          |

### 返利说明

* 邀请返利: 直接邀请的用户消费时, 得消费的 `20%` 返利（即 `A` 邀请 `B`, `B` 每消耗 `300` 点, `A` 得 `60` 点返利）
* 开发者返利: 用户消费调用服务接口时传入开发者 ID, 开发者得消费的 `20%` 返利（此时邀请者不得返利）
* 开发者返利优先级 > 邀请返利（即 `A` 邀请 `B`, `B` 填写 `C` 开发者 ID, `C` 得 `20%` 返利, `A` 不得返利）
* 调用时开发者 ID 填写自己, 无法获得返利

### 返利使用

* 转余额: `1:1` 转换为余额, 用于服务消费
* 提现: 目前支持 `10U` `20U` `50U` `100U` 四个额度的提现, 仅支持 `BSC链 (BEP20)` 地址提现

### 钱包数据查询接口

```text
http://api.nocaptcha.io/api/get_user_balance?user_token={User-Token}&nickname={nickname}
```

| 参数名          | 类型       | 说明                | 必须  |
|--------------|----------|-------------------|-----|
| `User-Token` | `String` | `用户令牌xxxx-xxx...` | `是` |
| `nickname`   | `String` | `登录邮箱abc@xxx.com` | `是` |

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