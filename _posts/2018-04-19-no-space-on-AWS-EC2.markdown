---
layout: post
title:  "Running Out of Space on AWS EC2 Instance"
date:   2018-04-19 15:52:00 +0800
categories: 
---

It is easy to run out of space on AWS EC2 instance. There could be many reasons and also there are some workaround with which you can avoid this problem. But when this problem occurs, this is what we can do.

First, while I am downloading the [**CelebA**](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) dataset via `wget`, I got no error but this prompt:
```
Saving to: ‘celeba.zip’

celeba.zip                 88%[=============================>     ]   1.18G  50.7MB/s    in 28s


Cannot write to ‘celeba.zip’ (Success).
```

The steps are as follows(I will try to provide as detailed information as possible):

1. In your EC2 instance, use this command `df -h` to confirm you are running out of space, this is my output:
```
Filesystem      Size  Used Avail Use% Mounted on
udev             30G     0   30G   0% /dev
tmpfs           6.0G  8.6M  6.0G   1% /run
/dev/xvda1       49G   48G  1.2G  98% /
tmpfs            30G     0   30G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs            30G     0   30G   0% /sys/fs/cgroup
tmpfs           6.0G     0  6.0G   0% /run/user/1000
```

Clearly I didn't have much space left.

2. From aws console, click on the instance which you want to add more space, and from the **Instance Description**, check the name of `Root Device`, take a note of it.

3. Stop the instance.

4. Click `Volumes` within `ELASTIC BLOCK STORE` on the left panel, right click the volume connected to your instance, choose `Detach Volume`.

5. Right click again, choose `Create Snapshot` and follow the instruction.

6. On the left panel within `ELASTIC BLOCK STORE` click `Snapshots`, right click the snapshot you just create, choose `Create Volume`.

7. On the `Create Volume` page, set the `Size(GiB)` larger than the current size of your instance, as large as it will create enough extra space for your new project. For mine, it is 50 by default, and I set it to be 60.

8. Make sure you choose the correct **`Availability Zone`**, note that `us-west-2a` and `us-west-2c` are different. And click the `Create Volume` button.

9. Since we have the new volume, go back to the `Volumes` page, and right click the volume you just create, choose `Attach Volume`. Here you need 2 pieces of information:
- `Instance`: copy your `Instance ID` and paste it here;
- `Device`: remember the `Root Device` name you took note? Type it here.

10. And here you go. Start the instance and you will have extra space. You can check by the command `df -h`:
```
Filesystem      Size  Used Avail Use% Mounted on
udev             30G     0   30G   0% /dev
tmpfs           6.0G  8.6M  6.0G   1% /run
/dev/xvda1       59G   50G  8.2G  86% /
tmpfs            30G  4.0K   30G   1% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs            30G     0   30G   0% /sys/fs/cgroup
tmpfs           6.0G   12K  6.0G   1% /run/user/1000
```

You can tell I have 10GiB more. Let's do our new project then.

References:

- [Not enough disk space '/' in AWS instance](https://askubuntu.com/questions/118094/not-enough-disk-space-in-aws-instance?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

- [EC2 instance on Amazon and I am greeted with “No space left on the disk”
](https://stackoverflow.com/questions/6151695/ec2-instance-on-amazon-and-i-am-greeted-with-no-space-left-on-the-disk?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)