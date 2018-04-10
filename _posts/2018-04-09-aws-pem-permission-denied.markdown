---
layout: post
title:  "Permission Denied Problem while Connecting to AWS EC2 Instances"
date:   2018-04-09 15:45:33 +0800
categories: 
---

Usually this error arises when it is the first time to connect to AWS. Once this problem is solved, you can connect to AWS successfully using this key.

The error looks like this (the wild card characters represent your information, such as your path, username, keyname, etc.):
```
~ $ ssh -i ~/***.pem ubuntu@88.88.88.88
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '***.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "****.pem": bad permissions
ubuntu@****: Permission denied (publickey).
```

In the terminal, go to the directory where you keep the ```.pem``` key, and type the following command(**replace the *** with your keyname**)
```
chmod  600 ***.pem
```

You can make sure the permission is changed by type the following command:
```
ls -la
```

And you should see the ```.pem``` file should have the permission as
```
-rw-------@  1 kevin  staff  1696 Apr  9 15:35 key1.pem
```
or
```
-rwx------@  1 kevin  staff  1696 Mar 13 21:15 key2.pem
```

Both permissions should work.

If it still doesn't work, make sure you have checked the following three problems:
* The key is correct, corresponding to the instance you are trying to connect;
* The username is correct. You can see from above that I am connecting to a Ubuntu instance, thus my username is ```ubuntu@88.88.88.88``` before the asperand sign.
* The host is correct. In the above example, the host name is 88.88.88.88 in ```ubuntu@88.88.88.88```. Of course, this is just an example, your host should definitely be different.

If all these fail, just Google your problem. It is very possible that someone else might have had the problem and posted it somewhere. Fortunately, it is solved and the solution is also online.

References:

- [Permission denied (publickey) when SSH Access to Amazon EC2 instance
](https://stackoverflow.com/questions/18551556/permission-denied-publickey-when-ssh-access-to-amazon-ec2-instance?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)