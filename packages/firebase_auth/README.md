# firebase_auth plugin
A Flutter plugin to use the [Firebase Authentication API](https://firebase.google.com/products/auth/).

[![pub package](https://img.shields.io/pub/v/firebase_auth.svg)](https://pub.dartlang.org/packages/firebase_auth)

For Flutter plugins for other Firebase products, see [FlutterFire.md](https://github.com/flutter/plugins/blob/master/FlutterFire.md).

*Note*: This plugin is still under development, and some APIs might not be available yet. [Feedback](https://github.com/flutter/flutter/issues) and [Pull Requests](https://github.com/flutter/plugins/pulls) are most welcome!

## Usage

### Configure the Google sign-in plugin
The Google Sign-in plugin is required to use the firebase_auth plugin. Follow the [Google sign-in plugin installation instructions](https://pub.dartlang.org/packages/google_sign_in#pub-pkg-tab-installing).

### Import the firebase_auth plugin
To use the firebase_auth plugin, follow the [plugin installation instructions](https://pub.dartlang.org/packages/firebase_auth#pub-pkg-tab-installing).

### Android integration

Enable the Google services by configuring the Gradle scripts as such.

1. Add the classpath to the `[project]/android/build.gradle` file.
```
dependencies {
  // Example existing classpath
  classpath 'com.android.tools.build:gradle:2.2.3'
  // Add the google services classpath
  classpath 'com.google.gms:google-services:3.0.0'
}
```

2. Add the apply plugin to the `[project]/android/app/build.gradle` file.
```
// ADD THIS AT THE BOTTOM
apply plugin: 'com.google.gms.google-services'
```

*Note:* If this section is not completed you will get an error like this: 
```
java.lang.IllegalStateException: 
Default FirebaseApp is not initialized in this process [package name]. 
Make sure to call FirebaseApp.initializeApp(Context) first.
```

*Note:* When you are debugging on android, use a device or AVD with Google Play services. 
Otherwise you will not be able to authenticate. 

### Use the plugin

Add the following imports to your Dart code:
```
import 'package:firebase_auth/firebase_auth.dart';
```

Initialize `FirebaseAuth`:
```
final FirebaseAuth _auth = FirebaseAuth.instance;
```

You can now use the Firebase `_auth` to authenticate in your Dart code, e.g. 
```
Future<Null> _handleSignIn() async {
  try {
    GoogleSignInAccount googleUser = await _googleSignIn.signIn();
    GoogleSignInAuthentication googleAuth = await googleUser.authentication;
    FirebaseUser user = await _auth.signInWithGoogle(
      accessToken: googleAuth.accessToken,
      idToken: googleAuth.idToken,
    );
    print("signed in" + user.displayName);
  } catch (error) {
    print(error);
  }
}
```

## Example

See the [example application](https://github.com/flutter/plugins/tree/master/packages/firebase_auth/example) source 
for a complete sample app using the Firebase authentication.

## Issues and feedback

Please file [issues](https://github.com/flutter/flutter/issues/new)
to send feedback or report a bug. Thank you!