# Android Example Application (WebView) + Push Notification!
![Android SDK](https://img.shields.io/badge/31-100000?label=Android%20SDK&style=for-the-badge&logo=android&color=)
![Android+Studio](https://img.shields.io/badge/Android_Studio-555555?style=for-the-badge&logo=Android+Studio)

Application that renders a web page in a simple and transparent way. With it, you can turn any website into a native application for your Android phone!
Plus, you'll find some other features like Slash Screen, custom logo, theme colors, error page, and a bonus: integration to receive Push Notifications with OneSignal!

_Note: This application was developed for study purposes. The original version of this project is from 2018._

<div align="center">
<img width="30%" src="https://raw.githubusercontent.com/arturmedeiros/android-java-webview-example/master/assets/Screenshot_1661977144.png">
<img width="30%" src="https://raw.githubusercontent.com/arturmedeiros/android-java-webview-example/master/assets/Screenshot_1661977153.png">
<img width="30%" src="https://raw.githubusercontent.com/arturmedeiros/android-java-webview-example/master/assets/Screenshot_1661977176.png">
</div>


## ✅ Requirements

To use the project, you need to have some packages and starter packages on your computer:

- GIT
- Android Studio
- Java SDK's

## ⬇️ Installation
Clone this repository and import into **Android Studio**:
```bash
git clone git@github.com:arturmedeiros/android-java-webview-example.git
```

## 📣 Push Notifications `OneSignal`

In the midst of the code, we prepared the necessary fields so that you can integrate the OneSignal service into your Android application! That way, your app will receive the notifications you send through that vendor's dashboard.

**⚠️ WARNING:** You need to have a OneSignal account and a token to be able to integrate.

## ⚙️ Configure OneSignal Token

In order for your application to receive Push Notifications, you need to provide your Token.

Line 25 ```/app/build.gradle```

```
    manifestPlaceholders = [
->      onesignal_app_id: 'ONESIGNAL_API_KEY_XXXXXXXXXXXXXXXXXXXX',
        onesignal_google_project_number: 'REMOTE'
    ]
```

## 📦 Generating signed APK
From Android Studio:
1. ***Build*** menu
2. ***Generate Signed APK...***
3. Fill in the keystore information *(you only need to do this once manually and then let Android Studio remember it)*

## 🧑🏻‍💻 Authors
This project is mantained by:
* [Artur Medeiros](http://github.com/arturmedeiros)


## ⚖️ License
MIT License

Copyright (c) 2022 @ARTURMEDEIROS - ARJOS.COM.BR

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
