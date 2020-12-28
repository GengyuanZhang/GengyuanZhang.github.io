---
layout: post
title: "Gengyuan's front-end progress!"
date: 2020-12-27
---

Gengyuan installed Node.js, npm as well as Angular CLI on his local. Then managed to deploy the company's website front-end on his local, [this page](https://stackoverflow.com/questions/60092642/ts1086-an-accessor-cannot-be-declared-in-ambient-context) of stackoverflow that helps! He noted it here, on his local, he needs to Setting "skipLibCheck": true in tsconfig.json solved his problem:

"compilerOptions": {
    "skipLibCheck": true
}

Deployment of Angular front-end -- success!

Right now, two parts to take care of when Gengyuan deploy front-end on his local next time: 1) Adding environment files 2) Setting "skipLibCheck": true in tsconfig.json.