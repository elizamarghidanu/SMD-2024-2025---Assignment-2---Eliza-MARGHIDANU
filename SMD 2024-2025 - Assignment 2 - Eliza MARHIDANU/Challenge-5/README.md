# Challenge 5 - Broadcast Receiver Flag Extraction

## Description

This challenge demonstrates a broadcast-based flag delivery mechanism. When the screen loads or the **BROADCAST** button is clicked, a broadcast is sent with a specific `Intent`. Our goal is to intercept that `Intent`, extract the encoded flag from it, decode it, and use it to complete the challenge.

## Analysis

Using JADX, we found the method responsible for broadcasting the intent:

```java
public void broadcastIntent(View view) {
    String str = new String(Base64.decode("VGhlZ2VhbG9GVXKb3JsZENhbNlNZUl1", 0));
    Intent intent = new Intent();
    intent.putExtra("INTRO", "Broadcast from MiniAndroidChallenges ");
    intent.putExtra("FLAG", str);
    intent.setAction("com.fake.minibroadcast");
    getActivity().sendBroadcast(intent);
}
```

The important parts:

- The broadcast action is: `com.fake.minibroadcast`
- The flag is stored as a Base64-encoded string in the `FLAG` extra
- The broadcast is triggered on fragment load or button click

## Solution Steps

We used ADB to intercept the broadcast:

```bash
adb logcat | grep FLAG
```

Or, use `frida-trace` to hook into `sendBroadcast` and dump the `Intent`.

If needed, decode the Base64 flag manually:

```bash
echo VGhlZ2VhbG9GVXKb3JsZENhbNlNZUl1 | base64 -d
```

## Tools Used

- Genymotion (Pixel emulator)
- JADX
- ADB (via `platform-tools`)
- `base64` or Python for decoding

## Flag

*TheWholeWorldCanSeeMe*

## Video

[Solution on Yt](https://youtu.be/tpSnQeio19w)
