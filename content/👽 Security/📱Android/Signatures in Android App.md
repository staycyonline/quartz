# Signatures in Android App
Tags: #signature #android #mobile 
Related to: #bug-bounty , #hacking #tools  
See also: 

#### Summary
Introduction to signing Android appliations

#### Signing an Android App
- Therer are no certificate authorities for android
- Devs can generate their own certs
- App signed with public key and private key stays with the owner.

#### Steps to sign an app
1. Use **keytool** to generate a key
	- Use command 
	`keytool -genkey -v -keystore [nameofkeystore] -alias [your_keyalias] -keyalg RSA -keysize 2048 -validity [no of days]` 
2. Sign the app using **jarsigner**
	- Use command
	  `jarsigner -verbose -sigalg MD5withRSA -digestalg SHA1 -keystore [name of keystore] [path to apk file] [your key alias]`
3. Verify the key with **jarsigner**
	- Use command
	`jarsigner -verify -verbose [path-to-apk file]`

#### Verifying app signature
 1. Unzip the apk file using command
	 `unzip [path to apk]`
2. Print signature 
	`keytool -printcert -file META-INF/CERT.RSA`
3. Display signature of included files
	`cat META-INF/CERT.SF`

- _Manifest.MF_ file declares the resources.

- _Cert.RSA_ is the public key certificate

- _Cert.SF_ contains signature of included files

###### References  (optional )
[Use of Manifest.MF in java](https://stackoverflow.com/questions/12767886/use-of-the-manifest-mf-file-in-java)
