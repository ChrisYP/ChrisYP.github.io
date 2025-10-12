------

[`返回首页`](../README.md)    [`上一页`](incapsula.md)       [`下一页`](incapsula_rbzid.md)   [`English Version`](../en-US/incapsula_utmvc.md)

## Incapsula ( __utmvc )

### 有问必答

* 接口(utmvc 需要保持代理一致, 有问题联系管理员)
    * 1、传入 href 和 proxy, 服务请求后计算 utmvc 
* utmvc 脚本怎么找(如下图,包含 SWJIYLWA 关键字的 url)
    * ![incapsula](/images/incapsula/incapsula3.png)
* utmvc 脚本返回样例
    * ![incapsula](/images/incapsula/incapsula4.png)

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|-------------------|---------------------------------------------------------|
| `utmvc` | `http://api.nocaptcha.io/api/wanda/incapsula/utmvc` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明  | 必须  |
|--------------|-----------|----------------------|-----|
| `cookies`    | `Object`  | `请求首页返回的 cookies, 全部上传` | `是` |
| `href`        | `String`  | `返回 utmvc 脚本的url` | `是` |
| `user_agent` | `String`  | `utmvc 流程需要 ua 一致, 所以请传你将使用的 ua`  | `是` |
| `script` | `String`  | `href 请求的结果脚本` | `是` |

#### json 示例

```
{
    "href": "https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=5074a744e2e3d891814e9a2dace20bd4,719d34d31c8e3a6e6fffd425f7e032f3",
    "script": "href 请求结果"
    "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36",
    "cookies": {
        "incap_ses_406_2314793": "w399Tycs8xhdpuG+aWeiBWGkYWQAAAAAKCTf+jt4Sq4R0xN0pU9VXA==",
        "visid_incap_2314793": "DVtB0J4PRoG+jHdSiyyjNWKkYWQAAAAAQUIPAAAAAABY5A3D8V2Yp2rCf0Qol0Kd"
    }
}
```

