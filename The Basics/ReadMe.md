Angular Basics
-

### Introduction

So now we get started with discourse and with angular and our project we're going to use and ofcourse  it's time to dive deeper into angular to understand what really does?  
* what happens behind the scenes? 
* How an angular gets  started in the first place and which base building blocks it offers us? 
* How we can build angular apps and which features we may use for this.
By the end of this section you will understand how can build your basic angular application? What it then does and what you need to change to reach a different result.	So with this let's dive into it and let's start by having a look what actually happens when we with

### How an Angular App gets Loaded and Started

Angular is a framework which allows you to create single page application.This is the single page which has served the *index.html* file.
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

Now if we have a look at this file here we actually see that somehow we kind of like to Component to strange at thing here is NgModule. But most important we get the bootstrap array which basically lists all the components which should be known to Angular at the point of time it analyzes our index.html. Here we reference our app component. So angular gets started this main.ts file, there we bootstrap an angular application and we pass this module as an argument. In this module we tell angular there is app component which you know when you try to start yourself and angular now analyze this app.component.ts read the setup we pass here, and therefore is selector is app-root. And now Angular is able to handle app-root in the index.file and it knows all right does is the selector. 

```
 bootstrap: [AppComponent]
```