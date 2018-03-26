## Navigating with Context

In the previous chapter, you learned how to integrate an API into your app. 

In this chapter, you'll be wrapping up the SpaceX app by creating a launch details page. You'll create the Details page, navigate from the List page, and learn how to pass context (or data) to the Details page during navigation. Finally, you'll learn how to use various Theme classes to align UI elements. 

### Navigating to the Details Page

Now that you've created a page showing the list of launches, let's build a details page that shows the details of a launch. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Details page
</h4>

In chapter 3 you added the list page to your app by creating a new component. Adding the details page is the same process. In this exercise, you'll be creating the Details page.

We're not going to walk you through this process step by step, so try it out for yourself. If you're new to Angular, that's ok. Don't feel like you need to have mastered what it takes to create a new page without help. We'll give you a few pointers: first, review what you did in [chapter 3](#chapter3.0); second, use this checklist to make sure you didn't forget any steps.

> **IMPORTANT**
>
> Before you get started, we'll be navigating to the details page in a different way than we did previously. So, you won't need to create a tap event handler in the UI markup or Detail component class. You will still need to register the *detail* route, so don't forget to create that.

<br/>

#### Checklist for creating the Detail component

If you need an assist when creating the Detail component, use this checklist:
* Add a folder for the new page/component.
* Add the new component (remember the Playground has a feature to quickly add a component).
* Register the new component in the app module (`app.module.ts` file).
* Register the new component as a route in `app-routing.module.ts` file. 

When you're finished creating the Detail component, you should have:
* A folder named *details* in the *views* folder.
* A `details.component.ts`, `details.component.html`, and `details.component.css` file in the *details* folder (see contents of these folders below).
* An updated `app.module.ts` file that registers the Detail component (see updated file below).
* The Details component registered as a route in the `app-routing.module.ts` file (see updated file below).

<br/>

#### details.component.ts

<br/>

```javascript
import { Component, OnInit } from "@angular/core";

@Component({
	selector: "detail",
	moduleId: module.id,
	templateUrl: "./detail.component.html",
	styleUrls: ['./detail.component.css']
})
export class DetailComponent implements OnInit {

	constructor() {
	}

	ngOnInit(): void {
	}
}
```

<br/>

#### detail.component.html

<br/>

```xml
<ActionBar title="Detail" class="action-bar">
</ActionBar>

<ScrollView class="page">
	<StackLayout class="home-panel">
		<!--Add your page content here-->
	</StackLayout>
</ScrollView>
```

<br/>

#### detail.component.css

<br/>

```css
.home-panel{
	vertical-align: center;
	font-size: 20;
	margin: 15;
}
```

<br/>

#### app.module.ts

<br/>

```javascript
import { NgModule, NO_ERRORS_SCHEMA } from "@angular/core";
import { NativeScriptModule } from "nativescript-angular/nativescript.module";
import { AppRoutingModule } from "./app.routing";
import { AppComponent } from "./app.component";
import { HttpClientModule } from "@angular/common/http";

import { HomeComponent } from "./views/home/home.component";
import { ListComponent } from "./views/list/list.component";
import { DetailComponent } from "./views/detail/detail.component";
import { LaunchService } from "./services/launchService";

// Uncomment and add to NgModule imports if you need to use two-way binding
// import { NativeScriptFormsModule } from "nativescript-angular/forms";

// Uncomment and add to NgModule imports  if you need to use the HTTP wrapper
// import { NativeScriptHttpModule } from "nativescript-angular/http";

@NgModule({
    bootstrap: [
        AppComponent
    ],
    imports: [
        NativeScriptModule,
        AppRoutingModule,
        HttpClientModule
    ],
    declarations: [
        AppComponent,
        HomeComponent,
        ListComponent,
        DetailComponent
    ],
    providers: [

    ],
    schemas: [
        NO_ERRORS_SCHEMA
    ]
})
/*
Pass your application module to the bootstrapModule function located in main.ts to start your app
*/
export class AppModule { }
```

<br/>

#### app-routing.module.ts

<br/>

