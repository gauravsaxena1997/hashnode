## Building blocks of Angular (Angular Concepts)

Let's discuss the features or concepts by which an Angular application is built. Every application has some important features which we can further break into small functionalities.
Let's take a simple example first then we can understand the concepts from it. Consider a simple E-Commerce website. What are the basic features it could have?

- Authentication
  - Sign up
  - Sign in
  - Forget password 
  - Reset password

- Products
  - Product categories
  - Product list
  - Cart functionality

- Payment
  - Add/update a card
  - Payment page
  - Payment success/failure page

Same as this, we can bifurcate the other applications and we should have to do it first. But should it stop there?

No, a separate functionality will also have specific features. The basic functionalities will be the same on all the E-Commerce apps discussed above but everyone has some specific features which stand them out from others. 
Take a step forward and see what these other functionalities could be. We can say in the Cart functionality if the amount of the product is greater than 5000 we want to highlight it in the cart so its appearance is different from others. Or from the product list remove the products if they are out of stock and many others will be there depending on the requirements. Let's stop here and try to understand the Angular features from this example.

## 1. Components
Components are like the basic building block in an Angular application. It is dedicated to specific functionality in the application, In the above example, these are the components if we are talking in Angular language:
- Sign up Component
- Sign in Component
- Forget password Component
- Reset password Component
- Product categories Component
- Product list Component
- Cart functionality Component
- Add/update a card Component
- Payment page Component
- Payment success/failure page Component

As in a typical webpage to handle a webpage we need HTML, CSS, and JS, Angular components are no different. Angular components have an **HTML Template** which handles the view, a **Class** basically a Typescript file which handles the logical part and **Styles** as you imaged a CSS/SCSS file which handles the styling.

## 2. Directives
Directives are nothing but the feature which uses to transform a [DOM](https://www.w3schools.com/whatis/whatis_htmldom.asp) element. Basically tells Angular to change some styling or some behavior of a DOM element.
In our example, we talked about in the cart functionality if the price is greater than 5000, we change some styling of it. It is exactly what a Directive does. We apply the directive in the Template and specify a condition according to that the DOM will automatically update.

Also, in the application, we need to iterate some data like product list or show some message conditionally like *No products in this category*. So in this case, we are also manipulating the DOM. So the syntax we need to *loop through* data of apply *if* conditions are also called as Directives. 

## 3. Pipes
While Directive changes the behavior of the DOM element, Pipes are used to transform the data or values. In our scenario, removing out-of-stock items is achieved by the Pipes. To display the product list we have some kind of list which we iterate (loop through) in the template to show all the products. So we simply apply our custom pipes which check some conditions like count equals to zero, removing them from the list, and after transforming the data return the updated product list.

## 4. Services
Service is used to specify any value, function, or feature which can be used by different elements of the application.
The basic example is user information, When we sign in, we need user info to show on almost every feature. So we can save the user info here and inject (use/import) it wherever we want. Or in any web application, we need to call APIs by some HTTP methods (GET, POST, PUT, etc). So we can make a separate service for these HTTP requests and inject it. 

## 5. Modules
The modules provide a functional grouping of the features which belong to specific functionality. What will it group exactly?

%[https://media.giphy.com/media/3o7TKTDn976rzVgky4/giphy.gif]

Well, what we discussed so far. A module is the combination or grouping of Components, Directives, Pipes, and Services which belong to a specific feature in the application. In the example we discussed above, we can have three modules in the app:
- Authentication Module
- Products Module
- Payment Module

***

Previous Blog [Setting up  an Angular App with Angular CLI](https://gauravsaxena.hashnode.dev/setting-up-an-angular-app-with-angular-cli)

Next blog [Wrap it up with Decorators](https://gauravsaxena.hashnode.dev/what-are-decorators)



