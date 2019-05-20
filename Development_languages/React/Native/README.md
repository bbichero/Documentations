React Native
------

Requirements:
```
NodeJS > 10.0
ReactNative: 0.59
expo-cli: 2.17.1
watchman
```

Install watchman and node:
```
brew install watchman node
```

You need to install `expo-cli` for react native environment:
```
npm install -g expo-cli react-native-cli
```

Initialize application:
```
expo-cli init ${APP_NAME}
```

You must define an displayable app name (with space and special char)
Now you can enter app directory and start app:
```
cd ${APP_NAME}
npm run start
```

If you want, install Expo application on your mobile device and view change in real time.
