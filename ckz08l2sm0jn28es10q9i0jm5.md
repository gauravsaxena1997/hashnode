## Wrap it up with Decorators 🎉

No! We're not wrapping up the series. We don't even start it yet properly.  

Before taking a deep dive into the Angular concepts, we learned in the [previous blog](). I want to discuss a really important topic first. As you guessed from the title, we're going to discuss Decorators. Angular without decorators is something like an Atom that exists without a nucleus.

If you are aware of Typescript features, you would have known that Decorators are a Typescript feature, not an Angular one. In the last blog, we discussed Modules, Components, etc. Let's open the project we set up previously and open the `app.module.ts` file. You can see a syntax with the **@** symbol which is `@NgModule`. Now open the `app.component.ts` file and there also you can see syntax similar to that `@Component`. Actually all the concepts we discussed there Services, Directives, Pipes have the same thing. So...

## What exactly is a Decorator?

The basic use of Decorator is to provide meta-data about something to the application or program. And meta-data is some information that tells an application app about some behavior and how the functionality should work. It is one of the coolest  😎 features of Typescript. All the Angular concepts we see, are nothing but just a class. Yes, in Angular all the things (Modules, Components, Pipes, etc) are defined by a class and Decorator is the key that tells Angular what is what by providing some meta-data about the class.

Decorators are a programming pattern where we warp *something* to change its behavior if I say it in more simple words. And the *something* refers to methods, classes, parameters, accessors (getters and setters) etc.

Let's simplify it a bit more. Decorators are nothing but functions, Yes! To add a decorator somewhere, we need to add the **"@"** symbol with the decorator we use.

Don't worry if sounds a little complex, we're going to create our own decorators here in this blog. One more thing you should know, it is a *stage two proposal* in Javascript. That means it is an experimental feature of JS and we can not directly run it on browsers. We need to enable some checks and transpile it first.

## Let's create some decorators

As we know that decorators are a typescript feature, we do not need Angular application necessarily. But as I mentioned earlier we need to enable some typescript features via config and needs a transpiler, Angular app does that for us because Angular already using Decorators. We're gonna use our Angular App which we created.

First thing first. Let's see the config which I mentioned in order to enable Decorators. Please open the `tsconfig.json` file which keeps the TypeScript compiler configuration of our app. In this, you will find the property `experimentalDecorators` which is already set to *true*.

```
    "experimentalDecorators": true
``` 

Let's move forward and open the `app.component.ts` file. Forget all which is written there and use it for our experiment to create Decorators. We are going to learn about **Components** real soon.

Decorators can be of different types according to what we are decorating with them. Let's discuss it one by one.

## Types of Decorators

### 1. Method Decorator

A *Method Decorator* is declared just before a method declaration. And it is used to observe, modify or replace a method definition. First, go to the *app.component.html* file, select all content there and remove it. Then add some code in the *app.component.ts* file at the *AppComponent* class available. 


```
export class AppComponent {
    constructor() {
        console.log('I\'m inside the constructor');
        this.getHypotenuse(5, 6);
    }

    getHypotenuse(perpendicular: number, base: number): number {
        console.log('Inside getHypotenuse method');
        const hypotenuse = Math.sqrt(Math.pow(perpendicular, 2) + Math.pow(base, 2));
        return hypotenuse;
    }
}
``` 

Here is a simple class with a method/function to calculate Hypotenuse. It takes two parameters Perpendicular and Base then applies a formula we all know as Pythagoras theorem and returns the calculated Hypotenuse. Also in the *constructor*, we call this method with two paraments. Nothing fancy!

Let's run it first with the command we know to start the app `ng s -o` and see the output in the developer tools of the browser. If you're using Google Chrome, then hit `Ctrl+Shift+i` or right-click anywhere and select Inspect. Then move to the **Console** tab. You can see these messages right away.

```
I'm inside the constructor
Inside getHypotenuse method
```
As we expected the log inside *constructor* is printed first and then our method's log gets printed because we call it in the *constructor*.

Now, let's define our first Decorator in the file. You can add it anywhere outside the class like below import statements.

```
const Log = function (
    target: Object,
    propertyKey: string,
    descriptor: PropertyDescriptor
) {
  console.log(
    'Inside Log decorator\n',
    'target is:', target, '\n', 
    'propertyKey is:', propertyKey, '\n', 
    'descriptor is:', descriptor
    );
}
```

Simple, isn't it? It's just a function that takes three arguments in the case of Method Decorator. Now let's decorate our `getHypotenuse` method with it. So we only need to add `@Log` just before the method like this.

