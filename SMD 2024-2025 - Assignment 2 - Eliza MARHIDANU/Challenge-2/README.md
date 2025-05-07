# Challenge 2 - Bypassing PIN Check with Frida

This challenge involves bypassing a PIN check in an Android app using Frida, a dynamic instrumentation toolkit.

## Setup

Ensure you have:
- [Genymotion](https://www.genymotion.com/)
- `adb` from Android platform-tools
- `frida-server` for the appropriate architecture (x86_64 for Genymotion)
- Frida tools installed on your system

## Steps

### 1. Push and Start Frida Server

```bash
adb -s <ip:port> push frida-server-16.7.14-android-x86_64 /data/local/tmp/frida-server
adb -s <ip:port> shell "chmod 755 /data/local/tmp/frida-server"
adb -s <ip:port> shell "/data/local/tmp/frida-server &"

`````````````
### Verify it’s running:

```bash
adb -s <ip:port> shell "ps | grep frida"
```
### 2. Create `bypass-pin.js`

```bash
Java.perform(function () {
    var PinUtil = Java.use("com.example.miniandroidchallenges.utils.PinUtil");
    PinUtil.pincodeCheck.implementation = function (input) {
        console.log("[+] Intercepted PIN check with: " + input);
        return true; // Always return true
    };
    console.log("✅ Hook complete.");
});
```
### 3. Launch the app with Frida:
```bash
frida -U -f com.example.miniandroidchallenges -l bypass-pin.js --runtime=v8
%resume
```
### Result

The app will accept any PIN input, and you'll see:

```bash
[+] Intercepted PIN check with: 1111
```

### Video
[Link](https://youtu.be/zGh5Q8FA_iI)
