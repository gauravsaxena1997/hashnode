## What the heck is Angular?

Angular is an open-source front-end framework of javascript mainly proposed to build Single page applications. As a framework, it also provides a  development platform to work with and scalability to manage huge applications.

Angular is written in TypeScript language and maintained by Google.

If you are a beginner, after reading this some questions can pop up in your mind.

- ### What exactly is a front-end framework?
Front-end is basically all about the parts of a website that users see. On the other hand, the back-end is about handling the application functionalities behind the curtains.
Also, we can say, it is the presentation layer of your application. So it can include interactive user interfaces, managing application data on the client-side, handling the data received by the back-end, and updating it in the back-end through APIs.
So a Front-end framework has the responsibility to manage these mentioned things efficiently and in a simple structured manner.



- ### How is a single-page application(SPA) different from the traditional one?
When we talk about the traditional websites, it will load a new page when you click a link and go a different route.
A single-page application doesn’t need to reload the page during its use and works within the browser. So when you load a SPA, all the data  (JavaScript, HTML, and CSS) is loaded with a single page. In the case of Angular, you will find an` index.html` in your project which is loaded on the browser. All of the apps you use every day, whether GitHub, Gmail, or Google Drive, use SPA. 
This is also important at times when the user has poor connectivity. Furthermore, the route between pages is performed without reloading the entire page. So you will never see the loading action of the browser if it is a SPA.
So yes,  a SPA literally has only one page.


- ### Development platform means only writing the code or logic for our project?
If you are thinking that it just provides you with an easy way of coding, that’s not it. In the current scenario only writing code is not enough. If you are working on a project you firstly need a server to run your code, if you are using modern Javascript or typescript you need a transpiler to convert all the code in plain JS which the browser supports, after you complete code you need to test your app with all the test case that can be possible and finally the code should be ready for the deployment. If you previously worked on an application without a framework you know how painful it is to manage. But, yes guessed right. With Angular no need to be concerned about these. Just focus on the logic to build the application. Angular will take care of the rest.


- ### Does scalability matter?
If you are thinking about any project, there will not be a huge amount of functionalities initially, but as the project grows, you must have to add new features to your application. So you have to consider the possibility of adding new features, updating existing ones, and removing some functionalities. So as a smart developers we have to manage our code in a manner that in the future we don’t have to re-write and update previous code much. So yes, In Angular you can scale up an application easily.

Now I can assume you got the idea of what Angular really is but it leaves us another question, why Angular comes in the first place. What are the previous holes so Angular is created to fill them?
For this, let's rewind the tape a bit.

What we need to make a web application is HTML for UI, CSS for styling, and Javascript for dynamic behavior for the application. As the complexity of web applications grows more, we have to add different types of event handlers like click, etc, and more DOM manipulation. And as different users use different browsers some handlers might work on one browser but not on the other. 

So to resolve those problems jQuery came to the rescue which was the most popular and usable library back in the days and still is. The point worth mentioning here is it is a library, not a framework. So it is just a tool to make implementing what you want easier. So we can do the same thing as javascript but more shortly and cleanly. Also, it adds up really handy new features. Some of the examples are Plugins, Animation, AJAX support, Cross-browser compatibility, etc.
So manipulating DOM is now a lot easier than writing plain JS. 

But still, maintainability is very hard if we are dealing with a large project, and also we need to test our application too before sharing it with the world.

Now AngularJS comes into the picture. It comes with a Model View Controller approach which is really good in structuring our project better. It also provides testing out Applications like Unit testing. In addition, Routing is a lot easier than ever. So, what now. We got everything we need to develop an app?


%[https://media.giphy.com/media/26tOXgoz0WNQhwb04/giphy.gif]


Our requirements never get over, does it?

Still, if we have a really big project, the structure is complex and as we surf the internet most of the time with Mobile and Tablets we need to have support for Mobile browsers too which AngularJS doesn’t provide.

So finally we are here. Angular! 
It is a complete rewrite of AngularJS, where AngularJS uses Javascript, Angular is written and uses Typescript as the default language which at the end of the day transpiled to Javascript because browsers only know the language of Javascript. Angular also introduced an Object-oriented programming paradigm in coding.
It adds a new feature Angular CLI which really helps to create an Angular project and scale it up. We can simply create an Angular feature like Modules, Components, Services with just a few commands.
Speed is another difference between Angular and AngularJS. Angular introduced many new features like two-way bindings etc to make the rendering ever faster.

If you are wondering if Angular and AngularJS are the same, the answer is no. Angular is a superset of AngularJS. The implementation is different in both of them. AngularJS is the first version of Angular. After that Angular 2 and 2+ are known as just Angular. If anyone is talking about Angular that means version 2/2+. You don’t need any knowledge of AngularJS if you want to learn Angular. 

## Prerequisites for Angular
As you expected, since Angular is a Front-end language, you should have the basic knowledge of:

- HTML
- CSS
- Javascript
- Typescript

***

Previous blog [Introduction: Learning Angular from scratch](https://gauravsaxena.hashnode.dev/introduction-angular-from-scratch)

Next blog [Setting up  an Angular App with Angular CLI](https://gauravsaxena.hashnode.dev/setting-up-an-angular-app-with-angular-cli)

* * *

### Playlist for this Angular blog series
Check out the whole playlist by clicking the below link for more details, updates, or jump to a specific blog.

[Learning Angular from scratch](https://gauravsaxena.hashnode.dev/series/angular-from-scratch).




