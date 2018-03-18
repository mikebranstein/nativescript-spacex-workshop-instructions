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

If you can ge thtis far on your own, skip to the end of this exercise. If not, it's ok. Let's review how to add a component.

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
> First, you need to know that every UI element in NativeScript has a variety of events. We don't have enough time to detail each event, and many of the events are intuitive. For example, buttons have "tap" events. In Angular, you can bind (or attach) a function to an event. By adding `(tap)="onViewLaunchesTap()"` to the button element, you told your app to run the `onViewLaunchesTap()` function when the button is tapped. 

> **Angular: Where to learn more** Ok, we'll admit it - if you've used Angualr before, you'll know there's a lot more to the binding syntax we just covered. Unfortunately, in a short workshop, we don't have time to cover it in greater detail. If you'd liek to learn more, check out [the Angular documentation](https://angular.io/guide/user-input).  

> **NativeScript: Where to learn more** If you'd like to learn more about the events available to various UI elements, check out the [NativeScript documentation](https://docs.nativescript.org/angular/core-concepts/angular-data-binding).

Let's get back to navigation...

#### Adding the tap event handler code

Now that you've added the markup to bind the "View Launches" button to the `onViewLaunchesTap()`, let's add that function.

Open the `home.component.ts` file and replace the Home component code with the code below. 

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
		this.page.actionBarHidden = true;
	}

	onViewLaunchesTap(): void {
		this.routerExtensions.navigate(["list"]);
	}
}
```



This concludes the exercise.

<div class="exercise-end"></div>

### Adding an Action Bar

