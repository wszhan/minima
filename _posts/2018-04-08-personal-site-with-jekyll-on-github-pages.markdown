---
layout: post
title:  "Build Your Site on GitHub Pages with Jekyll"
date:   2018-04-08 00:15:00 +0800
categories: 
---

After spending almost a whole day on struggling with Jekyll, I found that most tutorials, as well as the Jekyll official documentation, might not be friendly to a noob like me.

So I decided to write a easiest-ever tutorial about building your website on GitHub Pages with jekyll.

**Category**:
* Register on GitHub
* Find a Jekyll Theme
* Fork
* Modify **\_config.yml**
* Modify **about.md**
* Add Posts
* Go to your site

### 1. Register on GitHub

**GitHub** is a great website, and **GitHub Pages** is a great option for most people to build their personal sites, especially suited for blog sites. The learning curve might be a little bit steep, but it is totally worth it.

Registrating on GitHub would be as simple as doing it anywhere else. The steps would be:
* Go to [GitHub.com](https://github.com/);
* Click **Sign up** on the top right;
* Enter your information, and please remember what your *username* is;
* Click **Create an account**.

And it is done.


### 2. Find a Jekyll Theme

Since Jekyll is an open-source project, there are a lot of themes available to you on the Internet. However, some themes might require more tuning than the others. This would not be a problem for pros, but for me it took literally a day to figure out how to set up the default, also the simplest, theme.

Thus I would suggest you pick up a theme from [this list](https://pages.github.com/themes/). The steps of setting up any one of them would be quite similar. I am using the default theme **Minima**, which is quite friendly for beginners.
You can preview the themes while browsing. This helps you choose.

However, if you want to take a shot and try some fancy themes, go for it. It is totally worth it.

### 3. Fork

After you choose a theme, go to the github repository of the theme. This page looks like [this](https://github.com/jekyll/minima).

At the top right corner, you would see a **Fork** button. Click it and wait.

After the forking is done, you would have a copy of the theme in your own repository.

Usually we clone the respository to our computers and modify them. But I would like to suggest beginners do it online.

Before modifying our files, one last thing to do:
* On your forked page, there is a bar close to the top with several options;
* click on settings;
* Rename your repository as **your_username.github.io**. For example, my GitHub username is *wszhan*, so my repository name would be **wszhan.github.io**. **This repository name would be your website address, so don't forget it**(Of course you can come back and take a look whenever you like).

Okay, let's go to the next step.

### 4. Modify **\_config.yml**

Click into it and change the first few lines and that would suffice.

The first 11 lines of the original **\_config.yml** file:
```
title: Your awesome title
author: GitHub User
email: your-email@domain.com
description: > # this means to ignore newlines until "twitter_username:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
# social links
twitter_username: jekyllrb
github_username:  jekyll
```


My **\_config.yml** file:
```
title: Weisi Zhan
author: Weisi Zhan
email: zhanwes@gmail.com
description: > # this means to ignore newlines until "twitter_username:"
  Talk is Cheap. Show me the code.
# social links
twitter_username: Weisi_Zhan
github_username:  wszhan
```

### 5. Modify **about.md**

Similarly, click in this file and change the content.

**NOTE**:

1. Leave this part intact
```
---
layout: page
title: About
permalink: /about/
---
```
You can change the rest as you like.

2. Use **Markdown** to edit.

If you want to display plain text without any formatting, such as *italic*, **bold**, skip this part.

You have to know about Markdown sooner or later, so please take a [crash course](https://www.markdowntutorial.com/) about it first.

This is a [Markdown cheat sheet](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf) for your future use, which I find really helpful.

This is what the text in a Markdown file looks like:
```
*This text will be italic*
**This text will be bold**
```

And how it looks like on the web page:

>*This text will be italic*

>**This text will be bold**

### 6. Add Posts

Finally, we come to the last step.

Find **\_posts** and click, you would see files with names like **2018-04-07-first-post.markdown**. **Remember**, you'd better use this format for the names of your future posts.

You can click on the existing files and find the garbage bin icon on the top right on the post. Click on them to delete them all.

Let's write our own new post now. Go back to the **\_posts** directory, and you will see a **Create new file** button. Click on it and:
1. Name your file in the format of **YYYY-MM-DD-NAME-NAME.markdown**. The file name must end with **.markdown**.
2. Edit the file using Markdown language.
3. While finishing the editing, go to the bottom and you will see a table called **Commit new file**. Come up with mnemonic hints as the title to remind yourself what you did about this particular post, and click on the green button **Commit new file**.

* If your want to re-edit the post in the future, omit step 1 and edit it directly. No need to create a new file if you do not intend to.

### 7. Go to your site

Remember what your repo name? It is **your_username.github.io**.

Enter this repo name in the browser address bar, and you will see your personal blog site is done! **Congratulations!**

Actually the GitHub Pages can be much more powerful than this, and you can take more advantage of jekyll. But so far we have achieved a lot! You are ready and well equiped now to find out more about building a personal website in the future.