# react-native-background-fetch

https://github.com/transistorsoft/react-native-background-fetch/

# setup

### :open_file_folder: **`app.json`**

- Add the following to **`plugins`**:

```diff
{
  "expo": {
    "name": "your-app-name",
    "plugins": [
+     "react-native-background-fetch"
    ]
  }
}
```

- Add the following **`UIBackgroundModes`** and **`BGTaskSchedulerPermittedIdentifiers`** to the **`ios.infoPlist`** section:

```diff
{
  "expo": {
    "name": "your-app-name",
    "plugins": [
      "react-native-background-fetch"
    ],
    "ios": {
+     "infoPlist": {
+       "UIBackgroundModes": [
+         "fetch",
+         "processing"
+       ],
+       "BGTaskSchedulerPermittedIdentifiers": [
+         "com.transistorsoft.fetch"
+       ]
+     }
    }
  }
}
```

- If you intend to execute your own custom tasks via **`BackgroundFetch.scheduleTask`**, you must add those custom identifiers as well to the **`BGTaskSchedulerPermittedIdentifiers`**. For example, if you intend to execute a custom **`taskId: 'com.transistorsoft.customtask'`**, you must add the identifier **`com.transistorsoft.customtask`** to `BGTaskSchedulerPermittedIdentifiers`:

```diff
  "BGTaskSchedulerPermittedIdentifiers": [
    "com.transistorsoft.fetch",
+   "com.transistorsoft.customtask"
  ]
```

:warning: A task identifier can be any string you wish, but it's a good idea to prefix them now with `com.transistorsoft.` &mdash; In the future, the `com.transistorsoft` prefix **may become required**.

```javascript
BackgroundFetch.scheduleTask({
  taskId: 'com.transistorsoft.customtask',
  delay: 60 * 60 * 1000, //  In one hour (milliseconds)
});
```

### Re-build

You must rebuild your Android app for the added plugins to be evaluated.

- If you're developing locally:

```bash
npx expo prebuild
```

- If you're using _Expo EAS_:

```bash
eas build --profile development --platform android
```

# build

## setup eas

```
eas build:configure
```

## develop build (simulation)

### iOs

```
eas build --profile development-simulator --platform ios --local
```

作成できた tar.gz ファイルを解答し、app をシミュレーターへ drop する

### android

```
eas build --profile development --platform android --local
```

## preview build (実機インストール用)

### iOs

```
eas build --profile preview --platform ios --local
```

apple configurator で転送

### android

```
eas build --profile preview --platform android --local
```

android file transfer で転送
