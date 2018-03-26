## Pages and Navigation

In this chapter, you'll be creating a page to view recent and upcoming SpaceX launches, then you'll learn how to navigate to and from it. You'll also learn about these NativeScript elements:

*`ActionBar`

### Creating the List page

In the last chapter, you refined the Home page of your app, and finished by adding a button labeled View Launches. In this section, you'll put that button to use. 

But, before we can start using it, we'll need to create a page to navigate to. Let's start by adding the List page. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the List page
</h4>

In this exercise, you'll be adding the List page.

In a previous chapter you learned how to add a page (or component) via the Playground. You'll recall it's straight-forward and can be done by clicking the 3 dots next to a folder and selecting the "Add component" option. 

If you're comfortable doing this on your own, feel free to proceed by creating a folder underneath views named "list", then adding the List component. Your Playground should like this when you've finished:

<img src="images/chapter3/list-1.png" class="img-small" />

> **Don't forget!**
>
> After adding the List component folder and files, you need to register it in the `app.module.ts` file.

If you can get this far on your own, skip to the end of this exercise. If not, it's ok. Let's review how to add a component.

#### Adding a page in the Playground

The first step to creating a new page (or component) is to create a folder for the page. As you've learned earlier, Angular components should be placed inside a folder. 

Start by adding a folder named "list" to the "views" folder. Click the 3 dots next to the "views" folder:

<img src="images/chapter3/list-2.png" class="img-small" />

Select "Add folder" and name the folder "list":

<img src="images/chapter3/list-3.png" class="img-small" />

Then, create the "list" component by clicking the 3 dots next to the "list" folder, selecting "Add component":

<img src="images/chapter3/list-4.png" class="img-medium" />

After adding the list component, you should see:

<img src="images/chapter3/list-5.png" class="img-small" />

Finally, open the `app.module.ts` file and add the List component to the app module.

```javascript
import { NgModule, NgModuleFactoryLoader, NO_ERRORS_SCHEMA } from "@angular/core";
import { NativeScriptModule } from "nativescript-angular/nativescript.module";

import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";

import { HomeComponent } from "./views/home/home.component";
import { ListComponent } from "./views/list/list.component";

@NgModule({
    bootstrap: [
        AppComponent
    ],
    imports: [
        NativeScriptModule,
        AppRoutingModule
    ],
    declarations: [
        AppComponent,
        HomeComponent,
        ListComponent
    ],
    schemas: [
        NO_ERRORS_SCHEMA
    ]
})
export class AppModule { }
```

This concludes the exercise.

<div class="exercise-end"></div>

### Navigating to the List page

Now that you've created the List page, let's go back the button on the Home page and add navigation. 

<h4 class="exercise-start">
    <b>Exercise</b>: Navigating to the List page
</h4>

In this exercise, you'll be modifying the Home component's `home.component.html` and `home.component.ts` files to add navigation to the List page.

#### Adding a tap event handler to a button

Let's start by opening the Home component's markup file (home.component.html).

In the last chapter, you added a button labeled "View Launches":

```xml
<Button 
    text="View Launches" 
    class="btn btn-primary">
</Button>
```

Add a tap event handler attribute to the button's markup. Don't worry if you don't understand what's going on right now, we'll explain it in a moment:

```xml
<Button 
    text="View Launches" 
    class="btn btn-primary"
    (tap)="onViewLaunchesTap()">
</Button>
```

> **What did I just do?** 
>
> First, you need to know that every UI element in NativeScript has a variety of events. We don't have enough time to detail each event, and many of the events are intuitive. For example, buttons have "tap" events. In Angular, you can bind (or attach) a function to an event. By adding `(tap)="onViewLaunchesTap()"` to the button element, you told your app to run the `onViewLaunchesTap()` function when the button is tapped. 

