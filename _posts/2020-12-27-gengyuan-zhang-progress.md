---
layout: post
title: "Gengyuan's progress!"
date: 2020-12-27
---

Gengyuan installed Node.js, npm as well as Angular on his local. Then managed to deploy the company's website front-end on his local, [this page](https://stackoverflow.com/questions/60092642/ts1086-an-accessor-cannot-be-declared-in-ambient-context) of stackoverflow that helps! He noted it here, on his local, he needs to Setting "skipLibCheck": true in tsconfig.json solved his problem:

"compilerOptions": {
    "skipLibCheck": true
}

Deployment of Angular front-end -- success!