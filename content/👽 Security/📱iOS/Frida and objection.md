https://github.com/fkie-cad/friTap/issues/37

frida-ls-devices - lists the devices connected in the PC
get serial number

frida -D Device_serial DVIA-v2

objection -S Device_serial -g DVIA-v2 explore

https://codeshare.frida.re/ - get scripts for frida

---
In android when u try to patch a kotlin app you might get an error

invalid resource directory name: /home/framework/debug/app-debug/res navigation

This is because kotlin uses aapt2

Use below code to patch app to remediate the error

```
objection patchapk -s apnmae.apk --use-aapt2
```