---
title: Why Github?
categories: article
tags: tech git
author: Chen Yiyang
image: "/assets/img/2018-09-09-why-github-preview.jpg"
questions:
- question: "Which of the following is not true about Github? "
  answer: 
  - text: "You can collaborate with others on the same Github project."
    correct: false
  - text: "You can fork any repo from others on Github."
    correct: true
  - text: "You can change your project to any previous versions on Github."
    correct: false
  - text: "You can make changes on a repo you don’t have access to by forking it."
    correct: false
- question: "Which git command enables you to saves the changes made like a snapshot, before updating the remote repo? "
  answer: 
  - text: "git save"
    correct: false
  - text: "git add"
    correct: false
  - text: "git commit"
    correct: true
  - text: "git push"
    correct: false
---

You may have heard of [Microsoft’s acquisition of a tech company called Github for $7.5bn a few months ago](https://www.bbc.com/news/technology-44351214). Why is Microsoft willing to pay such a high price for a tech company of merely 800 employees, and what exactly *is* Github?

Some developers would tell you that Github is a web-based code sharing and publishing service, while others might call it the largest social networking site for programmes. Well,  both these statements are true. You may think of Github as a ‘Google Drive’ for developers, where they can create folders (“repositories” on Github, or “repo” for short) and upload files for their projects, and add collaborators to work on the projects. In addition, the open source project Git is a version control system that records down the full history of the repos and allows the users to compare or switch back to previous versions of their projects easily. “But why are developers so excited about Github? Why not just Google Drive? Version Histories are also available on Google Docs and I think they are easy to use as well.” You may wonder. Indeed, all the functions mentioned above are powerful, but they are not the reason why Github stands out. Before we talk about the uniqueness of Github, I want to introduce to you this concept called “Open Source”

![][image-1]

According to Wikipedia, open source software is a type of computer software developed in a collaborative public manner, and whose source code is released for everyone to study, change and distribute for any purpose. However, before Github, the way developers contribute to an open source project is to download the source code others have published, make changes on their own computers, and email back the edited versions, which is a very tedious process, and sometimes when many people in the community send their own modified version of the project, it is insanely demoralising for the publisher to incorporate changes made by different programmers into the project manually.

However, all these are changed with the three flagship functions of Github - fork, pull request and merge. To fork a Github repo from others , you copy it to your account and can modify it as you want. When you have finished editing and feel that you have improved the project, you can send a pull request back to the user from whom you have forked the repo. If the user would like to incorporate your changes, he can “accept” the pull request with a click of a button and merge the changes from your repo to the original one. These functions enable the users to work on open source projects very conveniently, and they also win Github the affection of the community! (Though Github does provide users with private repos which are hidden from the public and cannot be forked by the public.)

After reading all the thrilling stories of Github and Open Source, do you want to start your journey of contributing to the Open Source community? You can start by learning to use the basic commands for Git, the version control system [here](https://guides.github.com/introduction/git-handbook/). Even though Github also provides a web-based graphical interface, and you do not necessarily need to learn Git to use Github. It is always recommended and these commands allow you to operate with large amount of files at a time effortlessly.

In addition, do you remember the Google Code-In competition which you can finish tasks regarding open source projects and win cool Google t-shirts? Google Code-In 2018 is coming soon! For this year, it will start in October. Do look out for outreach emails that are going to be sent by DHS Infocomm Club and participate in the competition!!!

Meanwhile, let’s quickly master the skill of using Git :D

[image-1]: {{ "/assets/img/2018-09-09-why-github-1.png" | absolute_url }}

Ref.

[https://techcrunch.com/2012/07/14/what-exactly-is-github-anyway/](https://techcrunch.com/2012/07/14/what-exactly-is-github-anyway/)