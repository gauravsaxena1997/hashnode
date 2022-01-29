## All you need to know about Angular Modules

## What is an Angular Module?

Angular Modules can be seen as the broad features of our application. Like in any application authentication is a major feature, so in Angular, we can make a separate module for that and others like the Payment module, etc.

So, we can say that it is a logical grouping of Angular features that are related somehow. And what are these features? These are features or building blocks of Angular we already discussed which are components, directives, pipes, and services.

 It allows us to split up our application functionality into separate logical parts, where each part has its own internal details or functionality. Everything in your app is ultimately structured around modules.

### How Modules can be loaded in the Application

#### 1. Eagerly loaded modules

These are the modules that are loaded immediately when the application is loaded. It is the default behavior of all modules.

#### 2. Lazy loaded modules

The second way is we load our modules lazily, which basically means they get loaded when a particular route gets hit. Like we have a Payment module but we know that it is possible that users might not reach this point and only browse some stuff on your app. So, what is the need to load it right away when our app loads? It also boosts our app performance. We will learn about this more later on.

## Types of Angular Modules

#### 1. Root Module

When looking at the Angular module system, all things must begin with the root app module. The root app module is a necessary and mandatory part of every Angular app. By default, this module is named *AppModule*. it is possible to rename this module if we want.
The *AppModule* is the entry point to an Angular app. To understand this, we can think of it like this way: In other languages, we have the main function where the code execution starts like C/C++, Rust, etc. In Angular, we can compare it with *AppModule*.
So it is the entry point and the top-level container of any app's functionality and view layer.
Here we declare Angular components, directives, or pipes that we want globally available across our whole app.

#### 2. Feature Module

As the name goes, it is used to encapsulate a specific feature at a logic level. The main purpose is to organize our application code. We can code the entire app in the Root module (AppModule) itself, but that won't be a good idea because it will make the 
code unreadable, and also loading of the app gets very slow. A good example of a feature module can be a Dashboard module. The advantage of making a separate Feature module are:

- Code readability and reachability: We will have separate codes of each module differently so we will locate our code faster and it will not get messy.
- Lazy loading: We can lazy load a feature module will we know it increase our app performance.

#### 3. Routing Module

It is used to navigate our app according to user actions. You remember, when we create our app, Angular CLI asked a question whether we need to add angular routing or not, and we said yes. As a result of this, now we have a file in our app *app-routing.module.ts*. We can add all Routing paths to this file. Or as best practice, we can make separate Routing modules corresponding to each Feature module. It is the place where we utilize the concept of lazy loading which we learn in upcoming blogs.

#### 4. Service Module

It is the module that ideally consists of services that can be used for data access or messaging etc. Every app is incomplete without data. We need to show the data to the end-user. In order to do that, our components need to access the data. We can write data access code in each Component, but this is very inefficient and breaks the rule of single responsibility. For Components, the responsibility is to present the data to the user not to handle how and where we need the data. This is why service modules are needed.
The services are those which will provide the data to every component or we can say pass/share the data within multiple components. Hence,  The root AppModule is the only module that should import service modules. Because remember what we import in the Root module will be available globally. The *HttpClientModule* (Inbuilt Angular module that provides the functionality to send the HTTP requests to the Back-end server) and Singleton Services (We will discuss a lot about this later) are good examples of this.

#### 5. Shared Module

What we learn above is that a module consists of some components, directives, pipes, services, and other modules. In our app, we have some of these which need to be used in multiple places. All that should be imported here, so we will just import this shared module at multiple other places. We should avoid using/importing services here. since these should've been imported into Service modules. We need to also make sure to have only one Shared Module in the whole application. There is no reason to make multiple shared modules in one app. 
Some good examples are like *FormsModule* (which provides some forms feature we will discuss), it can be used in multiple modules so instead of importing it in every module we need, we can import in a shared module and import that shared module directly. Or some components we know that are used in different places like layout/grid component, a calendar component, etc.

#### 6. Widget Module

The third-party UI component libraries are widget modules. Like Angular Material which we integrate with our next blog. A widget module should consist entirely of declarations that mean no services only some modules or components etc.