### Response Data（JSON）:

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.__utmvc` | `String`  | `计算完成的 __utmvc 参数, 可用于后续接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
    "status": 1,
    "msg": "验证成功",
    "id": "61b4bb7f-abf9-4875-ae58-38916e1ecbff",
    "cost": "36.42ms",
    "data": {
        "___utmvc": "RcfBxntM86jhyTPW9\/oPyTZXmlRnma\/xzVbBTv\/R+EYCOhO+kToGT3voh01qY+XSbofVvKsiiT3idzZPd+\/D2rC8dghiDx9BghnUQmDnnTl1ItRMO2oSM11H1NOZzkYe7zMTCVt9J1lITjqAf7+6ugxunXAqgbprbsxFO0aTWZvFB7yk7mTDbmym6x54XJQTGFv\/EXDCZRRFdFGyvERlFd+NYnBflIZmGt78FvFx\/z377YrMoBFcvOMa9fitI6Om\/GncCxQp4Clfw5TEHiCUjag07zwzX9GBpFg\/WelYYkDHDiJE0XpBvrhGBFF\/6mEsjm4koZ+zKQRlsmhWVl3ebKDB+6XPEf1bSEPUFIjKTcX09XjgqWoVUKxcJ1M0TFCoISEBw6XomRAPesLIusgdLl76s++cxHfaouRsK6O4hHyDafDYBMIN1fMeK6onWYsl2KK4bklSOV5F9kLK2hYgnrPxONTd2WTqsnt4XDxqUc7FnmvRNeSJ7jdlAK7r3SpaZy2a5O+Dmmsff89kNmDOze3DiYl8sxNs4g9fhaaLEEavfhotUUL+p1Bu\/mHTjW7ZSfnTsjrL4AkeQN2IDL6jZ2giarbl\/QiRn\/JJo+4wppxXeUs\/iq8h+WFOyDRZYqTBKgbsR0V838D4G8pyZvOTomBnlFxaPMXQWapoDPZ5FxB6irCl\/Gp3vjH0QR31jkN7EV4ZzX1\/NG\/Uurgyr9fuSZAAaKh8A818xxshT5JIK30WPx8NzR7S\/BK+std1WK4Vbnxxnt+Ug\/2HImjJPkgqSOxpQCq0m3J48sZs1TsuHUryRpLVu7FPjIX\/Y4K2i1\/Oa6er+oNyyED4ZuBuEKTsIoDE3cQisABkK59OJw3e9nIPPvUA7S4j504DzcS0YyMEvubKfydUzcbuCqBv3bbtJvtCHTbd6RcRqnarOcnOSh51BdW7rBlopVLQNfdg5rI9lvNGBn3B7WmQvkoPi7DpEZA\/\/mgdIcFd3BAbYlyUNSuQG38Gw2BcclsUK4tF3ybYNGTuyHWYmlIgF4nIGfq7uZtYTeZkHEoZepneCKMiAm81fL9ySSU2agC7Uo7gDtzhrldrUI06XINOdRu5ghaeoNxcrJqkuvBlUKmhW37vhmPH\/B3I3\/r4PrgNAJfplRyLQv8fdJBg1HZDl2\/dvTs0Od\/NLQpDt3fTo0eYJ++EGiTReMHXXGGc7IgYN3zVGwTs6toqYRraRKqOGyjKZ1smsMkuZdHl899ZHMrbehaYVu+onsITpxTBjqQiHoV4Cs6PcLC8hs2Fat+3+Rq81pzOBc11A53y+bBDhm5rlGC6kuhWUYQZLGh6Q8dy7DaBuDagCEsq\/qGzyoayKqZBflHT3xotXWxsadCQGRVjY2V3lsk75yJIdegGLlcMCejZRVikY\/9vnwpdo7q6yptfoTmqxqr63WOOVVgRhw+oA1vnyXF85\/cV5R6L6B3EW28thIpeZlEhaqsH0jm3grVxZjuRRGFTQ4ObC5ubR6wmfioRoMLNQMQVZzUYlkmkSS1ixv05OS1cg5mDbC6WTuFl42Wl8a663VuGOtPTY1uSwZ8sOcXXlcGo9W1OQTAIbF\/2VoS+gJyvhiYDHq\/e6s04n7Sia5+lCCXJ0GPWHT0SLRtKHfaOyy9geB82UU9Sb47SIYunQ2S5OzL9X2XdA5823bytz42GKDR+c6dP7dB2xtxV27lciByVCn\/s5pQaJGQJm3X1wnd\/\/mzjxEoSATgm2fP3SJBElLrd3WQ6NED75XKgaw5hrKzG\/Yl\/IhbSFJdYkHK0Y4VRYEvZ0nDZBZtOX3r96JBHn5szz7TD7ngkGCa1RmUBvjHrQMwvCNvu6zwHozlN1nNXcw1ekTj4JEoXPLtYIIaw7amEdbBzdp3fvZJJ\/xwZhowaUpOH4Ml7Y\/slWsJ3B6ZNWvDD9izXritrNVc6yUljs053302cFkbG+qoaCSkol2hWf5LoAq+0i4xU9ZsTuE537w7t7Fv9ZcHwgEBTgrJ2Wc42pqAmw6JUDJdGbSUL11ZhYuHE5iixrlZJ2ZsYdTtaN180fpMDprT0YLOo4tPvYQa2cn8c0eTvmKbuAZlzcxmBJ9kx6a0pH8uA1YbXd5fpfYdy2vcO\/gO5qRJ2FrGvCF+RHD7Ana9OVbnHsFaI22ZqxLIBuSu6P4fIlLxf\/7Ri3qyhDJ40+owEBqajKOCBNDje+iL\/IgnQN1sUB+bFRfqAzAB9ejN\/0FUUwaculCjdiiOPy42y1Ml3nyrlWB89KL5kpFVWyZ6afiJLV2V0R4eJrg65sU3UbaWS0i4AChHLYInyXw0Ll4EnOAJo8dZ3hKdteYzhSx5CXRFXtbn9\/YeNjX1m7cbAkojc4RkxT\/ICULCwzo8Oshz8LHNigszgp40X71nvFiyxLN+ZGMSkGuz29XWrZN\/bfMN4cbzHFnmZaJmvWAtfzGyj5dw1B3WKBJHbEVy6f33cbMCbqEeHwCRibtPGvvHTDaP37pUO0Ya50TjHscaRbcdOgbBC24r65MOXeWQoKqARnuwN0fLkv9Vqpd2s8\/1\/8L6f1Sdk9FEcMrFqGAq\/xGmXpiGUStNdmWPuRADSo8XHWl\/OQdGhZk6TejmSccDrMwkG5Vm5jp1q7XpcbqDvj9natEYI3N+6h\/71eF+FAeZcfTef8yxkaWdlc3Q9MTgyMjU1LHM9NjE5MGE4OTM4M2EyN2Q5OWFhOWI5ZTY0OWM3ZTdmOGM2MDgzNjdiMmE3NjU4YzZjYThhZGE1NmE4YjY3NzdhYTczOTk5YzgwNzQ5ZjZmNmY="
    }
}
```

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import IncapsulaUtmvcCracker

cracker = IncapsulaUtmvcCracker(
    user_token="xxx",
    href="https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    script="href 请求结果",
    cookies={ 'incap_ses_406_2314793': 'w399Tycs8xhdpuG+aWeiBWGkYWQAAAAAKCTf+jt4Sq4R0xN0pU9VXA==', 'visid_incap_2314793': 'DVtB0J4PRoG+jHdSiyyjNWKkYWQAAAAAQUIPAAAAAABY5A3D8V2Yp2rCf0Qol0Kd' },
    proxy="usr:pwd@ip:port",
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
)
ret = cracker.crack()
print(ret)
```
