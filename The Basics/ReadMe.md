Angular Basics
-

### Introduction

So now we get started with discourse and with angular and our project we're going to use and ofcourse  it's time to dive deeper into angular to understand what really does?  

* what happens behind the scenes? 
* How an angular gets  started in the first place and which base building blocks it offers us? 
* How we can build angular apps and which features we may use for this.
 
By the end of this section you will understand how can build your basic angular application? What it then does and what you need to change to reach a different result.	So with this let's dive into it and let's start by having a look what actually happens when we with

### How an Angular App gets Loaded and Started

Angular is a framework which allows you to create reactive single page application.This is the single page which has served the *index.html* file.
The body of the file contains app root thing with a Loading... in between. Now clearly we don't see it Loading... here. All the files in the app folder which have component in their name. So these files are related to this component.
#### app.component.ts
Here you can see that we have to at component decorator does seems to be important but more importantly right now you'll see that there we have this **selector** is a property which assigns a string as a value and does string holds *app-root* it is clearly says the same text as in our *index.html* file

Angular able to needed to replace the file in the app folder in this html file with the template off this component and the component having this selector and the template of this component simply is the content here in this *app.component.html* file.

Now i will dive deeper into how to create components and how to configure them this is what basically happens at the startup, through the missing information is how is angular triggered.How is it kicked off to actually run over our body here these index.html file.

The answer is in the final index.html file getting served in the browser and we can verify this by inspecting the source code here we got a couple of script imports at the end.

```
<body>
<app-root></app-root>
<script type="text/javascript" src="inline.bundle.js">
</script><script type="text/javascript" src="polyfills.bundle.js"></script>
<script type="text/javascript" src="styles.bundle.js"></script>
<script type="text/javascript" src="vendor.bundle.js"></script>
<script type="text/javascript" src="main.bundle.js"></script>
</body>
```

These are injected by CLI automatically so that is why we don't see it here in the raw index.html file here we don't import these scripts but whenever it is **ng** **serve** process rebuilt our project. It will create bundles and javascript  script bundles and automatically add derived imports in the index.html and a little convenience functionality for us. 

So in the final file these scripts imports are present and these script imports will contain our own code too, So these script files are executed and they're actually the first code to be executed.And that is just something you have to keep in mind is too code we write in our **main.ts** file. That is why we call it as main. This is the first code which gets executed. Let's have a closer look at it then. 

Here you will see that we get a couple of imports then we check if we are in production mode or not. You basically turn off some warning messages i can tell you that. But most importantly here

```
platformBrowserDynamic().bootstrapModule(AppModule);

```
now bootstrap start our angular application by passing **AppModule** to this method and AppModule refers to the file **app.module.ts**

Now if we have a look at this file here we actually see that somehow we kind of like to Component to strange at thing here is NgModule. But most important we get the bootstrap array which basically lists all the components which should be known to Angular at the point of time it analyzes our index.html. Here we reference our app component. So angular gets started this main.ts file, there we bootstrap an angular application and we pass this module as an argument. In this module we tell angular there is app component which you know when you try to start yourself and angular now analyze this app.component.ts read the setup we pass here, and therefore is selector is app-root. And now Angular is able to handle app-root in the index.file and it knows all right this is the selector i know you told me that because it was listed in the bootstrap array in the app module this component.So now i know that in the index.html i should insert the app component and the app.component happens to have some html code, a template attached to it which is this <h3>I'm in the AppComponent!</h3> and this is the angular application starts.

```
 bootstrap: [AppComponent]
```

### Components

components are key feature in angular. You build your whole application by composing it from a couple of components which you create on your own. Now we do start with this app component, the root component you should say which holds our entire application basically in the end. So this root component is the app component will be the component where we nest or add our other components too. So to this template does index.html file off the app.component.
Each component has its own template it own html code maybe its own styling and more importantly also its own business logic and this is the great benefit. It allows us to split up your complex application your complex web page into reusable parts. You may use a component more that once and that allows you to easily replicate that business logic replicate that styling or in general make a finally controlled piece in your application without having to crunch eveything into one single script file, one single html file. Instead, it's very easy to update very easy to exchange and again re-usable.

### Creating a New Component

Let's say we want to ouput some information about a server. We're building a back end for our server management application and we want to output some server information.I will store a new folder which is a subfolder of the **app** because generally a angular CLI project all your app roll that will go into the app folder.I will name it **server** because it will hold my server component.

```
app
  server
    server.component.ts
```
So now we get an empty file for our new component. Now first of all a component simly is just a class that hides class so that angular able to instantiated it to create object based on the blueprint.

```
export class ServerComponent{

}
```
Naming convension we should follow (ServerComponent). This is normal typescript class nothing special about it. We should add something to it which tells angular this is not only a normal typescript class but instead something special component. We do this by adding a special **decorator**.
Decorators are a typescript feature which allow you to enhance your classes. Decorators are always attached by adding @ sing in-front of them.

```
@Component()
export class ServerComponent{

}
```
This component decorator not something typescript knows from the start, so we have to import it. We have to import

```
import { Component } from '@angular/core';
```
Angular ships with a couple of packages where basically groups it;s functionalities and the core package as the name implies give us access to some of the core functionalities of angular. with that we import that component. Now we need to pass javascript object component decorator to configure it because without any configuration it is stil not that valuable to angular. The important information piece is the **selector**. Basically the html tag by which we use this component. *The selector should be a string here you may setup any anem you want but you should make sure that it is a unique selector that you don't accidentially override a default html element.* So typically you prefix it with app-and thena fitting name like server because it's a server component. This is my own selector by which i can now later use this component in my other components html files.

```
@Component({
  selector:'app-server',
  templateUrl:'./server.component.html'
})
```
#### server.component.html
```
<p>The Server Component </p>
```
our module file structure

```
app
  server
    server.component.ts
    server.component.html    
```

With these we created our new component called server.   

