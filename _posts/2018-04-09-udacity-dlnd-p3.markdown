---
layout: post
title:  "Problems with Project 3 of Udacity Deep Learning Nanodegree"
date:   2018-04-09 16:50:33 +0800
categories: 
---

>NOTE:
I successfully finished my third project with all the solutions I am sharing here. However, I could not guarantee that they work for you too. Better check [summary](#summary) before moving forward on this post.

Contents:
* UTF-8 locale issue
* TensorFlow Version
* TensorFlow Installation
* The Mysterious Training Loss
* Summary

## 1. UTF-8 locale issue

If you have the same problem as I did as follows:
```
---------------------------------------------------------------------------
UnicodeDecodeError                        Traceback (most recent call last)
<ipython-input-4-ca321744a313> in <module>()
      5 
      6 data_dir = './data/simpsons/moes_tavern_lines.txt'
----> 7 text = helper.load_data(data_dir)
      8 # Ignore notice, since we don't use it for analysing the data
      9 text = text[81:]

~/p3-tv-script/helper.py in load_data(path)
      9     with open(input_file, "r") as f:
     10     #with open(input_file, "r", encoding='utf_8', errors='ignore'):
---> 11         data = f.read()
     12 
     13     return data

~/anaconda3/envs/dlnd-tf-gpu/lib/python3.6/encodings/ascii.py in decode(self, input, final)
     24 class IncrementalDecoder(codecs.IncrementalDecoder):
     25     def decode(self, input, final=False):
---> 26         return codecs.ascii_decode(input, self.errors)[0]
     27 
     28 class StreamWriter(Codec,codecs.StreamWriter):

UnicodeDecodeError: 'ascii' codec can't decode byte 0xc2 in position 17: ordinal not in range(128)
```

Line 10 might be different from the one in your ```helper.py``` file, but it doesn't matter.

Use your text editor to open the ```~/.bashrc``` and ```~/.profile``` files and append the following lines:
```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
```

Run the following command to find out what locales are currently defined for the current account([reference: How do I fix my locale issue?](https://askubuntu.com/questions/162391/how-do-i-fix-my-locale-issue?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)):
```
locale
```

And reconfigure them:

```
sudo dpkg-reconfigure locales
```

Use up and down arrow keys and ```Enter``` to choose and confirm the reconfiguration.

NOTE: The bug didn't go away until I **restarted jupyter notebook server**.

## 2. TensorFlow Version

Make sure you know what version of tensorflow-gpu needed for your project before you install tensorflow GPU. Projects in different time period or in different languages require different versions of tensorflow-gpu. For example, the global version of project 3 requires tensorflow version later than 1.3.0; however, the Chinese version requires [tensorflow version of 1.0.0, or 1.0.1 in some cases](https://discussions.youdaxue.com/t/p3/44550).

Besides, be aware of the Python version of the environment in which you are going to install tensorflow-gpu and with which project 3 is to be done. After ```source activate your-env```, you can check your Python version by type
```
python --version
```
in your terminal. 

## 3. TensorFlow Installation

There are two ways to install TensorFlow-GPU on your EC2 instance. Any one of them that works for you would be fine (which means that one of them might not work, as in my case).

### i. Install tensorflow-gpu with pip

**```pip install``` doesn't work for me.** I am still listing it here because some students on slack  said this work for them. Better have one more option.

```
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.3.0-cp35-cp35m-linux_x86_64.whl
```

The above means that I am intalling a ```1.3.0``` version GPU-supported TensorFlow (```tensorflow_gpu```) for Python of version 3.5 ```cp35```.

### ii. Install tensorflow-gpu with conda

Installing ```tensorflow-gpu``` with ```conda``` command might have potential compatibility issues, but ```pip``` version of tensorflow-gpu doesn't work for me, but the conda version does. Always go with the one that fits your situation.

After having installed conda and befoer ```conda install``` TensorFlow, make sure you ```source activate``` into the target environment.

Before install conda, check [this page](https://anaconda.org/anaconda/tensorflow-gpu) first and take a look at ***the different versions for different operating systems***, especially when you are not using AWS Ubuntu EC2 instance as I did.

I am using AWS Ubuntu, so I will be installing the linux 1.4.1 version of ```tensorflow-gpu```.

Then type the following command:
```
conda install -c anaconda tensorflow-gpu
```


## 4. The Mysterious Training Loss

It throws no error but you can tell something is wrong with the model.
```
Epoch   0 Batch    0/16   train_loss = nan
Epoch   0 Batch    1/16   train_loss = nan
Epoch   0 Batch    2/16   train_loss = nan
Epoch   0 Batch    3/16   train_loss = nan
Epoch   0 Batch    4/16   train_loss = nan
Epoch   0 Batch    5/16   train_loss = nan
Epoch   0 Batch    6/16   train_loss = nan
Epoch   0 Batch    7/16   train_loss = nan
Epoch   0 Batch    8/16   train_loss = nan
Epoch   0 Batch    9/16   train_loss = nan
Epoch   0 Batch   10/16   train_loss = nan
Epoch   0 Batch   11/16   train_loss = nan
Epoch   0 Batch   12/16   train_loss = nan
Epoch   0 Batch   13/16   train_loss = nan
Epoch   0 Batch   14/16   train_loss = nan
Epoch   0 Batch   15/16   train_loss = nan
```

**There are two possible pitfalls for this error.** I can't post my code here because it is against the [Udacity Honor Code](https://www.udacity.com/legal/community-guidelines). So I will share some hints that helped me out here. Usually the bug might reside in yoru ```create_lookup_tables``` function, that is the first function you must implement.
* The two outputs are dictionaries, they should not contain duplicate keys or values.
* The integer values that represent the words should start from 0. I haven't got any idea how this causes the ```nan``` training loss, but it did. I believe that most people who finished the previous **Sentiment Prediction RNN** exercise would, just as I did, start the value from 0. **Please share with me if you know why this is an issue.**

Look into ```problem_unittests.py``` to see how this function is tested, if necessary.

## Summary

While facing all these complicated structures and numerous function definitions, still we should keep in mind that we are actually writing with templates. In industrial production, we have to start every single expression from scratch and put all together into a giant project. What I am saying is that even though we are banging our heads and still have no idea why come all these bugs, we are lucky enough.

However, to avoid all these pitfalls for the future projects, which might be even bigger and more complicated, it is useful and significantly necessary to keep some principles in mind:

- **The type of the data your functions take as inputs and returns/yields.**
- **The shape of the inputs and outputs**
- **The version of the libraries in your environment.**

All these seem trivial but they are not.

Reference:

- [How to set up a clean UTF-8 environment in Linux](https://perlgeek.de/en/article/set-up-a-clean-utf8-environment)

- [Deep Learning Nanodegree FAQs - For the Chinese Version Project](https://discussions.youdaxue.com/t/topic/44102)