```javascript
import { NgModule } from "@angular/core";
import { NativeScriptRouterModule } from "nativescript-angular/router";
import { Routes } from "@angular/router";

import { HomeComponent } from "./views/home/home.component";
import { ListComponent } from "./views/list/list.component";
import { DetailComponent } from "./views/detail/detail.component";

const routes: Routes = [
    { path: "", component: HomeComponent },
    { path: "home", component: HomeComponent },
    { path: "list", component: ListComponent },
    { path: "detail", component: DetailComponent },
];

@NgModule({
    imports: [NativeScriptRouterModule.forRoot(routes)],
    exports: [NativeScriptRouterModule]
})
export class AppRoutingModule { }
```

This concludes the exercise.

<div class="exercise-end"></div>

That's it! Now that you have the Details component created, we'll be learning how to navigate and pass data to it.

### Passing Data to the Details Page

In chapter 3, you learned how to navigate between components by:
* Binding a tap event handler to a button.
* Passing the `/list` route to the `navigate()` function of the `RoutingExtensions` class.

This is a great way to navigate between pages/components, but there's also a different way. In this section, you'll learn how to use an *Angular/NativeScript attribute directive* to navigate (and pass data) to the Details component. 

> **What's an attribute directive?**
>
> In Angular, an attribute directive is a piece of code added to the UI markup that modifies the appearance (or behavior) of the UI element. It sounds really fancy (like most Angular terms do), but it's really just like HTML attributes that Angular knows how to decipher. If you're interested in learning more about Angular attribute directives, check out their [documentation](https://angular.io/guide/attribute-directives).

Now that you know a little about Angular attribute directives, let's use one to navigate between the list and details components!

<h4 class="exercise-start">
    <b>Exercise</b>: Using an attribute directive to navigate between components
</h4>

In this exercise, you'll learn about the `nsRouterLink` attribute directive, and see how it can make navigating between components easy.

> **nsRouterLink Attribute Directive**
>
> The `nsRouterLink` attribute directive is an attribute directive provided by NativeScript. It works like the Angular [routerLink](https://angular.io/guide/router#router-links) attribute directive, and allows you to add navigation capabilities to UI elements without needing to write code to bind to the tap event handler.

> **How do I choose?** 
>
> You may be thinking that navigation in Angular apps is confusing, because we've introduced 2 ways of navigating between pages/components. When should you write code and bind to the tap event handler, and when should you use `nsRouterLink`? We recommend you use `nsRouterLink` for navigation, by default. This will navigate you to components the Angular way. If you need to perform other actions before you navigate (like change UI components, submit data to a web API, or some other business logic), use a tap event handler.

#### Adding the *nsRouterLink* attribute directive

Start by opening the `list.component.html` file, and locate the `ng-template` you added to the Upcoming Launches `ListView`. Your code should look like:

```xml
<ng-template let-item="item">
    <GridLayout rows="*, *, *" columns="auto, *" class="list-group-item">
        <Image row="0" col="0" rowSpan="3" [src]="item.links.mission_patch" class="img-circle"></Image>
        <Label row="0" col="1" [text]="item.rocket.rocket_name"></Label>
        <Label row="1" col="1" [text]="item.launch_date_utc"></Label>
        <Label row="2" col="1" textWrap="true" [text]="item.launch_site.site_name_long"></Label>
    </GridLayout>
</ng-template>
```

Next, add the `nsRouterLink` attribute to the `GridLayout`:

```xml
<ng-template let-item="item">
    <GridLayout rows="*, *, *" columns="auto, *" [nsRouterLink]="['/detail', item.flight_number]" class="list-group-item">
        <Image row="0" col="0" rowSpan="3" [src]="item.links.mission_patch" class="img-circle"></Image>
        <Label row="0" col="1" [text]="item.rocket.rocket_name"></Label>
        <Label row="1" col="1" [text]="item.launch_date_utc"></Label>
        <Label row="2" col="1" textWrap="true" [text]="item.launch_site.site_name_long"></Label>
    </GridLayout>
</ng-template>
```

That's it! But, let's decode what's happening. 

By adding `[nsRouterLink]="['/detail', item.flight_number]"` to the `GridLayout` element, you tell Angular to navigate to the `/detail` route, passing in `item.flight_number` to the component linked to that route.

#### Updating the /detail route

Ok, we may have been a bit misleading by saying "that's it" above. There is one more step to making the `nsRouterLink` attribute directive navigate (and pass data) to the Detail component correctly. 

As you'll recall, you passed `item.flight_number` to the Details component above. But, the route doesn't know anything about the flight number being passed in, so we need to "educate it" ;-).

Open the `app-routing.module.ts` file, and locate the `/detail` route you created earlier in the chapter. You should see:

```javascript
{ path: "detail", component: DetailComponent }
```

Update the *detail* route so it expects data will be supplied to the route when it is navigated to:

```javascript
{ path: "detail/:id", component: DetailComponent }
```

You're finished! By adding `/:id` to the `/detail` route, you instruct Angular to expect (and parse) the data passed into it as a variable named `id`. 

Update the app on your mobile device and check that you can navigate between the List and Detail pages by tapping on a launch. 

> **DON'T FORGET**
>
> You just added the `nsRouterLink` attribute directive to the Upcoming Launches template, so don't forget to add it to the Past Launches list.

This concludes the exercise. In the next exercise, you'll learn how to access the `id` variable of the `/detail` route.

<div class="exercise-end"></div>

### Displaying Launch Details

In the last section, you learned how to use the `nsRouterLink` attribute directive to navigate (and pass data) to the Detail component. Now, let's learn how to access the flight number that you passed into the `id` router variable.

<h4 class="exercise-start">
    <b>Exercise</b>: Accessing navigation route data in a component
</h4>

In this exercise, you'll learn how to access navigate route data in the Detail component. 

#### Retrieving data from a route variable

Let's start by opening the `details.component.ts` file. We haven't changed the file since we created it, so you should have:

```javascript
import { Component, OnInit } from "@angular/core";

@Component({
	selector: "detail",
	moduleId: module.id,
	templateUrl: "./detail.component.html",
	styleUrls: ['./detail.component.css']
})
export class DetailComponent implements OnInit {

	constructor() {
	}

	ngOnInit(): void {
	}
}
```

Update the Details component with some new code. It's ok if you don't understand it right now, we'll explain.

```javascript
import { Component, OnInit } from "@angular/core";
import { ActivatedRoute } from "@angular/router";

@Component({
	selector: "detail",
	moduleId: module.id,
	templateUrl: "./detail.component.html",
	styleUrls: ['./detail.component.css']
})
export class DetailComponent implements OnInit {

	constructor(
		private route: ActivatedRoute) { }

	ngOnInit(): void {
		const flightNumber = +this.route.snapshot.params["id"];
	}
}
```

You just added 3 things to the Details component:
* Imported the `ActivatedRoute` class, which is an Angular class used to access route information (like the `id` variable you passed in).
* Injected an instance of the `ActivatedRoute` class via the constructor (you'll recall you did that previously in the workshop).
* Retrieved the value of the `id` variable and stored it in the `flightNumber` variable.

Most of the code you added should be familiar (the structure, but perhaps not the actual classes). We're not going to dive deep into the `ActivatedRoute` class, but we think it's a good opportunity to explain `const flightNumber = +this.route.snapshot.params["id"];`.

Let's start with `this.route.snapshot.params["id"]` - this retrieves the value passed into the `id` route variable. As you'll recall, this is the flight number we passed in via the `nsRouterLink` attribute directive. 

Next, what's with that `+` in front of `this.route.snapshot.params["id"]`? You may not have seen this before, and it's something we often forget. The `+` is a JavaScript feature that converts the value of `this.route.snapshot.params["id"]` to a number. It's needed because data passed via Angular routes are strings.

> **OnInit vs Component Constructor**
>
> You may be wondering why you didn't retrieve the route variable in the constructor. This is an Angular style guideline. Per Angular guidelines, component constructors should only be used to initialize class references. No processing, business logic, or any action that could take time should go into the constructor. Instead, Angular recommends placing these types of activities (like route parameter retrieval) be done in the `OnInit()` function. There are other details about why `OnInit()` should be used, but we're not going to cover them. For more details, see a good write-up by [Todd Motto](https://toddmotto.com/angular-constructor-ngoninit-lifecycle-hook).

This concludes the exercise. In the next exercise, you'll reuse the Launch service previously created to retrieve the details about a specific launch.

<div class="exercise-end"></div>

Cool. You just passed data between pages/components and retrieved the data. Let's keep going by getting the details of a launch.


<h4 class="exercise-start">
    <b>Exercise</b>: Retrieving launch details
</h4>

In this exercise, you'll retrieve launch details from the launch service.

#### Updating the launch service

Let's start by adding a function to the Launch service to retrieve data about a specific launch. 

Open the `launchService.ts` file.

Add a function named `getLaunch()` to the `LaunchService` class:

```javascript
public getLaunch(flight_number: number): Launch {
    let results = this.launches
        .filter((l: Launch) => l.flight_number == flight_number);
    if (results.length > 0) return results[0];
    return null;
}
```

We're not going to explain the details of this class, but it retrieves a specific launch by passing in the launch number. How convenient ;-).

#### Injecting the Launch service into the Detail component

Now, head back to the Details component, and inject the Launch service:

```javascript
import { Component, OnInit } from "@angular/core";
import { ActivatedRoute } from "@angular/router";

import { LaunchService } from "../../services/launchService";

@Component({
	selector: "detail",
	moduleId: module.id,
	templateUrl: "./detail.component.html",
	styleUrls: ['./detail.component.css'],
	providers: [LaunchService]
})
export class DetailComponent implements OnInit {

	constructor(
		private route: ActivatedRoute,
		private launchService: LaunchService) { }

	ngOnInit(): void {
		const flightNumber = +this.route.snapshot.params["id"];
	}

}
```

As you can see, you added a few things:
* Imported the `LaunchService` class.
* Added the `LaunchService` class as a provider.
* Injected an instance of the `LaunchService` class by adding it to the constructor.

You've done this before, so it should look familiar. 

#### Retrieving a launch

Next, update the Details component to get a launch from the Launch service:

```javascript
import { Component, OnInit } from "@angular/core";
import { ActivatedRoute } from "@angular/router";

import { Launch } from "../../models/launch";
import { LaunchService } from "../../services/launchService";

@Component({
	selector: "detail",
	moduleId: module.id,
	templateUrl: "./detail.component.html",
	styleUrls: ['./detail.component.css'],
	providers: [LaunchService]
})
export class DetailComponent implements OnInit {
	launch: Launch;

	constructor(
		private route: ActivatedRoute,
		private launchService: LaunchService) { }

	ngOnInit(): void {
		const flightNumber = +this.route.snapshot.params["id"];
		this.launch = this.launchService.getLaunch(flightNumber);
	}
}
```

You'll notice that you added a public `launch` variable to the Details component, then populated it in the `OnInit()` function by calling the `getLaunch()` you created previously. 

That's all!

This concludes the exercise. In the next exercise, you'll update the UI markup to display the launch details.

<div class="exercise-end"></div>

In this final exercise, you'll finish the SpaceX app by adding UI markup to the Details page.


<h4 class="exercise-start">
    <b>Exercise</b>: Retrieving launch details
</h4>

In this exercise, you'll update the UI of the Details page to display launch details.

#### Establishing a foundation layout

In previous chapters, you learned about the `ActionBar`, `ScrollView`, and `StackLayout` elements. 

* A `ActionBar` is used to set the page title.
* A `ScrollView` allows the page to scroll if content extends past the original view.
* A `StackLayout` allows you to *stack* UI elements above/below in a vertical manner.

Update the `details.component.html` file.

```xml
<ActionBar title="Launch Details" icon="" class="action-bar">
</ActionBar>
<ScrollView class="page">
	<StackLayout>

	</StackLayout>
</ScrollView>
```

> **What's the page class name?**
>
> That's another use of the NativeScript Theme plugin. The `page` class is a convenient class name that makes you app pages look uniform with very little effort. To learn more, check out the [documentation](https://docs.nativescript.org/ui/theme#page).

#### Adding a Mission Patch

With the foundation set, let's start adding various UI components.

Add an image inside the stack layout. You've added an images throughout the workshop, and this image is like the images you added to the List component. Note the `src` attribute is data-bound to the `links.mission_patch` property of the `launch` variable.

```xml
<Image [src]="launch.links.mission_patch"></Image>
```

> **How can the page bind to the launch variable?**
>
> You might be wondering why the UI page can bind to the `launch` variable. If you look back earlier in this chapter, you'll recall that we added a public variable named `launch` to the DetailComponent class. Public variables can be data-bound.

Next, update the `details.component.css` file to restrict images to 50% width.

```css
image {
    width: 50%;
}
```

#### Adding the Flight Number

Add a flight number by binding to the `flight_number` property.

```xml
<Label 
	text="{{ 'Flight Number: ' + launch.flight_number }}" 
	class="body m-l-20 m-t-20" 
	textWrap="true">
</Label>
```

You'll notice that we used an advanced form of Angular data-binding that allows you to mix text and data-bound variables. The double-mustache syntax treats it's internal text as a data-binding expression. Using data-binding expressions like this comes in handy, making it easier to seamlessly blend text and variables.

> **What to the CSS class names do?**
>
> The `body`, `m-l-20`, and `m-t-20` are more CSS class names from the NativeScript Theme plugin. The `body` class name styles the label text as long-form paragraphs. You can learn more about text formatting in the [text formatting documentation](https://docs.nativescript.org/ui/theme#text). 
>
> The other class names also come from the themes plugin, and are short-hand for alignment and spacing. Generally, `m` stands for *CSS margin*, `l` and `t` stand for *left* and *top*, and the number value stand for *20 space units*. So, you can read it as *margin-left-20* and *margin-top-20*. You'll continue to use theme class names like this throughout the page. If you'd like to learn more, check out the [padding and margin documentation](https://docs.nativescript.org/ui/theme#padding-and-margin).

#### Launch Date, Site, & Details

Add three more launch data points the stack layout below the launch number.

```xml
<Label 
	text="{{ 'Date: ' + launch.launch_date_utc }}" 
	class="body m-l-20 m-t-20" 
	textWrap="true">
</Label>

<Label 
	[text]="launch.launch_site.site_name_long" 
	class="body m-l-20 m-r-20 m-t-20" 
	textWrap="true">
</Label>

<Label 
	[text]="launch.details" 
	class="body m-l-20 m-r-20 m-t-20" 
	textWrap="true">
</Label>
```

#### Launch Article

Each launch has an official article describing the launch. It's nice to show the URL, but on a mobile device, that's not enough. You really need to hyperlink the URL to open in a browser. You'll be adding the URL to the page as a label, and then using a tap event handler to open the URL in a browser.

Start by adding the launch article label to the stack layout.

```xml
<Label 
	text="{{ 'Article: ' + launch.links.article_link }}" 
	class="body m-l-20 m-r-20 m-t-20" 
	textWrap="true" 
	(tap)="onLinkTap(launch.links.article_link)">
</Label>
```

Next, implement the `onLinkTap()` function in `details.component.ts`. 

```javascript
onLinkTap(link: string): void {
	// to do: open the link in a browser
}
```

Now that you have the `onLinkTap()` stub added, turn your attention to the implementation of the function. 

You're welcome to write custom code for Android or iOS that opens a URL in the appropriate browser, but NativeScript has a collection of utility functions that provide various cross-platform functionalities (like opening a URL). They're done the heavy lifting for you, so let's take advantage of it!

Import the utility classes into `detail.component.ts` by adding this import statement.

```javascript
import * as utils from "utils/utils";
```

Then, use the `utils` class to call the `openUrl()` function. Your completed `onLinkTap()` function should look like this.

```javascript
onLinkTap(link: string): void {
	utils.openUrl(link);
}
```

Now, when you tap the launch article URL, a browser will open, loading the URL.

#### Launch Video

The last UI element to add is the launch video. After all, what's a SpaceX app without a video of the launch (and my personal favorite is the Falcon Heavy - check it out - *definitely*).

Add another label to the stack layout.

```xml
<Label 
	text="{{ 'Video: ' + launch.links.video_link }}" 
	class="body m-l-20 m-r-20 m-t-20" 
	textWrap="true" 
	(tap)="onLinkTap(launch.links.video_link)">
</Label>
```

You'll notice you were able to reuse the `onLinkTap()` function with this link. Pretty convenient. 

This concludes the exercise.

<div class="exercise-end"></div>

Well done. You've finished the workshop, and have a sweet SpaceX mobile app to show your friends and family.

This concludes the workshop.