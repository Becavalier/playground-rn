# playground-rn
Playground for React Native.

### React Native

```shell
# Install react-native-cli
npm install -g react-native-cli

# Build and run
react-native run-ios/run-android

```

### CodePush 

#### Azure Server

```shell
# Install code-push-cli
npm install -g code-push-cli

# Register, and get a token
code-push register

# Register apps (ios and android), and get two deployment keys
# code-push app add <appName> <os> <platform>
code-push app add PlayRN-IOS ios react-native 
code-push app add PlayRN-IOS android react-native 

# Link react native package manager
npm install rnpm -g
rnpm link react-native-code-push
```

Take care of the "Scheme" you set in Xcode:
```objective-c
#ifdef DEBUG
    jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index.ios" fallbackResource:nil];
#else
    jsCodeLocation = [CodePush bundleURL];
#endif
```

```shell
# Push updates, seperatly
mkdir bundles

# Packing
react-native bundle --platform ios/android --entry-file index.ios.js --bundle-output ./bundles/index.ios.bundle --dev false

# Pushing 
code-push release PlayRN-IOS ./bundles -t '1.*' --des "Update for IOS app."

# Push updates altogether (includes packaging and pushing)
code-push release-react PlayRN-IOS ios/android -t '1.*' -d Production --des 'Update for IOS app.'
```

```shell
# Log
code-push deployment history PlayRN-IOS Staging/Production
# Remove app from current code-push account
code-push app remove playRN-IOS
```

#### Custimized Server

