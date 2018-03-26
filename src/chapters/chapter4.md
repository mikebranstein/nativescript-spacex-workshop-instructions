## Displaying Data

Now that you know how to navigate between different views, you can work on making the list component more complex by displaying data. In this chapter you will learn about two new NativeScript elements:

* `ListView`
* `TabView`

### Creating a list view

<h4 class="exercise-start">
    <b>Exercise</b>: Creating a list view
</h4>

As you already know, the NativeScript playground provides numerous components you can drag and drop into your project. Go ahead and find the `ListView` component in the list of components and drag it inside the stack layout.

<img src="images/chapter4/chapter4-1.png" class="img-med" />

And you're done! you created a list view! Just kidding, but the playground does make it easy to get started learning NativeScript components. Go ahead and save your project and take a look at your app in preview.

<img src="images/chapter4/chapter4-2.jpeg" class="img-small" />

You may have noticed that there is data showing up. That's because when you drag a component in the playground it scaffolds out a lot of code for you. Take a look at `list.component.ts` and you will see the code that is generating the data in the `ListView` that you drag-and-dropped.

<img src="images/chapter4/chapter4-3.png" class="img-med" />

Before we replace this code, let's just back over the the view code and update it a bit. Replace the current `ScrollView` and `StackLayout` with a single `StackLayout` containing a `Label` and `ListView`.

```xml
<StackLayout class="page">
	<Label class="h2 text-center" text="Upcoming Launches"></Label>
	<ListView [items]="launches" class="list-group">
		<ng-template let-item="item">
			<GridLayout rows="*, *, *" columns="auto, *" class="list-group-item">
				<Image row="0" col="0" rowSpan="3" [src]="item.links.mission_patch" class="img-circle"></Image>
				<Label row="0" col="1" [text]="item.rocket.rocket_name"></Label>
				<Label row="1" col="1" [text]="item.launch_date_utc"></Label>
				<Label row="2" col="1" textWrap="true" [text]="item.launch_site.site_name_long"></Label>
			</GridLayout>
		</ng-template>
	</ListView>
</StackLayout>
```

Let's talk about the `ListView` in more depth. We're using the Angular syntax to bind the items in the `ListView` to a collection of elements called `launches`: 

`<ListView [items]="launches" class="list-group">`

When using the `ListView` component we typically define a template.

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

Let's take a moment to review the `ListView` template that we just created. You added a new layout type called `GridLayout`. The `GridLayout` allows you to place each nested element into a row or column. Rows and columns are defined in a comma separated list the the `rows` and `columns` properties. Rows and columns can be sized in the following three ways:
* (fixed number) - A fixed width in pixels
* (*) - The row or columns will take up all the remaining space left over after the other rows/columns are sized
* (auto) - The row or column will grow or shrink to the size of the child elements

In or grid example we use `*` for the rows to make each row the same size. Then our first column is auto-sized based on the image in with the second column taking up the remaining space.

The rest of the components in our `GridLayout`, the `Image` and `Label`, should be familiar to you because we used them earlier. However, take not that we are binding these to properties of `item`. The `let-item` syntax of Angular defines the `item` variable that is used to bind to and render each template for the list of `launches` that we are binding to (similar to how a for loop works).

This concludes the exercise.

<div class="exercise-end"></div>

### Binding to data from a service

Now that you have the view updated we need to produce the list of launches that our UI is binding to. In order to bind data to our UI we will first need to create some models and return them from a service. Let's get started.

<h4 class="exercise-start">
    <b>Exercise</b>: Binding to data from a service
</h4>

The first order of business is to generate some models so you can bind your data to strongly typed objects. First create a new folder underneath the `app` folder called `models`.

<img src="images/chapter4/chapter4-4.png" class="img-med" />

Next, create 4 TypeScript interfaces inside of the `models` folder.

#### rocket.ts

Specific data on the rocket that was launched.

```javascript
export interface Rocket {
    rocket_id: string;
    rocket_name: string;
}
```

#### links.ts

Metadata about the rocket launch.

```javascript
export interface Links {
    mission_patch: string;
    article_link: string;
    video_link: string;
}
```

#### launchSite.ts

Location data about where the rocket was launched from.

```javascript
export interface LaunchSite {
    site_id: string;
    site_name: string;
    site_name_long: string;
}
```

