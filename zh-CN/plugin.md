[`返回首页`](../README.md)     [`English Version`](../en-US/plugin.md)

## ReCaptcha & hCaptcha

- 首先安装扩展，扩展下载地址为：

  `https://chrome.google.com/webstore/detail/nocaptcha-solver/kkphlbgphimpedeckcepigahenlmpggc?utm_source=ext_sidebar&hl=zh-CN`

  ##### 或 [`点我下载`](https://chrome.google.com/webstore/detail/nocaptcha-solver/kkphlbgphimpedeckcepigahenlmpggc?utm_source=ext_sidebar&hl=zh-CN)

![图1](/images/fill-params/1.png)

- 安装好扩展后，将`NoCaptcha Solver`扩展固定在扩展栏中（方便操作）后登录自己平台的账号。`token`为消费的`令牌`，`user name` 为平台`登录账号`，即`邮箱地址`。

  ![图](/images/fill-params/3.png)

  ![图](/images/fill-params/2.png)

- 点击`管理扩展程序`或者浏览器输入`chrome://extensions/`进入扩展程序页面, 点击`Service Worker`

  ![图](/images/fill-params/4.png)

- 点击后会打开开发者工具，此时切换至`network`面板。

  ![图](/images/fill-params/5.png)

- 打开需要破解的网站，如`https://democaptcha.com/demo-form-eng/recaptcha-2.html` 扩展会自动开始破解`reCaptcha`或者`hCaptcha`。

  ![图](/images/fill-params/6.png)

  ![图](/images/fill-params/7.png)

- 此时，在`network`栏里，则可获取到验证码需要的所有参数。注意**无需理会**`extra`对象，也**不要提交该参数**。

  ![图](/images/fill-params/8.png)

```json	
{
    "sitekey": "6LfGqN0UAAAAAFdGo4OSj5Awi8hM_9kmR7VfXUP2",
    "referer": "https://democaptcha.com/demo-form-eng/recaptcha-2.html",
    "title": "reCAPTCHA 2 demo form | AntiCaptcha plugin demo forms",
    "size": "normal",
    "action": null,
    "s": null,
    "extra": {
        "origin": "chrome-plugin",
        "cb": null
    }
}
```

至此，破解所需要的参数就一次性全部获取到了，hCaptcha的操作也是和reCaptcha一摸一样的，在此就不再赘述了。

