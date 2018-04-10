---
layout: post
title:  "Installing Anaconda on EC2 Instance"
date:   2018-04-09 15:50:33 +0800
categories: 
---

![Anaconda](http://ijstokes-public.s3.amazonaws.com/dspyr/img/AnacondaCIO_Logo){:width="60%"}

For more information about installing TensorFlow on EC2 Instance, plase check **TensorFlow Version and Installation** part in [my another post]({{ site.baseurl }}{% post_url 2018-04-09-udacity-dlnd-p3 %}).

Although not required, but you are highly recommended to launch a new EC2 instance on AWS before proceeding, especially when your existing instance has been used and modified.

After you connect to the AWS instance in terminal, we can start the installation process.

If you are quite familiar with Anaconda, there is no need to read this post. The procedures are the same as they are on local machines.

Contents:
>1. Download Anaconda
2. Install Anaconda
3. Create New Environment
4. Install Necessary Libraries

## Download Anaconda

Go to the [Anaconda official website](https://www.anaconda.com/download/?lang=en-us) and choose a version that fits your machine/EC2 instance. I picked **Anaconda 3 for Python 3.6 on Linus** because I am using an **Ubuntu** instance. Copy the link of the Anaconda installation package.

Connect to the EC2 instance, and go to the root directory by type in terminal:
```
cd ~
```

Use ```wget``` to download Anaconda installation package to your root directory:
```
wget link-of-Anaconda-package
```

## Installing Anaconda On AWS

NOTE:
- Make sure the downloaded Anaconda installation package is in the root directory and
- you are in the **root directory** while trying to install Anaconda with bash.
Otherwise, things would get pretty weird.

After downloading the file to our machine, use ```bash``` command to run the file and install it(replace ```Anaconda3-5.1.0-Linux-x86_64.sh``` with the name of the file you download):
```
cd ~
bash Anaconda3-5.1.0-Linux-x86_64.sh
```

This can take a while.

## Create New Environment

Things can't just work out without bugs. So usually this error arises:
```
-bash: conda: command not found
```

Luckily it is not a tough problem. By one single command we can solve it out.

For Anaconda 2:
```
export PATH=~/anaconda2/bin:$PATH
```

For Anaconda 3:
```
export PATH=~/anaconda3/bin:$PATH
```

Now we can create a new environment:
```
conda create -n deep-learning python=3
```
Explanation:
- the command after ```create -n``` is the name of your newly-created environment. So the environment I am creating here is named "deep-learning".
- ```python=3``` specifies the Python version in my ```deep-learning``` environment. If not specified in detail, this command installs Python 3.6 on my machine. So if your demand is more specific, your can provide more information in the command, such as ```python=3.5```, in which case my environment would have Python 3.5.

After the environment is created, you can check by
```
conda info --envs
```

You will see results similarly to mine:
```
wzhan ~ $ conda info --envs
# conda environments:
#
DAND                     /Users/wzhan/anaconda/envs/DAND
dlnd                     /Users/wzhan/anaconda/envs/dlnd
deep-learning            /Users/wzhan/anaconda/envs/deep-learning
```

## Install Necessary Libraries

If you want to install libraries into an environment, or you want to use that environment, you have to activate the environment first by
```
source activate deep-learning
```

Only after the above command, we can install desired packages into the target environment.

The installation command is pretty straightforward:
```
conda install numpy pandas
```

But sometimes it can be
```
conda install -c conda-forge some-package
```
Here the command ```-c conda-forge``` are specifying the **channel** from which we are getting the package. The default channel is ```-c anaconda```, which we don't have to specify if we are using the default channel.

You can find all Anaconda packages [here](https://anaconda.org/anaconda/repo). Search for anything you want and just follow the instructions.


References:

- [Getting Spark, Python, and Jupyter Notebook running on Amazon EC2](https://medium.com/@josemarcialportilla/getting-spark-python-and-jupyter-notebook-running-on-amazon-ec2-dec599e1c297)

- [How to run Conda?](https://stackoverflow.com/questions/18675907/how-to-run-conda?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

- [Download Anaconda Distribution](https://www.anaconda.com/download/#linux)

- (Optional)[How to uninstall Anaconda completely from MacOS
](https://stackoverflow.com/questions/42182706/how-to-uninstall-anaconda-completely-from-macos?rq=1)