------
[`Back to Home`](en.md)    [`Previous`](incapsula_rbzid.md)    [`Next`](tls.md)    [`中文文档`](../zh-CN/akamai.md)

## Akamai

### Description
* Akamai has many other factors that affect it. It is strongly recommended to use `pynocaptcha` directly. See the python example below for details!
* v2/v3 universal

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `v2（universal）` | `http://api.nocaptcha.io/api/wanda/akamai/v2` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| `href`       | `String`  | `Page URL that triggers akamai verification`                                                                                                                          | `Yes` |
| `api`        | `String`  | `Akamai submit sensor_data verification API address, this address will change after a period of time`       | `No` |
| `telemetry`  | `Boolean` | `Whether it's the telemetry parameter verification form in headers (such as akamai-bm-telemetry for https://api.maersk.com/ API), default false`   | `No` |
| `cookies`  | `Object`  | `Cookie values, can be string format or key-value pairs, must include _abck and bm_sz parameters`   | `No` |
| `proxy`    | `String`  | `No need to keep proxy consistent, if passing proxy please use overseas proxy, format: ip:port or usr:pwd@ip:port (contact admin if issues)` | `No` |

#### json examples

```json
{
    "href": "https://www.jetstar.com/"
}
```

```json
{
    "href": "https://www.jetstar.com/",
    "cookies": {
        "value": "_abck=D719B7C0C6B1EBE8FC8F5C1B804B2265~-1~YAAQJescuEJsVzWIAQAAnwAZQQkN297mPe+Q48Xd0/10jSvgz/y69qQbPEwxUuQZhIhisL+GFAMfvabHtQPRUbiIqzDD6vA9iN9lvjzaAbKaL+aNXF/3EhpYYYUsBa0q92JUxusD8F09nFXy3mfZ8p8GzDk+/ikw4Y8QVQcchjC/s6XYbG+I2RSHl+lDOSvR2biGLFZ1dW2PsFZQ6Fs4M1/ccWfaXg6IRvzjlWaF0vH8GIoljDVRvZxwCeUO71QJORFxeVEEO43BiC3LczJhMomt8pnTbnJcMbMbi1zFcYUKUZjYvB7+kJ1JsMHfVdzbrwTB2I3bePGPgX06RvzCReVCETYpJB7H+XEeJgQQDzKiYZhCONfnae3BQUll~-1~-1~1684722838; bm_sz=751A827227D797408E66A3559D978757~YAAQpVcyuNsPVjCIAQAAMTCrRhNw86NLVNcBypYZvOkbMMnc+ef6EeDWu9UtvPw3OfyfpKLmEFQeDw99mddahdMlOj3VxzPz8eV9mfMSWDLxup33fIKAvsMvnUjvAJV0gpZvTTwdk0atKXCg1DXvs+U+VOvPPJtS76B2t+r0jXrB+cUm2hJL7qF59kbHLBl54yypauoWa1qEu9lgelS5kdwiR93A0c9IRagfLG4VjFydhZBoD6ldWEQjQUflrf00GSoxQpL0QBKRlD7fFNRtMhBmndvu5yoGdixtPXCEKk5BzRl/~4605506~4276528; ak_bmsc=0E5236AFD795DD698B2E15191CEF0FDC~000000000000000000000000000000~YAAQpVcyuNoPVjCIAQAAMTCrRhNkrxzrgkZ1QP7XH0+hyJ2ul+4V0reJDlf1omJylP4/7vc+bxfB8EW1pfuYQWdBmzTBnE84h+7tH1SbFvNNNDul53BJsoOd79t8V0LGQdlXls3FWxITVSwuVlvCQTuJY1jq+uxrTTFFWpuqWQZnWkaLC/p8E7KRycXTaDSh7UW4k6ISRmssUftgDxwjZg43T6IbMyPf9dugLQSg9dKx4p8wyTcNern/fHfx7dAABbnUJkwmP+Y/eR4mfc9MJtIsJ3006DKH7PNoZ5JhtmnN9JTuhwfSEEnCrhs0j/cb2TrsSMo26w4C1xIaUNwZXE77YDci8VIkwEq9NvSTrTZUncSl0rsvoBz0j4QheSI=",
        "uri": "https://www.jetstar.com/"
    }
}
```

```json
{
    "href": "https://www.sephora.com/",
    "device": "pc"
}
```

```json
{
    "href": "https://www.maersk.com.cn/instantPrice/quotes",
    "telemetry": true
}
```

