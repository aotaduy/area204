---
title:  "Angular Runtime Environments"
date:   2020-05-11 11:30:05 -0300
tags: software bestPractices codeReview
categories: software angular typescript 
toc: true
---
We will present a way to handle environments in runtime vs in compile time that is the standard way to do it.
## The problem
You have multiple deploy environments each one having different configurations such as api baseurl 
## The Angular-CLI way
### Compile Time environment
Angular CLI provides a way to handle different environments built-in. 
You can set different options for your build, compiler flags, environments, file replacements, etc. 
This feature allows to define a configuration object that normally contains the base url for the api you need to call in your web app.
This is a very useful feature, but when the system gets larger and you need an environment for development, production, qa, and in most cases UAT, with this integrated ina Continous Integration / Contiunous delivery. 
You will need to execute something like this

### Example pipeline
The pipeline may look like something like this:

 ```console 
 git clone http://github.com/aotaduy/peticomputer.git
 cd peticomputer
 npm install
 ng lint
 ng test --watch=false
 ng build --environment=dev
 publish dev
 ng build --environment=qa
 publish qa
 ng build --environment=uat
 publish uat
 ng build --environment=production
 publish production
 cd ..
 rm -Rf peticomputer
 ```

This will resolve the environments in compile time and will produce four artifacts that will need to be deployed en every environment.
This solution can be a bit cumbersome, for the example above we will need to create 4 different builds that will take at least 2 or 3 minutes each one, addint to the npm install time, and maybe running the tests, in most of the pipelnes we have an average of 16 minutes of total pipeline time.
This dont look much but in a hotfix scenario when you need to ship to, test in uat and then deploy as fast as posible to production. The numbers add up and can become a problem. 

