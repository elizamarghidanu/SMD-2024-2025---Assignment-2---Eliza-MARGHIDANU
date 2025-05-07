
# Challenge 1 – Root Detection Bypass

This challenge involves bypassing a root detection check performed by the app. It uses a library like `RootBeer` to detect rooted devices. We'll hook the method at runtime using Frida and force it to return `false`.


## Setup

Requirements:
- Genymotion (rooted emulator)
- ADB & Frida properly installed
- Matching `frida-server` running on the device

## Steps

### 1. Push and Start Frida Server

```bash
adb -s <ip:port> push frida-server-16.7.14-android-x86 /data/local/tmp/frida-server
adb -s <ip:port> shell "chmod 755 /data/local/tmp/frida-server"
adb -s <ip:port> shell "/data/local/tmp/frida-server &"
```
Verify it's running:
```bash
  adb -s <ip:port> shell "ps | grep frida"
```
### 2. Create `bypass-root.js`

```bash
Java.perform(function () {
    var RootBeer = Java.use("com.scottyab.rootbeer.RootBeer");
    RootBeer.isRooted.implementation = function () {
        console.log("Bypassed isRooted() check");
        return false;
    };
});

```

### 3. Run Frida to hook the method

```bash
frida -U -f com.example.miniandroidchallenges -l bypass-root.js --runtime=v8
```
At the Frida prompt:

```bash
  %resume
```

### Video
[Link to yt video](https://youtu.be/RolQOleHgD8)
