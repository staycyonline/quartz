https://developer.android.com/reference/android/Manifest.permission
https://developer.android.com/guide/topics/manifest/manifest-intro

things to look for Android manifest.xml 

Unnecessary permissons
activity exported = true

content providers- exported
hardcoded creds

backup true
debug true

---
decompile using apk apktool

```
apktool d appname.apk  # -f -r 
```


or use jadx gui

---

gets a decoded folder

lib to inject objects

.so files might have keys

original has android manifest.xml

smali - has app src code

---
Hardcoded strings

resources/strings.xml

can be found in activity source code

google api keys can cost money to perople

look for urls, buckets, keys,, secrets

use search featue of jadx

find locations of dbs

---
Start an exported activity

am start apppackagename/.activityname


---
# Enumerating AWS Storage buckets

**Cloud Enum Link**: [https://github.com/initstring/cloud_enum](https://github.com/initstring/cloud_enum)

**AWS CLI:** sudo apt-get install awscli

**AWS CLI Documentation:** [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)

---
# Enumeration of Firebase

**Firebase Enum Github:** [https://github.com/Sambal0x/firebaseEnum](https://github.com/Sambal0x/firebaseEnum)

find endpoints and try to access url/.json endpoint

Some firebase areas may be out in the open while some is protected

---
# Automating static analysis

**MobSF Github Repo:** [https://github.com/MobSF/Mobile-Security-Framework-MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF)

**MobSF Dependencies:** [https://mobsf.github.io/docs/#/requirements](https://mobsf.github.io/docs/#/requirements)

**wkhtmltopdf to generate PDF Reports:** [https://wkhtmltopdf.org/downloads.html](https://wkhtmltopdf.org/downloads.html)

---
Whats deeplink

---
