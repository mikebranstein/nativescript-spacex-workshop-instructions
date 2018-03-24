## Navigating with Context

In the previous chapter, you learned how to integrate an API into your app. 

In this chapter, you'll be wrapping up the SpaceX app by creating a launch details page. You'll create the Details page, navigate from the List page, and learn how to pass context (or data) to the Details page during navigation. Finally, you'll learn how to use various Theme classes to align UI elements. 

### Navigating to the Details Page

Now that you've created a page showing the list of launches, let's build a details page that shows the details of a launch. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Details page
</h4>

In chapter 3 you added the list page to your app by creating a new component. Adding the details page is the same process. 

We're not going to walk you through this process step by step, so try it out for yourself. If you're new to Angular, that's ok. Don't feel like you need to have mastered what it takes to create a new page without help. We'll give you a few pointers: first, review what you did in chatper 3; second, use this checklist to make sure you didn't forget any steps.

> **IMPORTANT**: Before you get started, we'll be navigating to the details page in a different way than we did previously. So, you won't need to create a tap event handler in the UI markup or Detail component class. You will still need to register the *detail* route, so don't forget to create that.

#### Checklist for creating the Detail component

If you need an assist when creating the Detail component, use this checklist:
* Add a folder for the new page/component.
* Add the new component (remember the Playground has a feature to quickly add a component).
* Register the new component in the app module (`app.module.ts` file).
* Register the new component as a route in `app-routing.module.ts` file. 

When you're finished creating the Detail component, you should have:
* A folder named *details* in the *views* folder.
* A *details.component.ts*, *details.component.html*, and *details.component.css* file in the *details* folder (see contents of these folders below).
* An updated *app.module.ts* file that registers the Detail component (see updated file below).
* The Details component registered as a route in the *app-routing.module.ts* file (see updated file below).




If you're comfortable doing this on your own, feel free to proceed by creating a folder underneath views named "list", then adding the List component. Your Playground should like this when you've finished:

<img src="images/chapter3/list-1.png" class="img-small" />

> **Don't forget!** After adding the List component folder and files, you need to register it in the `app.module.ts` file.

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

### Passing Data to the Details Page


### Displaying Launch Details