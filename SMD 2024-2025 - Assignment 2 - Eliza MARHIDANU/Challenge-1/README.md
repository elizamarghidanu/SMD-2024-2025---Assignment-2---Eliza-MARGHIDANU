# Challenge 1 – Mini Android Root Detection Bypass

## Objective
Bypass the app’s root detection mechanism to display the screen that appears only if no root is detected.

## Tools Used
- APKTool
- JADX (for inspection)
- Uber APK Signer
- BlueStacks (Emulator)

## Steps Taken
1. Decompiled the APK using APKTool.
2. Found the `isRooted()` method in `RootBeer.smali`.
3. Replaced the entire method body to always return `false`.
4. Rebuilt the APK using APKTool.
5. Signed it using Uber APK Signer.
6. Installed the signed APK on BlueStacks.
7. Opened the app and confirmed it now says: **“No root detected”**.

## Result
Bypassing the detection logic allowed access to the screen that’s only shown when the app thinks root is absent.
