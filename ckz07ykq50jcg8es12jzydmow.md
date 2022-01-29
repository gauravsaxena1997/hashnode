## Setting up  an Angular App with Angular CLI

# Setting up the environment

## IDE
For coding, you must have an IDE installed on your system. I’m using Visual Studio Code for this series but you can use your favorite one. If you don't have an IDE installed you can install VS Code from  [here](https://code.visualstudio.com/download).

## Node
A question can put up on your mind that we are learning and building Angular project here. Why we need Node for that. Well, Node does the magic behind the curtains. Angular doesn’t need Node directly but it is useful when we are developing an application.


%[https://media.giphy.com/media/l0He7dUSIKllrGtr2/giphy.gif]


Some points are given below.

#### 1. npm
When we are installing Node, npm comes by default, which is used to install and manage our dependencies in Angular projects. For instance, to even start our project we need npm because Angular CLI is installed with the help of npm itself.

#### 2. Transpiler
As we know, Angular uses Typescript by default, and Typescript is not understood by browsers. Browsers only know the language of Javascript. So to transpile our code from Typescript to Javascript, we need NodeJs.

#### 3. Web Server
Node provides a lightweight web server by which we can easily run our code and see the result on the browser.

Now we know why we need NodeJS, so you can install it by clicking [here](https://nodejs.org/en/download/).

Please install the latest LTS (Long Term Support) version available on the site.
You check both Node and npm install or not by the below commands.
```
node -v
``` 
```
npm -v
``` 
# Let’s create the App

## Angular CLI
Angular CLI is the command-line interface of Angular. We can create, build, deploy and manage our code by command line. Installing it is very easy. As we already have npm installed just hit the following command to install Angular CLI globally.

```
npm install -g @angular/cli
```
Flag `-g` is used to install an npm package globally so you can use it anywhere throughout your system. And `@angular/cli` is the name of the npm package we want to install.
After installing Angular CLI, we should now be able to use the `ng` commands provided by it which we are going to use a lot. But for now, let’s use it to know the current version of Angular CLI installed. 

```
ng version
``` 
It will give you the details of Angular, Node and npm versions installed. Again please make sure you have the latest stable version installed for compatibility and in the future, we don’t get any warning and errors that some package is not supported with the Node version, etc.
You can see more details around angular CLI [here](https://angular.io/cli).

## Create a new Angular Application
All you need to create a fully-loaded Angular project is a cool app name. So let’s create our Angular application by hitting our second `ng` command.
```
ng new survenalysis
``` 
It will ask you a few questions.

- Would you like to add Angular routing? Yes
- Which stylesheet format would you like to use? SCSS

Well, It is the name that pops into my mind. If you have a better name suggestion, comment it down.

And our basic skeleton of Angular Application is ready. Just make sure while creating the app, you don’t have any warnings or errors. We need a good start. If you are getting any please check the Node and Angular versions again.
Let’s quickly see whether it is successfully created or not. So move to the project directory we just created and hit the following command. 

```
cd project-manager
ng serve
```
It will compile and run the application on port 4200 by default. After you see Compiled successfully hop on a browser and open localhost:4200 and there is our app running.
Angular also provide a shorthand for almost every `ng` command for lazy developers like me 😌, for this one, we can also use the below command.

```
ng s
``` 
We can use `ng s -- open` or `ng s -o` which also opens the app in a browser for you.
One more important option of `ng serve` is **port**. It is useful if any other application is already running on port 4200.

```
ng s --port 8080
``` 
Unfortunately, no shorthand for this one  😅. You can read more about `ng serve` [here](https://angular.io/cli/serve).


## Angular file structure

Let's open the project inside our IDE.

```
code .
``` 
You will notice there are many files and folders. One most important thing to understand, what are these files for and what are the uses for each file. The structure is available on Angular official DOCs. It is a simple one-two-line description that I find unnecessary to mention here. You should it first before hands-on.
 - [Project file structure](https://angular.io/guide/file-structure) 
 - [Angular workspace configuration](https://angular.io/guide/workspace-config)

Once you read it and after that, you look in your created app and have confidence that you know the functionality of each file and folder, you are good to go and can move to the next one.

***
Previous Blog [What the heck is Angular?](https://gauravsaxena.hashnode.dev/what-is-angular)

Next blog [Building blocks of Angular (Angular Concepts)](https://gauravsaxena.hashnode.dev/building-blocks-of-angular)




 