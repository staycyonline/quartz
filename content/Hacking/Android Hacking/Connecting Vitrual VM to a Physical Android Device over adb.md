# Connecting VitrualBox VM to a Physical Android Device over adb
Tags: #android #adb #hacking #setup #mobile #remote-machine
Related to: #virtualbox #mobexler #bug-bounty #lab
See also: 

#### Summary
My notes on how to connect Mobexler VM on VirtualBox with a physical android device

#### Steps to connect
1. Start an adb server on the machine(host) that is connected to the physical device  using the command `adb -a -P <port number> nodaemon server`. Default port being 5037
2. Make sure that the VM and the host is connected to the same network for this to work. I used ==Bridged Adapter== on the VBox VM.
3. Note the IP address of the host machine.
4. Use the following command inside VM `adb -H <Host IP> -P <Port Number> devices`
5. You can see the connected devices. 
6. Use other adb commands by replacing `devices`

###### References  (optional )
 [Deploy and execute an android application on a device connected to a remote system](https://stackoverflow.com/questions/27245597/how-can-i-deploy-and-execute-an-application-on-a-device-connected-to-a-remote-sy)
 