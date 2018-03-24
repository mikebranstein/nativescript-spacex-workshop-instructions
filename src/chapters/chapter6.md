## Navigating with Context

In the previous chapter, you learned how to integrate an API into your app. 

In this chapter, you'll be wrapping up the SpaceX app by creating a launch details page. You'll create the Details page, navigate from the List page, and learn how to pass context (or data) to the Details page during navigation. Finally, you'll learn how to use various Theme classes to align UI elements. 

### Navigating to the Details Page

Now that you've created a page showing the list of launches, let's build a details page that shows the details of a launch. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Details page
</h4>

In chapter 3 you added the list page to your app by creating a new component. Adding the details page is the same process. In this exercise, you'll be creating the Details page.

We're not going to walk you through this process step by step, so try it out for yourself. If you're new to Angular, that's ok. Don't feel like you need to have mastered what it takes to create a new page without help. We'll give you a few pointers: first, review what you did in [chatper 3](#chapter3.0); second, use this checklist to make sure you didn't forget any steps.

> **IMPORTANT**: Before you get started, we'll be navigating to the details page in a different way than we did previously. So, you won't need to create a tap event handler in the UI markup or Detail component class. You will still need to register the *detail* route, so don't forget to create that.

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

> **What's an attribute directive?**: In Angular, an attribute directive is a piece of code added to the UI markup that modifies the appearance (or behavior) of the UI element. It sounds really fancy (like most Angular terms do), but it's really just like HTML attributes that Angular knows how to decipher. If you're interested in learning more about Angular attribute directives, check out their [documentation](https://angular.io/guide/attribute-directives).

Now that you know a little about Angular attribute directives, let's use one to navigate between the list and details components!

<h4 class="exercise-start">
    <b>Exercise</b>: Using an attribute directive to navigate between components
</h4>

In this exercise, you'll learn about the `nsRouterLink` attribute directive, and see how it can make navigating between components easy.

> **nsRouterLink Attribute Directive**: The `nsRouterLink` attribute directive is an attribute directive provided by NativeScript. It works like the Angular [routerLink](https://angular.io/guide/router#router-links) attribute directive, and allows you to add navigation capabilities to UI elements without needing to write code to bind to the tap event handler.

> **How do I choose?** You may be thinking that navigation in Angular apps is confusing, because we've introduced 2 ways of navigating between pages/components. When shoudl you write code and bind to the tap event handler, and when should you use `nsRouterLink`? We recommend you use `nsRouterLink` for navigation, by default. This will navigate you to components the Angular way. If you need to perform other actions before you navigate (like change UI components, submit data to a web API, or some other business logic), use a tap event handler.

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

Ok, wemay have been a bit misleading by saying "that's it" above. There is one more step to making the `nsRouterLink` attribute directive navigate (and pass data) to the Detail component correctly. 

As you'll recall, you passed `item.flight_number` to the Details component above. But, the route doesn't know anything about the flight number being passed in, so we need to "educate it" ;-).

Open the `app-routing.moduel.ts` file, and locate the `/detail` route you created earlier in the chapter. You should see:

```javascript
{ path: "detail", component: DetailComponent }
```

Update the *detail* route so it expects data will be supplied to the route when it is navigated to:

```javascript
{ path: "detail/:id", component: DetailComponent }
```

You're finished! By adding `/:id` to the `/detail` route, you instruct Angular to expect (and parse) the data passed into it as a variable named `id`. 

Update the app on your mobile device and check that you can navigate between the List and Detail pages by tapping on a launch. 

> **DON'T FORGET**: You just added the `nsRouterLink` attribute directive to the Upcoming Launches template, so don't forget to add it to the Past Launches list.

This concludes the exercise. In the next exercise, you'll learn how to access the `id` variable of the `/detail` route.

<div class="exercise-end"></div>

### Displaying Launch Details

In the last section, you learned how to use the `nsRouterLink` attribute directive to navigate (and pass data) to the Detail component. Now, let's learn how to access the flight number that you passed into the `id` router variable.

<h4 class="exercise-start">
    <b>Exercise</b>: Accessing navigation route data in a component
</h4>

In this exercise, you'll learn how to access navigate ruote data in the Detail component. 

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

Update the Details component with some new code. It's ok if you don't understand it right now, we'll exaplin.

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

This concludes the exercise. In the next exercise, you'll reuse the Launch service previosuly created to retrieve the details about a specific launch.

<div class="exercise-end"></div>

Cool. You just passed data between pages/componets and retrieved the data. Let's keep going by getting the details of a launch.








