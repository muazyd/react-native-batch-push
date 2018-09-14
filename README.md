# react-native-batch-push

> React Native integration of Batch.com push notifications SDK

## Getting started

```
$ npm install @bam.tech/react-native-batch --save

# OR

$ yarn add @bam.tech/react-native-batch
```

### Mostly automatic installation

```bash
react-native link @bam.tech/react-native-batch
```

#### iOS specific

If you don't have a Podfile or are unsure on how to proceed, see the [CocoaPods](http://guides.cocoapods.org/using/using-cocoapods.html) usage guide.

In your `Podfile`, add:

```
pod 'Batch', '~> 1.10'
```

Then:

```bash
cd ios
pod repo update # optional and can be very long
pod install
```

### Configuration

#### Android

Go to the Batch dashboard, create an Android app and setup your GCM configuration.
Then, in `android/app/build.gradle`, provide in your config:

```
defaultConfig {
    ...
    resValue "string", "GCM_SENDER_ID", "%YOUR_GCM_SENDER_ID%"
    resValue "string", "BATCH_API_KEY", "%YOUR_BATCH_API_KEY%"
}
```

Note that you can also customize the keys depending on your product flavor or build type.

##### Mobile landings and in-app messaging

If you set a custom `launchMode` in your `AndroidManifest.xml`, add in your `MainActivity.java`:

```java
// import android.content.Intent;
// import com.batch.android.Batch;

@Override
public void onNewIntent(Intent intent)
{
    Batch.onNewIntent(this, intent);

    super.onNewIntent(intent);
}
```

#### iOS

Go to the Batch dashboard, create an iOS app and upload your iOS push certificate.
Then, in `Info.plist`, provide:

```xml
<key>BatchAPIKey</key>
<string>%YOUR_BATCH_API_KEY%</string>
```

## Usage

### Enabling push notifications

```js
import Batch from '@bam.tech/react-native-batch';

// when you want to ask the user if he's willing to receive push notifications (required on iOS):
Batch.registerForRemoteNotifications();
```
