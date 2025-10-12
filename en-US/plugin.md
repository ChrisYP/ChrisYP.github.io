[`Back to Home`](en.md)    [`中文文档`](../zh-CN/plugin.md)

## ReCaptcha & hCaptcha

- First, install the extension. The extension download link is:

  `https://chrome.google.com/webstore/detail/nocaptcha-solver/kkphlbgphimpedeckcepigahenlmpggc?utm_source=ext_sidebar&hl=zh-CN`

  ##### Or [`Click here to download`](https://chrome.google.com/webstore/detail/nocaptcha-solver/kkphlbgphimpedeckcepigahenlmpggc?utm_source=ext_sidebar&hl=zh-CN)

![Figure 1](/images/fill-params/1.png)

- After installing the extension, pin the `NoCaptcha Solver` extension to the extensions bar (for convenience) and then log in to your platform account. `token` is the `token` consumed, `user name` is the platform `login account`, i.e., `email address`.

  ![Figure](/images/fill-params/3.png)

  ![Figure](/images/fill-params/2.png)

- Click `Manage extensions` or enter `chrome://extensions/` into the extension page and click `Service Worker`.

  ![Figure](/images/fill-params/4.png)

- Clicking will open the developer tools, at this point, switch to the `network` panel.

  ![Figure](/images/fill-params/5.png)

- Open the website that needs to be cracked, such as `https://democaptcha.com/demo-form-eng/recaptcha-2.html`, and the extension will automatically start to crack `reCaptcha` or `hCaptcha`.

  ![Figure](/images/fill-params/6.png)

  ![Figure](/images/fill-params/7.png)

- At this point, in the `network` column, you can get all the parameters needed for the captcha. Pay **no attention** to the `extra` object and **do not submit this parameter**.

  ![Figure](/images/fill-params/8.png)

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

With this, all the parameters needed for cracking are obtained at once. The operation of hCaptcha is exactly the same as reCaptcha, so it is not repeated here.
