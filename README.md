# flutter_vk_login

A Flutter plugin for using native android VKSdk.

This project havealy influented by [flutter_facebook_login](https://github.com/roughike/flutter_facebook_login).

Warning: This Flutter plugin working only on Android.

## Getting Started

First things first, create standalone app on your [VK app manage page](https://vk.com/apps?act=manage). Save AppID
(или ID приложения).

In your android res/values create strings.xml and fill with this examples
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Flutter VK Login example</string>
    <integer name="com_vk_sdk_AppId">YOUR_VK_APP_ID</integer>
</resources>
```

Than, add vksdk dependency in android/app/build.gradle

```gradle
dependencies{
    //...your other dependecies
    api 'com.vk:androidsdk:1.6.9' //or api, I am new to android dev.
}
```

Next, in android section off your flutter app create class Application
```java
package com.example.name;

import io.flutter.app.FlutterApplication;
import com.vk.sdk.VKSdk;

public class Application extends FlutterApplication {
    @Override
    public void onCreate() {
        super.onCreate();
        VKSdk.initialize(this);
    }
}

``` 
And in your AndroidManifest.xml edit application section to this

```xml
<application
        android:name=".Application"
        ...
/>        
```

##Dart usage
```dart
final VkLoginResult result =
        await vkSignIn.logIn(['email']);

    switch (result.status) {
      case VKLoginStatus.loggedIn:
        final VKAccessToken accessToken = result.token;
        _showMessage('''
         Logged in!
         
         Token: ${accessToken.token}
         User id: ${accessToken.userId}
         Expires: ${accessToken.expiresIn}
         Permissions: ${accessToken.scope}
         ''');
        break;
      case VKLoginStatus.cancelledByUser:
        _showMessage('Login cancelled by the user.');
        break;
      case VKLoginStatus.error:
        _showMessage('Something went wrong with the login process.\n'
            'Here\'s the error Facebook gave us: ${result.errorMessage}');
        break;
    }
  }
```
