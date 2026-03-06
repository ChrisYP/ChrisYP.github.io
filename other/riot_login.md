# Riot Login

## !!! How to get rqdata ?


```txt

POST https://authenticate.riotgames.com/api/v1/login

headers: content-type: application/json

{
    "apple": null,
    "campaign": null,
    "clientId": "riot-client",
    "code": null,
    "facebook": null,
    "gamecenter": null,
    "google": null,
    "language": "en_GB",
    "mockDeviceId": null,
    "mockPlatform": null,
    "multifactor": null,
    "nintendo": null,
    "platform": "windows",
    "playstation": null,
    "qrcode": null,
    "remember": false,
    "riot_identity": {
        "captcha": null,
        "password": null,
        "state": "auth",
        "username": null
    },
    "riot_identity_signup": null,
    "rso": null,
    "sdkVersion": "25.3.0.5220",
    "type": "auth",
    "xbox": null
}


```
## !!! pass [confirm] param

```txt
POST http://api.nocaptcha.io/api/wanda/hcaptcha/universal

{
    "sitekey": "019....",
    ...,
    "confirm": "v1.0.0"
}

```

pass right `confirm` param mean you know how to correct rqdata