> **Angular: Where to learn more** 
>
> Ok, we'll admit it - if you've used Angular before, you'll know there's a lot more to the binding syntax we just covered. Unfortunately, in a short workshop, we don't have time to cover it in greater detail. If you'd like to learn more, check out [the Angular documentation](https://angular.io/guide/user-input).  

> **NativeScript: Where to learn more** 
>
> If you'd like to learn more about the events available to various UI elements, check out the [NativeScript documentation](https://docs.nativescript.org/angular/core-concepts/angular-data-binding).

Let's get back to navigation...

#### Adding the tap event handler code

Now that you've added the markup to bind the "View Launches" button to the `onViewLaunchesTap()`, let's add that function.

Open the `home.component.ts` file and replace the Home component code with the code below. 

> **Note**
>
> We know there's a lot of new code here, and we'll walk you through it in just a moment.

```javascript
import { Component, OnInit } from "@angular/core";
import { RouterExtensions } from "nativescript-angular/router";

@Component({
	selector: "home",
	moduleId: module.id,
	templateUrl: "./home.component.html",
	styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {
	constructor(
		private routerExtensions: RouterExtensions) {
	}

	ngOnInit(): void {
	}

	onViewLaunchesTap(): void {
		this.routerExtensions.navigate(["list"]);
	}
}
```

In this updated code, you'll notice 3 major changes:
* At the top: `import { RouterExtensions } from "nativescript-angular/router";`
* In the constructor: `private routerExtensions: RouterExtensions`
* The `onViewLaunchesTap()` function

Let's walk through each of these one by one.

#### Importing RouterExtensions

At the top of the Home component code, you imported an additional class named RouterExtensions from `nativescript-angular/router`. This class is a NativeScript-specific class for interacting with Angular's routing/navigation system. There's not much more to learn about it, so just remember that you need to import it on every page that you'll need to use navigation. 

And here's an extra secret...we've found that you'll need this in about every component you create.

#### Including RouterExtensions in the constructor

The second addition to the Home component is passing an instance of the RouterExtensions class into the constructor:

```javascript
constructor(
    private routerExtensions: RouterExtensions) {
}
```

By adding this to the Home component's constructor, you have access to an instance of the RouterExtensions class from within the Home component class. 

> **But, how does this work?** 
>
> You may be interested into how the Home component *actually* gets an instance of the RouterExtensions class. Angular's [dependency injection](https://angular.io/guide/dependency-injection) does this heavy lifting. If you're not familiar with dependency injection, we recommend you read up on Angular's site.

#### The onViewLaunchesTap() function

The final change to the Home component is the addition of the `onViewLaunchesTap()` function:

```javascript
onViewLaunchesTap(): void {
    this.routerExtensions.navigate(["list"]);
}
```

As you'll recall, we imported the RouterExtensions class at the top of the file and injected an instance of RouterExtensions into the Home component. This allows us to access it via `this.routerExtensions`.

The RouterExtensions class has a function named `navigate()`, which takes an array of strings as a parameter. The first value in that array is the name of a *registered route* in our application. 

> **Registered routes?** 
>
> A registered route is a key-value pair, where the key is a string (like "list") and the value is a component (like the List component we just created). You may have noticed we haven't "registered" the "list" route yet, but we'll do that next.

Now that you know how the `navigate()` function works, you can see that when the "View Launches" button is tapped, the `onViewLaunchesTap()` function navigates to the registered route named "list".

#### Registering the "list" route

To close out our journey to navigate between pages / components, we need to register the "list" route and point it to our List component.

Open the `app-routing.module.ts` file, import the List component, and add an entry to the Routes array:

```javascript
import { NgModule } from "@angular/core";
import { NativeScriptRouterModule } from "nativescript-angular/router";
import { Routes } from "@angular/router";

import { HomeComponent } from "./views/home/home.component";
import { ListComponent } from "./views/list/list.component";

const routes: Routes = [
    { path: "", component: HomeComponent },
    { path: "home", component: HomeComponent },
    { path: "list", component: ListComponent },
];

@NgModule({
    imports: [NativeScriptRouterModule.forRoot(routes)],
    exports: [NativeScriptRouterModule]
})
export class AppRoutingModule { }
```

#### Testing it out

Now that we've finished adding navigation, reload the app on your mobile device. When you tap the "View Launches" button, you should navigate to the List page/component:

<img src="images/chapter3/list-6.png" class="img-small" />

This concludes the exercise.

<div class="exercise-end"></div>

Nice work! You've just learned how to add navigation to your app. As a quick reminder, there are a few steps to take:
* Add a folder for the new page/component
* Add the new component
* Register the new component in the app module (`app.module.ts` file)
* Bind a button's tap event to a function with `(tap)="onTapFunction()"`
* Import `RouterExtensions` into the originating component's class code
* Using Angular's dependency injection, inject a `RouterExtensions` instance into the originating component's constructor
* Add the tap event handler function to the originating component's class code
* Register the new component as a route in `app-routing.module.ts` file 

> **NOTE**
>
> Yeah, we know, it's a lot of code just to navigate, but that's the Angular way ;-)