```json
{
    "href": "https://www.maersk.com.cn/instantPrice/quotes",
    "cookies": {
        "value": "_abck=D719B7C0C6B1EBE8FC8F5C1B804B2265~-1~YAAQJescuEJsVzWIAQAAnwAZQQkN297mPe+Q48Xd0/10jSvgz/y69qQbPEwxUuQZhIhisL+GFAMfvabHtQPRUbiIqzDD6vA9iN9lvjzaAbKaL+aNXF/3EhpYYYUsBa0q92JUxusD8F09nFXy3mfZ8p8GzDk+/ikw4Y8QVQcchjC/s6XYbG+I2RSHl+lDOSvR2biGLFZ1dW2PsFZQ6Fs4M1/ccWfaXg6IRvzjlWaF0vH8GIoljDVRvZxwCeUO71QJORFxeVEEO43BiC3LczJhMomt8pnTbnJcMbMbi1zFcYUKUZjYvB7+kJ1JsMHfVdzbrwTB2I3bePGPgX06RvzCReVCETYpJB7H+XEeJgQQDzKiYZhCONfnae3BQUll~-1~-1~1684722838; bm_sz=751A827227D797408E66A3559D978757~YAAQpVcyuNsPVjCIAQAAMTCrRhNw86NLVNcBypYZvOkbMMnc+ef6EeDWu9UtvPw3OfyfpKLmEFQeDw99mddahdMlOj3VxzPz8eV9mfMSWDLxup33fIKAvsMvnUjvAJV0gpZvTTwdk0atKXCg1DXvs+U+VOvPPJtS76B2t+r0jXrB+cUm2hJL7qF59kbHLBl54yypauoWa1qEu9lgelS5kdwiR93A0c9IRagfLG4VjFydhZBoD6ldWEQjQUflrf00GSoxQpL0QBKRlD7fFNRtMhBmndvu5yoGdixtPXCEKk5BzRl/~4605506~4276528; ak_bmsc=0E5236AFD795DD698B2E15191CEF0FDC~000000000000000000000000000000~YAAQpVcyuNoPVjCIAQAAMTCrRhNkrxzrgkZ1QP7XH0+hyJ2ul+4V0reJDlf1omJylP4/7vc+bxfB8EW1pfuYQWdBmzTBnE84h+7tH1SbFvNNNDul53BJsoOd79t8V0LGQdlXls3FWxITVSwuVlvCQTuJY1jq+uxrTTFFWpuqWQZnWkaLC/p8E7KRycXTaDSh7UW4k6ISRmssUftgDxwjZg43T6IbMyPf9dugLQSg9dKx4p8wyTcNern/fHfx7dAABbnUJkwmP+Y/eR4mfc9MJtIsJ3006DKH7PNoZ5JhtmnN9JTuhwfSEEnCrhs0j/cb2TrsSMo26w4C1xIaUNwZXE77YDci8VIkwEq9NvSTrTZUncSl0rsvoBz0j4QheSI=",
        "uri": "https://www.jetstar.com/"
    },
    "telemetry": true
}
```

### Response Data (JSON):

#### Successful Response

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data._abck`   | `String`  | `The available _abck cookie returned after successful verification, can be used for subsequent verification APIs`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
	"status": 1,
	"msg": "验证通过",
	"id": "8a8f0778-da09-4eea-a32d-e3b508654ba6",
	"cost": "1984.57ms",
	"data": {
		"_abck": "2EDD22DB758F24695963E50D3C9A776F~0~YAAQx\/ggF8FPIJ2HAQAA8nKqrQmFx5H17A\/jMUd1alzWlJ6VXb6NGDhXkb\/1cJW+Bp0jJYvWVj8hQVc1vRKAiKQ1HLm0JIo8kg00KEBoAyRG+VZZPRV6ikricthJ69SlXF99wcHaHwx7mvDZdwwAtJBl+Fp2Kagx62AbUYZjEpc9aOCZ5KXBQhdrwCrzzXWsu5WEgmGovNqegFuIpW1ifsVPe13QSi8EjwF\/nsuJQShLeRgsls1JB0Trwx8Kg3qRFiL9g4rtAdeW8OwYQ4DXj3PoBU56G0I4oCrhm6urGs8wMaU3OdpW6SRBAV93r4FO6K+lmcm8BVcfYc70\/wVuEx3Fx0zpesE0fkdKC6N5c80AjVtSgJnDLFuShDnXo+wsWGROM1vxP7sC7N6raiSN66sX4UxGlkAJiCU=~-1~||1-hkqRyYlvue-1-10-1000-2||~-1"
	}
}
```
