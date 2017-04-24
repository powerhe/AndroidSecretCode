# AndroidSecretCode

# What's the android secret code?
In Android a secret code is defined by this pattern: *#*#<code>#*#*.
If such a secret code is executed, the system Dialer app will trigger this code:![AOSP Code](https://android.googlesource.com/platform/packages/apps/Dialer/+/91197049c458f07092b31501d2ed512180b13d58/src/com/android/dialer/SpecialCharSequenceMgr.java#131)

```
static private boolean handleSecretCode(Context context, String input) {
    int len = input.length();
    if (len > 8 && input.startsWith("*#*#") && input.endsWith("#*#*")) {
        Intent intent = new Intent(TelephonyIntents.SECRET_CODE_ACTION,
                Uri.parse("android_secret_code://" + input.substring(4, len - 4)));
        context.sendBroadcast(intent);
        return true;
    }

    return false;
}
```

# How to execute the secret code?
