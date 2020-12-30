---
layout: post
title: "Gengyuan's back-end deployment progress!"
date: 2020-12-28
---

Gengyuan did the following things today:

1) Installed Docker Desktop.

2) Enable the Windows Subsystem for Linux.

3) Update to WSL2(Windows Subsystem for Linux)

4) Enable Virtual Machine feature

5) Download and install the Linux kernel update package

6) Set WSL 2 as your default version

7) Install your Linux distribution of choice - Ubuntu

8) Install Windows Terminal

9) Set your distribution version to (WSL 1) or WSL 2 : After checking Windows updates and restart, it finally works!

10) Ensure that Docker Desktop is [configured to use the WSL2 backend](https://docs.docker.com/docker-for-windows/wsl/)

11) Create the first test Laravel Project - /Users/gyzha/example-app

12) The test Laravel application can be accessed by http://localhost, success!

13) Installed the PHP language (test in cmd by "php -v") and Composer (test in cmd by "composer -V")

14) Using PHP and Composer to create Laravel project (much more convenient). Note: be sure to follow [this](https://stackoverflow.com/questions/52734707/your-requirements-could-not-be-resolved-to-an-installable-set-of-packages-for-la) before using composer. one of the internal php file (php.ini in php7 folder) needs modification:

 extension=fileinfo needs to be uncomment.




