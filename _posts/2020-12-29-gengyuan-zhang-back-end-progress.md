---
layout: post
title: "Gengyuan's back end progress!"
date: 2020-12-29
---

Gengyuan did the followings today:

1) Installing MySQL from [here](https://dev.mysql.com/doc/refman/8.0/en/windows-installation.html).

2) Installing MySQL workbench.

2) Installing Microsoft Visual Studio 2019 Community

3) After fixing the "undefined index" problem with the help from [here](https://stackoverflow.com/questions/64620849/laravel-packagemanifest-php-line-131-undefined-index-name), the company's backend has run successfully on my local! Cheers!

Backend really takes another day to get it finished.

4) Error when importing MySQL database, solved by [this](https://stackoverflow.com/questions/20488311/error-1049-42000-unknown-database-localized-wordpress-database)

Notes: 
1) Next time when I run the backend on my local, I need to update the .env file as in the documentation.

2) front-end running by "ng serve"; back-end running by "php artisan serve --port==XXXX"

3) PHP7 does not naturally allow connection with database. One needs to enable mysqli extension, especially in the php.ini file, one needs to uncomment:

extension=pdo_mysql.so
extension=mysqli

Then it will connect with db successfully. Two helpful links here: [one](https://stackoverflow.com/questions/42909397/laravel-5-4-on-php-7-0-pdo-exception-could-not-find-driver-mysql), [the other](https://laracasts.com/discuss/channels/laravel/could-not-find-driver-error-in-laravel-55)

Today so much time spent on the connection of local backend application and the local MySQL database. 