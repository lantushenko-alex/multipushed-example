# Pushed React Native Example
A working example of using multipushed library. It was not possible to run it on the latest React Native so some 
3rd party lib versions were rolled back.

This is an example project demonstrating how to use the `@PushedLab/pushed-react-native` package for integrating push notifications from Pushed.ru into your React Native application.

## Installing the Package

### Option 1: Install from GitHub
You can install the package directly from GitHub:

```bash
npm install github:PushedLab/Pushed.Messaging.ReactNative
```

Or specify a specific version or branch:
```bash
npm install github:PushedLab/Pushed.Messaging.ReactNative#main
npm install github:PushedLab/Pushed.Messaging.ReactNative#v0.1.7
```

### Option 2: Use Local Version
For development, you can link to a local version by adding this to your package.json:

```json
"dependencies": {
  "@PushedLab/pushed-react-native": "file:/path/to/Pushed.Messaging.ReactNative"
}
```

Then run `npm install` or `yarn` to install the package.

## Usage in Your App

To implement automatic service initialization in your own app, use this pattern:

```typescript
import { useEffect, useState } from 'react';
import { startService, PushedEventTypes } from '@PushedLab/pushed-react-native';

export default function App() {
  const [token, setToken] = useState('');
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    // Auto-start the service
    startService('PushedService')
      .then((newToken) => {
        setToken(newToken);
        setIsLoading(false);
      })
      .catch((error) => {
        console.error('Failed to start service:', error);
        setIsLoading(false);
      });
  }, []);

  // Your app UI here...
}
```

---
if you get error
```
Unable to load script. Make sure you're either running Metro or that you bundle index.android.bundle is packed correctly for release
```
then do this
https://stackoverflow.com/questions/55441230/unable-to-load-script-make-sure-you-are-either-running-a-metro-server-or-that-yo
```
mkdir android/app/src/main/assets
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
react-native run-android
```
