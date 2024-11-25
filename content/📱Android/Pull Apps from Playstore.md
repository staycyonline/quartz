Summary of How to Pull APK From Play Store:

1.Download app from Play Store
2 In terminal issue the following commands:
3.adb shell (this drops you into a shell on your emulator or physical phone)
4.pm list packages | grep <insertIdentifier> (this will display the name of the package installed on the phone, in our case we did grep injured, copy result for step 5 below)
5. pm path <insertpackagename> (list the file path of the package, copy the file path for step 7 below)
6. exit (exit the adb shell)
7. adb pull <insertPathToPackage> <insertNameOfNewFile>.apk (this will pull the apk from the file path on the phone and save it to whatever file name we want