#### launch.ts

Full launch data.

```javascript
import { Rocket } from "./rocket";
import { LaunchSite } from "./launchSite";
import { Links } from "./links";

export interface Launch {
    flight_number: number;
    launch_year: string;
    launch_date_utc: string;
    launch_success: boolean
    details: string;

    rocket: Rocket;
    launch_site: LaunchSite;
    links: Links;
}
```

Now that you have created the models to hold the SpaceX launch data, you need to create a service to return it. In this chapter we will be creating a service that returns some hard-coded data. In the next chapter we will pull the data from the SpaceX public api.  Start by adding another folder to help keep your code organized called `services` underneath the `app` folder.

<img src="images/chapter4/chapter4-4.png" class="img-med" />

Next, add a `launchService.ts` file to the folder that you just created.

```javascript
import { Injectable } from "@angular/core";
import { Launch } from '../models/launch'

@Injectable()
export class LaunchService {
    private launches: Launch[];

    constructor() {
        this.launches = [
            {
                "flight_number": 42,
                "launch_year": "2017",
                "launch_date_utc": "2017-06-23T19:10:00Z",
                "rocket": {
                    "rocket_id": "falcon9",
                    "rocket_name": "Falcon 9",
                },
                "launch_site": {
                    "site_id": "ksc_lc_39a",
                    "site_name": "KSC LC 39A",
                    "site_name_long": "Kennedy Space Center Historic Launch Complex 39A"
                },
                "launch_success": true,
                "links": {
                    "mission_patch": "https://i.imgur.com/VAvulaO.png",
                    "article_link": "https://en.wikipedia.org/wiki/BulgariaSat-1",
                    "video_link": "https://www.youtube.com/watch?v=Y8mLi-rRTh8"
                },
                "details": "Second time a booster will be reused: Second flight of B1029 after the Iridium mission of January 2017. The satellite will be the first commercial Bulgarian-owned communications satellite and it will provide television broadcasts and other communications services over southeast Europe."
            },
            {
                "flight_number": 56,
                "launch_year": "2018",
                "launch_date_utc": "2018-02-22T14:17:00Z",
                "rocket": {
                    "rocket_id": "falcon9",
                    "rocket_name": "Falcon 9",
                },
                "launch_site": {
                    "site_id": "vafb_slc_4e",
                    "site_name": "VAFB SLC 4E",
                    "site_name_long": "Vandenberg Air Force Base Space Launch Complex 4E"
                },
                "launch_success": true,
                "links": {
                    "mission_patch": "https://i.imgur.com/6iUJpn4.png",
                    "article_link": "https://spaceflightnow.com/2018/02/22/recycled-spacex-rocket-boosts-paz-radar-satellite-first-starlink-testbeds-into-orbit/",
                    "video_link": "https://www.youtube.com/watch?v=-p-PToD2URA"
                },
                "details": "First flight with fairing 2.0. Will also carry two SpaceX test satellites for the upcoming Starlink constellation."
            }
        ];
    }

    public getUpcoming(): Launch[] {
        return this.launches;
    }

    public getPast(): Launch[] {
        return this.launches;
    }
}
```

For now, we will create some dummy data and return it from our service so we can quickly test our UI code. Our service just exposes 2 methods - `getUpcoming()` and `getPast()`. Both of the return the same dummy data for now but when we implement the actual api calls in the next chapter you will be getting back different data.

Next you need to call the service from the `list.component` when it loads. To do this, update the `list.component.ts` file.

```javascript
import { Component, OnInit } from "@angular/core";
import { Launch } from "../../models/launch";
import { LaunchService } from "../../services/launchService";

@Component({
	selector: "list",
	moduleId: module.id,
	templateUrl: "./list.component.html",
	styleUrls: ['./list.component.css'],
	providers: [LaunchService]
})
export class ListComponent implements OnInit {
	launches: Launch[];

	constructor(private launchService: LaunchService) { }

	ngOnInit(): void {
		this.launches = this.launchService.getPast();
	}
}
```

