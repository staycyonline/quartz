Tags: #aws #pentesting 
Related to: #s3-buckets 
See also: [[BlackSky Hailstorm AWS]] 

![[Pasted image 20230719223811.png]]

There is a .git file in the repo

Lets try downloading it.

Lets run git log to see commit history

![[Pasted image 20230719224726.png]]

We see  a special commit

Lets revert to the pervious commit (make sure you are outside the .git folder)
![[Pasted image 20230719225317.png]]

![[Pasted image 20230719225352.png]]

we see the access keys 

>access_key AKIAJ366LIPB4IJKT7SA
secret_access_key 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

Let us configure a profile named flaws using the keys

![[Pasted image 20230719225718.png]]

To see all the buckets a profile runs - `aws --profile flaws s3 ls`

![[Pasted image 20230719225911.png]]

http://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud/ - link to next level