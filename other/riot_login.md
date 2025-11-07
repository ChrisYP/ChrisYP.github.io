# Riot Login

## Last Updated at 2025-11-08

## !!! How to get rqdata ?

### Step 1. get region and useragent from preflight data

```
{
    "success": true,
    "data": {
        "preflight_uuid": "b5e404b6-55ca-4672-a83f-9a5f3e2e9882",
        "data": {
            "region": ...,
            "navigator": {
                "userAgent": ...
            },
            ...
        }
    }
}

```

### Step 2. Based on UA different methods are used to getting rqdata

### A. Client UA

sample `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) riot-client-ux/120.0.0 Chrome/108.0.5359.215 Electron/22.3.27 Safari/537.36`

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
    "sdkVersion": "25.3.0.5220",// dynamic
    "type": "auth",
    "xbox": null
}


```

### B. Web UA

sample `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36`

getting rqdata in the same way as with you use the broswer.

## !!! pass [confirm] param

```txt
POST http://api.nocaptcha.io/api/wanda/hcaptcha/universal

{
    "sitekey": "019....",
    ...,
    "confirm": "v1.0.1"
}

```

pass right `confirm` param mean you know how to correct rqdata