```
  @Log
  getHypotenuse(perpendicular: number, base: number): number {
    console.log('Inside getHypotenuse method');
    const hypotenuse = Math.sqrt(Math.pow(perpendicular, 2) + Math.pow(base, 2));
    return hypotenuse;
  }
```
Let's see what we get in the browser console.

```
Inside Log decorator
target is: {
        constructor: ƒ, getHypotenuse: ƒ}
        constructor: class DemoClass
        getHypotenuse: ƒ getHypotenuse(perpendicular, base)
    }
propertyKey is: getHypotenuse 
descriptor is: {
        writable: true,
        enumerable: false,
        configurable: true,
        value: ƒ
    }
I'm inside the constructor
Inside getHypotenuse method
``` 

So, our decorator runs first. That's because the decorator is called on runtime after we add it somewhere. 
Let's discuss the arguments of Method Decorator:
- **target**: Contain either the constructor function of the class for a static member or the prototype of the class for an instance member.  We can see the **prototype** of our class i.e. the *constructor* and the method we write in it, that is `getHypotenuse`.
- **propertyKey**: Contains the name of the member where we apply the decorator. In our case, we get *getHypotenuse*.
- **descriptor**: The Property Descriptor is the member by which we can modify or replace the current behavior of the method. It has four properties as we can see in the console writable, enumerable, configurable, and value. If you further open *value* property, you will see it is nothing but our method. That's just what we want to modify our method.

Currently, the decorator is of no use. Let's update it so it can give us some info about the method.


```
const Log = function (
    target: Object,
    propertyKey: string,
    descriptor: PropertyDescriptor
) {
  const originalValue = descriptor.value;
  descriptor.value = function (...args: Array<any>) {
    console.log('The arguments passed in the method are', args);
    const result = originalValue.apply(this, args);
    console.log('Result from the decorator is', result);
  }
  return descriptor;
}
``` 

Let's discuss the code line by line:

1. Firstly, we assign  *descriptor.value* which has our method itself in a variable *originalValue* so we can use it further. After that, we are assigning our new function in that. It the function parameter, we give the *args* variable with the help of the **[spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)** which has our function arguments in an array.
2. Inside our new function, we printed the arguments of the function.
3. Then we call our method which we assign previously in *originalValue*. We use **[apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)** method to bind the arguments with the context. So, it will bind and call the method immediately. We assigned the result in the *result* variable.
4. Now we just print out the *result*.
5. At last, we *return* the *descriptor* we write ourselves.

In short, we just modify the behavior of the *getHypotenuse* method. That is the result you will see in the browser console if you added the code properly.

```
I'm inside the constructor
The arguments passed in the method are (2) [5, 6]
Inside getHypotenuse method
Result from the decorator is 7.810249675906654
``` 
After adding the decorator, now we can see additional info about the method. We can have more than one Decorator for a single method.

Let's do something more interesting this time. The `getHypotenuse` method is a standard function that should never change. Let's mess it around to change the functionality of the method by instantiating an **object** of the class and re-write the method again. Add this code after our *AppComponent* class ends.

```
const demoObject = new AppComponent();
demoObject.getHypotenuse = (perpendicular: number, base: number) => {
  const someWrongResult = perpendicular * base;
  console.log(`Re-write getHypotenuse function which give wrong result ${someWrongResult}`);
  return someWrongResult;
};
demoObject.getHypotenuse(4, 5);
``` 
Pretty simple code. We just create a new object by the *AppComponent* class. Re-write the *getHypotenuse* to give some wrong results and call the function from the newly created object with some parameters. lets' run the code.

```
Re-write getHypotenuse function which gives wrong result 20
```

Among the logs, we can see we are able to overwrite the current method. So let's make the method read-only with the help of a simple Decorator. Let's add this just after our previous decorator.

```
const Readonly = function(
    target: Object, 
    name: string,
    descriptor: PropertyDescriptor
) {
  descriptor.writable = false;
  return descriptor;
}
``` 
For this one, we are just updating the **writable** property to *false* which exists on the Property descriptor, and then returning the modified descriptor. Also, let's decorate the method with this one too.

```
@Readonly
@Log
getHypotenuse(perpendicular: number, base: number): number {
    console.log('Inside getHypotenuse method');
    const hypotenuse = Math.sqrt(Math.pow(perpendicular, 2) + Math.pow(base, 2));
    return hypotenuse;
}
``` 

This time, it will return a Type error instead that we can not assign anything to a read-only property. So, this worked too  😌.

### 2. Class Decorator

