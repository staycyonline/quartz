copy the ipa into zip and transfer to iphone.

find location of the folder using `find . -name "myFile*" `

use unzip to unzip the file

unzip the ipa file

you find  a directory called Payload

move Payload/app_name.app to /Appilications
chmod +x /Applications/app_name.app/binary_name

then run `uicache` as root or mobile user


Vuln apps - https://github.com/lucideus-repo/UnSAFE_Bank
	https://github.com/prateek147/DVIA-v2
	https://resources.infosecinstitute.com/topic/getting-started-damn-vulnerable-ios-application/