> **NOTE**
>
> In the updated ListComponent class, there is a new line defining `providers: [LaunchService]`. Providers are part of Angular dependency injection. In a nutshell, when Angular creates a component, it automatically creates instances of the the items in the providers array (the dependencies); the lifecycle of these dependencies is tied to the component that they are providing. For additional information you can read more about [Angular Dependency Injection](https://angular.io/guide/dependency-injection).
>
> Classes must be marked `@Injectable()` for Angular to be able to recognize them as providers. Notice that we you marked the `LaunchService` as injectable earlier in this chapter.

Go ahead and take a look at your app in the NativeScript preview app.

<img src="images/chapter4/chapter4-6.jpeg" class="img-small" />

The images aren't showing correctly! This is because you haven't given our images a proper size so you just need to update the `list.component.css` file.

```css
image {
    width: 40;
    margin-right: 16;
}
```

After saving everything looks great!

<img src="images/chapter4/chapter4-7.jpeg" class="img-small" />

This concludes the exercise.

<div class="exercise-end"></div>

### Adding tabs

<h4 class="exercise-start">
    <b>Exercise</b>: Adding tabs to the list view
</h4>

Right now you have only added the upcoming launches to the list view, well, it's time to learn about the `TabView` component and have previous launches and upcoming launches on the same `ListComponent`. Let's get started!

Update the `list.component.html` to contain 2 lists, one for upcoming launches and one for past launches.

```xml
<ActionBar title="SpaceX Launches" class="action-bar">
</ActionBar>
<TabView class="tab-view" selectedIndex="0">
	<StackLayout class="page" *tabItem="{title: 'Upcoming Launches'}">
		<Label class="h2 text-center" text="Upcoming Launches"></Label>
		<ListView [items]="upcoming" class="list-group">
			<ng-template let-item="item">
				<GridLayout rows="*, *, *" columns="auto, *" class="list-group-item">
					<Image row="0" col="0" rowSpan="3" [src]="item.links.mission_patch" class="img-circle"></Image>
					<Label row="0" col="1" [text]="item.rocket.rocket_name"></Label>
					<Label row="1" col="1" [text]="item.launch_date_utc"></Label>
					<Label row="2" col="1" textWrap="true" [text]="item.launch_site.site_name_long"></Label>
				</GridLayout>
			</ng-template>
		</ListView>
	</StackLayout>
	<StackLayout class="page" *tabItem="{title: 'Previous Launches'}">
		<Label class="h2 text-center" text="Previous Launches"></Label>
		<ListView [items]="past" class="list-group">
			<ng-template let-item="item">
				<GridLayout rows="*, *, *" columns="auto, *" class="list-group-item">
					<Image row="0" col="0" rowSpan="3" [src]="item.links.mission_patch" class="img-circle"></Image>
					<Label row="0" col="1" [text]="item.rocket.rocket_name"></Label>
					<Label row="1" col="1" [text]="item.launch_date_utc"></Label>
					<Label row="2" col="1" textWrap="true" [text]="item.launch_site.site_name_long"></Label>
				</GridLayout>
			</ng-template>
		</ListView>
	</StackLayout>
</TabView>
```

Tabs inside of the `TabView` component are denoted using the `*tabItem=` syntax. You have created 2 `ListView` components in 2 tabs. The list views should look the the ones that you just created in the last exercise. Notice that the you are binding the separate `ListViews` to different arrays named `upcoming` and `past` but the rest of the syntax is the same.

> **NOTE** 
>
> The `TabView` component sets a default selected tab using the `selectedIndex` property: `<TabView class="tab-view" selectedIndex="0">`.

Update the `list.component.ts` to add the `upcoming` and `past` arrays.

```javascript
import { Component, OnInit } from "@angular/core";
import { Launch } from "../../models/launch";
import { LaunchService } from "../../services/launchService";

@Component({
	selector: "list",
	moduleId: module.id,
	templateUrl: "./list.component.html",
	styleUrls: ['./list.component.css'],
	providers: [LaunchService]
})
export class ListComponent implements OnInit {
	upcoming: Launch[];
	past: Launch[];

	constructor(private launchService: LaunchService) { }

	ngOnInit(): void {
		this.past = this.launchService.getPast();
		this.upcoming = this.launchService.getUpcoming();
	}
}
```

Save your project and test out your tabs!

<img src="images/chapter4/chapter4-8.jpeg" class="img-small" />

This concludes the exercise.

<div class="exercise-end"></div>

Nice work, and congrats on getting through a lot of code in this chapter! In th next chapter, you'll continue to update the app by obtaining live launch data from an API.
