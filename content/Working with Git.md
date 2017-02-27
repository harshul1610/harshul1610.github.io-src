Title: Working with git
date: 2017-02-27 19:32
category: Pelican
tags: Git, Blog, Pelican
author: Harshul Jain
excerpt: This is an excerpt of my post.


My name is Harshul Jain, and I am the part of this Open source world. It is the world, where good and bad practices for creating the softwares are followed. I look on both the ways, but prefer to use the most preferrable way of developing software.

Development of Github platform was started on around 1 October 2007 and the site was launched in April 2008. This
site is known for holding the repositories of world's greates projects. Some of these projects are Cpython, Pandas, Spark etc. I am a contributor to some of these, and a FOSS enthusiast as well. During my early stages, I used to face the issue with ecosystem of git. I was not able to recognize the exact flow of commands. So I thought of documenting a Process that may help any one.

** Fork the Repository **
First thing that we should do when starting to work for any project is, Fork a project. We will call the repository as forked repository. Repository from which fork is created is called as upstream repository for me.
Forking is done via Github and pretty easy for any developer. developer just needs to visit the upstream repository github url and press fork button.

** Clone your forked repo and make remote connections**
Once you have forked repository on github with you, you will need to clone that repository to your local machine.
We are doing this because all the development stuff will be done on local machine. So for cloning the repository
do the folowing from your terminal:
```
git clone <github forked repository url>
git remote add ups <github upstream repository url>
git remote add home <github forked repository url>
```

** Follow the build process **
By now you should have the project repository on your local machine. So you should build the project as per the project guidelines. For this you should follow the README.md present in project repository. It will walk you through the right way of building the project.

Always try to understand the build process clearly, as it is one of the key process of development. Without the proper builds, your changes are not valid.

** Create a feature branch **
Once you have completed the above three steps, you are ready to be a contributor to the project. Let us suppose, while iterating through bug list, you found an issue that you can improvise or solve, you must follow the below proceedure:

Be inside the updated master branch | Make and checkout a feature branch
```
git checkout -b feature_branch_xyz
```
** Changes and Commits **
Now say, you woked on some code refactoring, and you are able to solve the issue. you will need to save your work and push the changes to your forked repository at first.

local repository --> Forked Repository

For this follow the following proceedure:

```
git add <file1>
git commit -m "<commit message>"
git pull --rebase ups master
```
git pull --rebase command, fetches the updated changes made by other people and apply your commits on top of 
other previous commits. This command does not create any merge commits, and thus makes a clean linear history. This is the magical command of git.

** Push your changes **
Push your commits to the forked repository but in a sepparate branch.
```
git push -f home feature_branch_xyz
```

This way you will be able to work on different issues simultaneously in separate branches.

** Make a Pull request | When Merged | update the master **
by now, your forked repository on github has updated code that can solve an issue. And all of this is present in separate feature branch. Now you will raise a pull request using github to Master branch of upstream repository.

i.e.,
Forked feature branch --> Master branch

** Changes are accepted **

If the chanages are accepted and merged into your master, you will update the master in your local repository on your local machine.

For this do the following:

```
git checkout master
git pull --rebase ups master
git push home master
```

** Changes are rejected **

If changes are rejected, you will work on more changes as per suggestions and code review and do the following:
```
git add <file1>
git commit -m "<commit message>"
git pull --rebase ups master
git push -f home feature_branch_xyz
```