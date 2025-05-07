# Challenge 3 - Mirror Mirror on the Wall (Reflected XSS in WebView)

## Challenge Description
> The webview below takes in and reflects input from the textbox. Try doing something fun with this!
> _(Note: there's no flag or success screen for this.)_

## Objective
The goal is to exploit a **reflected Cross-Site Scripting (XSS)** vulnerability in an Android `WebView`.

The challenge reflects user input into the page using a `WebView` and enables JavaScript. If the input is not sanitized, malicious code can be injected and executed.

---

## Steps Taken

1. I launched the APK in BlueStacks.
2. I entered this payload into the input field:
   ```html
   "><script>alert('XSS')</script>
3. Pressing the "OK" button caused the JavaScript alert() to execute, confirming XSS. Decompiled the APK using JADX to inspect the implementation:
Found `ChallengeThree.java` in the `com.example.miniandroidchallenges.frags` package.
   Confirmed the vulnerable line:
   ```html
   webView.loadData(editText.getText().toString(), "text/html", "UTF-8");
Also noted JavaScript is explicitly enabled with:
      `webView.getSettings().setJavaScriptEnabled(true);`
    
## Why This Is Vulnerable
User input is passed directly into the WebView without encoding or validation.
JavaScript execution is enabled.
Therefore, any HTML/JS inserted into the input field will be executed as part of the page.
