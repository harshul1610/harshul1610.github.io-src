Title: Working with pelican
date: 2016-07-28 19:32
category: Pelican
tags: Python, Blog, rst, Pelican
author: Harshul Jain
excerpt: This is an excerpt of my post.


I am a Python developer, and an active document making guy. I love making documents through Blogs and over sphinx
because it helps other developers understand, and contribute on what I love to do. It has been 2 months when
I started preparing the blog with Django. Yeah a Dynamic blog with Django, which fetches the blog data from a database.
I was happy at that time that I could complete that stuff, but it now makes me feel sick on my thinking now. Because
including database in my Blog will only put delays in blog site.

So, I tend to switch to [Pelican](http://getpelican.com), which is a static site generator. For documentation you can
always hit on [here](http://pelican-cn.readthedocs.io). For now, Let us see how far we can learn here:

1. **Quickstart** : For a Quickstart prefer going on this [blog](https://fedoramagazine.org/make-github-pages-blog-with-pelican/)
 This blog will give you complete start to your pelican project and even get your project publish on Github. It is super easy.

2. **Adding Themes**: For this, you have to fork [Flex Theme](https://github.com/alexandrevicenzi/Flex/tree/608e6925ab629324e6cc9cff9b459d1bbad07e4a)
 in your project directory. Instructions are well written in Flex/README.md file by author. In your ``pelicanconf.py`` file
 put ``THEME = "~/Flex"``. Run ``make html`` and ``make serve``. view the updated page. By the way, even I'm using
 [Flex theme](https://github.com/alexandrevicenzi/Flex), it's responsive, mobile first and good looking.
 Don't thank me. Thank the [original author](https://travis-ci.org/alexandrevicenzi/Flex).

3. **Adding Content**: Since we have something working now, we will now focus on making content for our blog site. All
the content related to the page is written in either in .md or .rst format under content directory of your project.
So, for a blog on ``testing`` we will make a ``testing.md`` file in ``content`` directory. If you do not understand what are .md
files, you must google about it. It is a markdown language, that you can write your content in form of. After writing the
testing.md file run ``make html`` and ``make serve`` commands in terminal to update the html files and host those updated
files on your local server. I will suggest writing the content in .md file than .rst file. .md files are pretty
easier to create.

4. **Writing [about me](harshul1610.github.io/pages/about-me.html#about-me) page**:
For this at first put ``DISPLAY_PAGES_ON_MENU=True`` in ``pelicanconf.py`` file. This is the file where you will get all settings
related to website being configured. when we run make html it is this file variables that are picked up by system. Do not
be in hurry to view the about me page in web site, because we still have not created it. we have just enabled the settings.
To create 'aboutme.html' using ``make html`` you have to write your aboutme.md or ``aboutme.rst`` file and put it under pages directory
in content directory. now run ``make html`` and ``make serve`` and view the updated page.

5. **Social Buttons**: You can definitely add them just by putting ``SOCIAL = (('facebook', url ),)``
 in ``pelicanconf.py``. For more social configurations, you have to check about that theme. Best way to get the info of that
 theme is github. Some themes don't have social media handling in them. But Flex does and that is why it is amazing.

6. **Adding syntax highlighting**: For implementing the syntax highlighting in your blog, you just have to write your code
snippet between two ``. Remember default pygment used is github, you can always change that. It depends
on the theme you are using.

I hope this gives you the quick start good enough to create your own blog and host it via github pages.





