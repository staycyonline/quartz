**MobSF Dynamic Analysis Documentation:** [https://mobsf.github.io/docs/#/dynamic_analyzer](https://mobsf.github.io/docs/#/dynamic_analyzer)

**How to Add Files to your Path Variables:**

1. **(Windows)** [https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/)
2. **(Linux/Mac)** [https://www.baeldung.com/linux/path-variable](https://www.baeldung.com/linux/path-variable)

**Commands Utilized:**

- emulator -list-avds
- emulator -avd <AVD_Name> -writable-system -no-snapshot

Then, start MobSF:

- Windows - (navigate to MobSF directory), run.bat
- Linux/Mac - (Navigate to MobSF Directory), run.sh

Upload your apk, and then click "Start Dynamic Analysis", and then click "MobSFy Emulator"

  

---

  

When starting the dynamic analyzer you may receive an error similar to "Error Running ADB Command", please refer to this github troubleshooting document [https://github.com/MobSF/Mobile-Security-Framework-MobSF/issues/1127](https://github.com/MobSF/Mobile-Security-Framework-MobSF/issues/1127) or add adb to your PATH variables.