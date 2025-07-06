---

[`返回首页`](../README.md) [`English Version`](../en-US/hcaptcha_preflight.md)

## hCaptcha 预请求接口 (Enterprise)

### 什么时候应该使用

网站有明显的分数检测时, 提高验证通过率

### 说明

用于保持与业务的上下文代理地区, UserAgent 等数据相同

### 🚨🚨🚨

拿到`region`(如 `hk` `gb` `us` )之后, 传入的代理请对应该地区

### 请求地址 (POST):

| API 端点                                                    |
| ----------------------------------------------------------- |
| `http://api.nocaptcha.io/api/wanda/hcaptcha/preflight_uuid` |

### 请求头 (Request Headers):

| 参数名         | 描述               | 是否必需 |
| -------------- | ------------------ | -------- |
| `Content-Type` | `application/json` | 是       |

### POST 数据 (JSON):

| 参数名    | 类型     | 描述                | 是否必需 |
| --------- | -------- | ------------------- | -------- |
| `sitekey` | `String` | `hcaptcha 对接 key` | 是       |

### 响应数据 (JSON):

| 参数名                     | 类型      | 描述                     |
| -------------------------- | --------- | ------------------------ |
| `success`                  | `Boolean` | `调用是否成功`           |
| `data.data`                | `Object`  | `预请求返回的数据`       |
| `data.data.preflight_uuid` | `String`  | `预请求返回的ID`         |
| `data.data.region`         | `String`  | `预请求对应的国家缩写`   |
| `cost`                     | `String`  | `验证耗时（单位：毫秒）` |

#### json 示例

```
{
    "success": true,
    "data": {
        "preflight_uuid": "b5e404b6-55ca-4672-a83f-9a5f3e2e9882",
        "data": {
            "region": "ca",
            "navigator": {
                "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36"
            },
            ...
        }
    }
}
```
