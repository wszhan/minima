---
layout: post
title:  "Problems with Jupyter Notebook on AWS"
date:   2018-04-10 15:50:33 +0800
categories: 
---

While using AWS, I am always using Jupyter Notebook in Anaconda environments, so this post is exclusively about Jupyter notebook with Anaconda.

If you want to know more about installing Anaconda on AWS, check [here]({{ site.baseurl }}{% post_url 2018-04-09-installing-anaconda-on-ec2 %}).

## Install Jupyter Notebook with Conda

There are **two necessary steps**:
- activate your conda environment;
- install jupyter notebook with conda command.

```
source activate your-envs
conda install jupyter notebook
```

## Start Jupyter Notebook Server

Before this step, make sure that you add **a security group** in your AWS instance. I added a security group named **Jupyter** and set its TCP source IP to be ```0.0.0.0```. I am using this IP below.



```
jupyter notebook --no-browser --ip=0.0.0.0
```
You can even specify the port you want to use.

You will see the following message.

```
(deep-learning) ubuntu@ip-188-254-234-567:~$ jupyter notebook --no-browser --ip=0.0.0.0
[I 06:29:23.190 NotebookApp] Serving notebooks from local directory: /home/ubuntu
[I 06:29:23.190 NotebookApp] 0 active kernels
[I 06:29:23.190 NotebookApp] The Jupyter Notebook is running at:
[I 06:29:23.190 NotebookApp] http://0.0.0.0:8888/?token=sdjf8wefhdiufoiuasdf9wef33cc9da4sdfkjwe93238c71c
[I 06:29:23.190 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```

Copy this address
```
http://0.0.0.0:8888/?token=sdjf8wefhdiufoiuasdf9wef33cc9da4sdfkjwe93238c71c
```
to your browser address bar, and replace the ```0.0.0.0```(this address might differ according to your security group setting on AWS) with the **IPv4 Public IP** of your instance.

## Restart Jupyter Notebook Server

Sometimes if I terminate a Jupyter Notebook session and restart it, the port generated is not 8888, and with ports other than 8888 I can never connnect to the Jupyter Notebook server(no idea why, at least for now). So I have to find out the PID of 

Replace the port# with the port number you use. For me, it is always 8888.

```
netstat -tulnp | grep <port#>
```

And you will find the 4-digit **PID** of your previous session that is listening on port 8888.

NOTE: **DON'T DO THIS WHILE YOU ARE STILL USING THE PREVIOUS SESSION.**
Use the following command to kill the previous session that is out-of-date:
```
kill -9 <PID>
```

Now nothing is listening on port 8888, we can start a new Jupyter Notebook session.

References:

- [How to check opened/closed port on my computer?](https://askubuntu.com/questions/538208/how-to-check-opened-closed-port-on-my-computer?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

- [Who is listening on a given TCP port on Mac OS X?
](https://stackoverflow.com/questions/4421633/who-is-listening-on-a-given-tcp-port-on-mac-os-x)