The main takeaway is, all of these are just concepts that provide a better vision towards creating an app. Again, we can (but shouldn't) write the whole code inside the Root module itself without any logical problem and all the types we discussed not have anything special like we don't have to use different commands to create these and basic structure is also the same. We just need to keep these in mind while creating our project structure, so we could make a scalable, high-performing, bug-free, and clean application.

Well! That's enough about theory and now let's check...


## How does an Angular Module look like?

To define a Module in Angular, we have to use the **NgModule** decorator. And, I think I don't have to tell you what a decorator is. By checking the code, we would know is a class decorator since it applied to a class. Let's check the one and only module we currently have in our application which is our Root module Angular creates for us. Please open the *app. module.ts* file which looks like this.
```
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
```
We need to pass an object that has the following array type properties in the object. 

1. **declarations**: In this array, we specify which components, directives, and pipes belong to this module. We have *AppComponent* in this array since it is a component.
2. **imports**: In this array, we have to import the modules which are exported by other modules and which this module component is needed. In our root module, we have *BrowserModule* and *AppRoutingModule* because both are modules.
3. **providers**: In this array, we specify all the services that can be used across the app in any component, directive, or pipe. Initially, we don't have any services that's why this array is empty.
4. **bootstrap**: In this array, we specify the component that should be loaded at the start of the app. Or we can say it is where we define the root component of our module. Even though this property is also an array, in general, we will define only one component. By default *AppComponent* is the one that loads first. Don't worry it will also discuss the whole **Bootstrapping process of Angular** shortly.
5. **exports**: There is one more, which is not available at our Root module but we will use it in the future.  In this, we define the modules that should be visible and usable in the component templates of other *NgModules*. This means the modules we will know that are used in other modules.

Let's look at the import statements in the Root module

```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
```

All the basic stuff like decorators like *NgModule* comes from the `@angular/core` library. All the built-in Angular libraries start with `@angular/`. 
Then we have *BrowserModule*. It provides services that are essential to launch and run a browser app. So basically responsible for rendering stuff on the browser.
After that, we have a Routing Module that Angular created *AppRoutingModule* and the root component *AppComponent*.

An easy way to identify a root module is by looking at the imports property of its *NgModule* decorator. If the module is importing the *BrowserModule* then it's a root module, if instead is importing the *CommonModule* then it is a feature module.
*BrowserModule* and *CommonModule* is almost the same, the only difference is *BrowserModule* has some rendering still too.


If you read all the properties of the *NgModule* decorator carefully. You will find that:
- In a service module, ideally, it should have the content in the providers array only since here all the services reside and the declaration array should be empty.
- In a Widget module, most of the modules are exported so we can use them anywhere else.
- Any feature module will have the first three arrays (declarations, imports, providers) but not the fourth array (bootstrap).
- In a small app, the root module or app-level module is enough to organize different components, directives, pipes, and services. But as the app grows, you should refactor the root module into feature modules, which represent related functionality.
- In an application, we only have one root module and zero or many feature modules.

## Why are Angular modules needed?

One major task of Angular is to parse the template (HTML code) but here we will have some problems. In the whole application, we will have multiple components, directives, pipes, and services. How does Angular know which components, directives, and pipes should it be looking for while parsing the HTML? That is when Angular modules come in, they provide that exact information in a single place which is none other than the module. So, we can say that An Angular module encapsulates these artifacts as one compilation unit.

## Don't get confused with Javascript Modules

Angular modules and Javascript modules are different!

JS modules (also known as “ES modules” or “ECMAScript modules”) are a major new feature, or rather a collection of new features in Javascript. In JS, A module is just a file. One script is one module. As simple as that. And, with the help of JS modules functionality, we can easily import or export a module by the same keywords as well.

On the other hand, the Angular module as we discussed above provides a compilation context to Angular. So, both are different concepts but we use JS module functionality in our Angular app to import and export built-in and custom-created modules.

That's enough of this tutorial. In the next one, we will create our first module and integrate Angular Material into our app.

***
Previous Blog [Wrap it up with Decorators](https://gauravsaxena.hashnode.dev/what-are-decorators)

Next blog [Integrating Angular Material as a Module](https://gauravsaxena.hashnode.dev/integrating-angular-material)





