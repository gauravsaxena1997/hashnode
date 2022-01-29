## Integrating Angular Material as a Module

Angular Material is a UI library component developed by Google in 2014. It is specially designed for Angular developers. It helps to design the application in a structured manner. Its components help to construct attractive, consistent, and functional web pages and web applications. It is used to create a responsive and faster website.

That's why we will use this to make our app looks good.

## Add Angular Material in our app

We just need to hit one command for that. So go to the terminal inside our project directory and execute this command. 

```
ng add @angular/material
```

It will ask some questions like:
- Choose a prebuilt theme name (Choose anyone, we will make a custom theme so it doesn't matter)
- Set up global Angular Material typography styles? (Yes)
- Set up browser animations for Angular Material? (Yes)

Typography is a way of arranging type to make the text more readable and appealing when displayed. Check [here](https://material.angular.io/guide/typography) for more. Browser animations are used to add the animation to your angular application.
The whole process looks like this.

```
ℹ Using package manager: npm
✔ Found compatible package version: @angular/material@13.1.2.
✔ Package information loaded.

The package @angular/material@13.1.2 will be installed and executed.
Would you like to proceed? Yes
✔ Package successfully installed.
? Choose a prebuilt theme name, or "custom" for a custom theme: Indigo/Pink        [ Preview: https://material.angular.io?theme=indigo-pink ]
? Set up global Angular Material typography styles? Yes
? Set up browser animations for Angular Material? Yes
UPDATE package.json (1134 bytes)
✔ Packages installed successfully.
UPDATE src/app/app.module.ts (502 bytes)
UPDATE angular.json (3359 bytes)
UPDATE src/index.html (572 bytes)
UPDATE src/styles.scss (181 bytes)

```

### So, what really changed after it?

Angular CLI installed it for us and added some things to our code. Let's check it.

#### 1. package.json

There are two new node modules added.
- [`@angular/cdk`](https://material.angular.io/cdk/categories) (The Component Dev Kit (CDK) is a set of behavior primitives for building UI components.)
- [`@angular/material`](https://material.angular.io/components/categories)


#### 2. angular.json

We know that it is our project configuration file. If you are using VS Code as your IDE, you have the Open changes feature for review changes done in the file. So, can check from there. Otherwise, search for *styles*. You will find an array. It is where all the stylesheets of our app are being added.
```
...
"styles": [
    "./node_modules/@angular/material/prebuilt-themes/indigo-pink.css", 
    "src/styles.scss"
],
...
```

Angular Material added a stylesheet which is an in-built theme available for us. There are many themes available. But in the installation, we choose this one.

#### 3. index.html

It added some link tags. Angular Material uses **Roboto** font.

```
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```
It also adds a class *mat-typography* to the *body* tag. These are pre-built classes of Angular Material, we don't need to declare it anywhere. 
```
<body class="mat-typography">
  <app-root></app-root>
</body>
```

#### 4. styles.scss

There are some styles added that will impact the overall look and feel of the app and use Roboto font for the whole body, which means whole angular app.

```
html, body { height: 100%; }
body { margin: 0; font-family: Roboto, "Helvetica Neue", sans-serif; }
```

#### 5. app.module.ts

It adds a new module that is *BrowserAnimationsModule*. As Angular DOC says:

> Animation provides the illusion of motion: HTML elements change styling over time. Well-designed animations can make your application more fun and straightforward to use, but they aren't just cosmetic. Animations can improve your application and user experience in a number of ways:
  - Without animations, web page transitions can seem abrupt and jarring.
  - Motion greatly enhances the user experience, so animations give users a chance to detect the application's response to their actions.
  - Good animations intuitively call the user's attention to where it is needed.

```
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
```
And as we know it should be available globally and a module is also added in the **imports** array.
```
imports: [
    ...,
    BrowserAnimationsModule
]
```

### Let's test, it works or not

Angular Material provides different modules for different components like buttons, input, sliders, etc. So, you should look at the Angular Material documentation. So let's try to add a slider. Open [this](https://material.angular.io/components/slider/overview) tab or go to Angular material component and search for Slider. Move to the *API* tab. There will be an API reference for the Angular Material slider. Copy that and paste it into our `app.module.ts` file for now since we only have this module available. Also, add it in the **imports** array.
```
import { MatSliderModule } from '@angular/material/slider';
```
Move to the *Overview* tab in DOC and copy the code of Basic Slider and paste it in `app.component.html`. If there is any content in this file remove all that file.

```
<mat-slider aria-label="unit(s)"></mat-slider>
```

You should have seen the slider on the browser screen. But what we did is efficient? WE import the Slider module in the `app.module.ts` file. In the future, we will use many more Angular Material components in our app. Say, we added twenty modules then we have to load twenty modules in this file and our `app.module.ts` file will get overloaded. As we discussed in our last blog, we should not write all the things in the Root module. So what? Well! we need to create a separate module for Angular Material, so all the modules related to it will be imported in that module only. In that way, our Root module looks cleaner. So, let's create our separate widget module for Angular Material.

### Create our first module

With Angular CLI, creating any Angular block is done with just one comment. To create a module, use the below command.

```
ng generate module material --flat
```
Or a shorthand 
```
ng g m material --flat
```
With option `--flat`, it will generate the new module without any folder. If we don't use this option, the module will be created under a new folder *material* which we don't need for this one. Let's open this file. So, nothing fancy here. It will look like the Root module.
```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  declarations: [],
  imports: [
    CommonModule
  ]
})
export class MaterialModule { }
```
Let's do some modifications to the file.
1. Remove `CommonModule` from import and *imports* array of the decorator.
2. Remove *declarations* property from `NgModule` decorator.
2. Go to `app.module.ts`, Since `BrowserAnimationsModule` and `MatSliderModule` belong to the Angular Material module remove that from the import statement and *imports* array and add the import statement and *imports* array in the `material.module.ts` file. So now the file should look like this.

```
import { NgModule } from '@angular/core';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatSliderModule } from '@angular/material/slider';

@NgModule({
  imports: [
    BrowserAnimationsModule,
    MatSliderModule
  ]
})
export class MaterialModule { }
```
Now, the catch is, we're making this Material module so all of our applications could use these and we know to achieve this we need to add this Material module into the Root module (`app.module.ts`). But one more thing is, in order to use these modules in other places we need to export these too, otherwise these are not accessible to other modules. 

Also, we learned in the previous blog that a widget module mostly export modules. So, what we're importing here, we need to export these too. And what do we need to use for that? Add the *exports* array in our `NgModule` decorator. But then there will be code duplication because both *imports* and *exports* array will have the same things.

So for that, let's make a new array where we have all the modules and we simply add this array in both  *imports* and *exports*. So, the updated code will look like this.
```
import { NgModule } from '@angular/core';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatSliderModule } from '@angular/material/slider';

const materialModules = [
    BrowserAnimationsModule,
    MatSliderModule
];

@NgModule({
  imports: [...materialModules],
  exports: [...materialModules]
})
export class MaterialModule { }
```

Simple isn't it! The thing remaining is to add this Material module in the Root module so it is accessible to the whole app. So, move back to the `app.module.ts` file and import this new module and add it in the *imports* array. Updated, the file should look like this.

```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { MaterialModule } from './material.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    MaterialModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

You shouldn't get any errors at this point and when you move towards the browser you should still see the slider we add in our HTML file.

One thing you should remember is that you should always keep Developer tools in the browser open to check we don't have any kind of errors.

In the next blog, we will create a custom Angular Material theme for our app.


***
Previous Blog [All you need to know about Angular Modules](https://gauravsaxena.hashnode.dev/angular-modules)

Next blog [Create a Custom Angular Material Theme](https://gauravsaxena.hashnode.dev/create-a-custom-angular-material-theme)