### Adding an Action Bar

In the final part of this chapter, you'll learn how to use NativeScript's Action Bar. 

> **Action Bar** 
>
> The Action Bar is a UI element that controls the upper area of the screen, allowing you to create (or customize) a "header" of the page. 

Here's the area of the page we're going to modify:

<img src="images/chapter3/list-7.jpg" class="img-small" />

Action Bars are a versatile UI element in NativeScript, and you can use them to customize your app in various ways, including: navigation to the previous page, header icons, and page title/headings. We're not going to dive into the intimate details of Action Bars, so if you're interested in learning more, check out the [official documentation](https://docs.nativescript.org/angular/code-samples/ui/action-bar).

Now that you know a little bit about the Action Bar,let's dive in and customize it.

<h4 class="exercise-start">
    <b>Exercise</b>: Customizing an Action Bar
</h4>

In this exercise, you'll be modifying the List component's Action Bar (ever so slightly) to change the header text of the List page.

#### Reviewing the Action Bar markup

Earlier in this chapter, you created the List component, and left the UI markup alone. Open the `list.component.html` file again and review it's contents. It should look similar to:

```javascript
<ActionBar title="List" class="action-bar">
</ActionBar>

<ScrollView class="page">
	<StackLayout class="home-panel">
		<!--Add your page content here-->
	</StackLayout>
</ScrollView>
``` 

As shown in the markup above, an Action Bar can be customized by adding a title attribute. The title attribute is straight-forward and sets the title of the page. The `action-bar` class name helps to style it to match your overall app theme's and applies default styles using the NativeScript Theme plugin.

> **Theme Details** 
>
> For more information about styling the Action Bar with the Theme plugin, check out the [official documentation](https://docs.nativescript.org/ui/theme#actionbar).

As for the markup following the Action Bar, ignore it. You'll be replacing it later.

#### Update the Action Bar

Let's make a simple modification to the Action Bar and update the title.

Change the title to "SpaceX Launches" or something equally appropriate:

```xml
<ActionBar title="SpaceX Launches" class="action-bar">
</ActionBar>
```

Refresh the app on your mobile device and you should see something similar on the List page:

<img src="images/chapter3/list-8.png" class="img-small" />

> **NOTE** 
>
> This was a simple example on using an Action Bar. If you're in for a challenge, try adding an icon to the Action Bar, customizing the background color, or changing the back button icon. There are a ton of online resources for customizing the Action Bar in NativeScript. [Let me Google that for you](http://lmgtfy.com/?q=NativeScript+Action+Bar+Customization).

This concludes the exercise. 

<div class="exercise-end"></div>

### Updating the Home page Action Bar

In the last chapter, we said you'd be updating the Home page action bar to fix an Android issue. 

> **Cross-platform Differences**
>
> In the cross-platform work, rendering native UI components (like NativeScript does) is a tough problem because of subtleties in the underlying mobile platforms. As a mobile developer, you'll run into these from time to time. NativeScript does well at abstracting these differences from you, but dealing with Angular's status bar / action bar is one of those times you need to do a little more legwork. Let's get started and fix the problem.

<h4 class="exercise-start">
    <b>Exercise</b>: Fixing the Home page Action Bar on Android
</h4>

Let's start by investigating the problem on Android. In the last chapter, we removed the Action Bar element from the UI. When you did this, it removed it from iOS devices, but it did not remove it from Android devices. It displays an ugly *PREVIEW* text at the top. 

<img src="images/chapter3/android-fail.png" class="img-small" />

The appearance of the status bar / action bar at top makes the app less appealing. So let's remove it.

#### Removing the Action Bar on Android

Start by opening the `home.component.ts` file. 

Import the `Page` class at top:

```javascript
import { Page } from "ui/page";
```

Next, update the `constructor` and `ngOnInit()` function:

```javascript
constructor(
    private routerExtensions: RouterExtensions,
    private page: Page) {
}

ngOnInit(): void {
    this.page.actionBarHidden = true;
}
```

We're not going to dive deep on what you just did right now, but we promise to cover it later. For now, just know that when your page loads, it will set the action bar to hidden using this code: `this.page.actionBarHidden = true;`.

And let's see how it looks on Android:

<img src="images/chapter3/android-success.png" class="img-small" />

Beautiful.

This concludes the exercise. 

<div class="exercise-end"></div>



This concludes the chapter.