As you thought, A Class Decorator is declared just before a class declaration. The class decorator is applied to the constructor of the class and can be used to observe, modify, or replace a class definition. If the class decorator returns a value, it will replace the class declaration with the provided constructor function.

And as the TS official documentation says:
> The expression for the class decorator will be called as a function at runtime, with the constructor of the decorated class as its only argument. If the class decorator returns a value, it will replace the class declaration with the provided constructor function.

We can see our *AppComponent* is already decorated with **@Component** Class Decorator. But we also know now, that we can use more than one Decorator. Comment out or remove the previous code we have to write to see a clear picture here, so it will go to starting state. I will attach the full file below for reference if you need it.

Let's start with a simple declaration for the class decorator.


```
const MyComponent = function(arg: any) {
  console.log('Inside the class decorator:', arg);
}
``` 
And don't forget to add the decorator just before *AppComponent* class like `@MyComponent `. And you can see that it will print out the class. Let's try to mimic the *@Component* Decorator and try to understand how we can pass an object similar to that. That's how it should look like where you add your decorator above the class.


```
@MyComponent({
  id: 'something',
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
``` 

Previously, we didn't pass anything so the decorator tasks class itself as an argument. But this time we passed an object. So, let's update our Class Decorator so that, it can handle it.

```
const MyComponent = function(options: any) {
  console.log('The options passed are:', options);
  return (target: any) => {
    console.log('The initial target is:', target);
    target.id = options.id;
    target.selector = options.selector;
    target.templateUrl = options.templateUrl;
    target.styleUrls = options.styleUrls;
  };
}
``` 
 
In the browser console, you can see that in *options*, there is the object we passed in and in *target* we have the class declaration. As we learn above, if we return something from the class decorator, it will replace the class declaration with the provided constructor function. So what we're returning from the decorator is actually a constructor.

Let's verify whether it added the values for us in the class or not. But first, we need to add [static variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static) in the class so we can call them inside our class and add some logs in the *constructor* to verify that. Adjust your class code that has this new code.


```
export class AppComponent {
    static id: string;
    static selector: string;
    static templateUrl: string;
    static styleUrls: Array<string>;
    constructor() {
      console.log(
        'AppComponent id is' , AppComponent.id + '\n' +
        'AppComponent selector is', AppComponent.selector + '\n' +
        'AppComponent templateUrl is', AppComponent.templateUrl + '\n' +
        'AppComponent styleUrls is', AppComponent.styleUrls
        );
    }
}
``` 
We should see that in the console, it will print the values we passed through the Class Decorator. Now you got the basic idea, how Angular uses decorators to provide meta-data about the class and handle the behavior accordingly.

### 3. Property Decorators

I think no need to tell where we should apply them. Just like the method decorator, you’ll get the *target* and *propertyKey* parameters. The only difference is that you don’t get the property descriptor for this one. 


```
const PropertyDecorator = function(target: Object, propertyName: string) {
  console.log('Inside property decorator', 'target:', target, 'propertyName: ', propertyName);
}
``` 
Add the Property Decorator to a property in the class.


```
  @PropertyDecorator
  static someName: string
``` 

You will see the class prototype in *target* and the name of the property in *propertyName* inside the browser console.

### 4. Parameter Decorator

This decorator can be added to the parameters of a function. Parameter Decorator has three different arguments.


```
const ParamDecorator = function(target: Object, name: any, index: number) {
  console.log('In papamDecorator', 'target', target, 'name', name, 'index', index);
}
``` 

As the last argument, it has the index of the parameter where we apply the decorator. Let's add it in our old `getHypotenuse` method's parameter.


```
getHypotenuse(@ParamDecorator perpendicular: number, base: number): number {
    const hypotenuse = Math.sqrt(Math.pow(perpendicular, 2) + Math.pow(base, 2));
    return hypotenuse;
}
``` 
You can see the expected results in the browser.

There are other decorators as well but we're just limiting to the above as Angular uses only these four decorators. If you are curious to learn more. Take a shot at the Typescript Decorators [here](https://www.typescriptlang.org/docs/handbook/decorators.html).

Ahh! That was a long one. Doesn't it?


%[https://media.giphy.com/media/Tgn6WxWJzp89uVlkpR/giphy.gif]


But it was necessary for you to understand this. Now if you will saw decorators in Angular anywhere, you know what they are and how they will work.

***
Previous Blog [Building blocks of Angular](https://gauravsaxena.hashnode.dev/building-blocks-of-angular)

Next blog [All you need to know about Angular Modules](https://gauravsaxena.hashnode.dev/angular-modules)

 