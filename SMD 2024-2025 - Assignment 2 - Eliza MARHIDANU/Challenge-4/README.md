# Challenge 4 – Exported Activity

## Objective
Identify and exploit an *unintended exported activity* that is not reachable from the user interface.

---

## Approach

The challenge hinted that an activity is exported and can be accessed externally:

> "This challenge isn't actually related to this screen and can be exploited at any point in the application!"

---

## 🛠Steps Taken

### 1. Listed all exported activities via ADB:

`adb shell dumpsys package com.example.miniandroidchallenges | findstr "Activity"`

This revealed:

`com.example.miniandroidchallenges/.activities.SecretActivity`

### 2. Launched the activity manually:

`adb shell am start -n com.example.miniandroidchallenges/.activities.SecretActivity`

In my case, I had to specify the device:

`adb -s 192.168.56.103:5555 shell am start -n com.example.miniandroidchallenges/.activities.SecretActivity`

### 3. Result
This started a hidden screen displaying:

> "Congratulations, you did it!"

This confirms the activity was unintentionally exported and accessible externally — a common security misconfiguration.


