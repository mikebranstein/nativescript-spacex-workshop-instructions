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



### Displaying Launch Details