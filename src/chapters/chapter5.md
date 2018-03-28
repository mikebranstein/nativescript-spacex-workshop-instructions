## Dynamic Data

The SpaceX app is starting to look great but you still have some work to do. Static data isn't much fun so let's work on getting data from the [SpaceX API](https://github.com/r-spacex/SpaceX-API).

> **NOTE**
>
>This chapter isn't going to cover anything specific to NativeScript. Instead you'll learn how to integrate a restful API into Angular. Even though this isn't NativeScript-specific, it's still important. Almost every mobile app you'll write will integrate with an API. 

Let's jump in! 

### RxJS

Before you call the SpaceX API we need to first discuss RxJS. You may have heard of it before - if so feel free to skip ahead. [RxJS](http://reactivex.io/rxjs/) is the ReactiveX library for JavaScript. (ok but what does that mean?)

RxJS is a library for using Observables. We aren't going to discuss observables in detail, but, you do need to know that observables are objects that allow you to subscribe events. For example, if a value changes in an observable, subscribers will be notified of the change. Luckily for us NativeScript and Angular already know how to use observables so we can bind observable objects straight to our UI when we receive them back from our API calls.

### Calling an API

<h4 class="exercise-start">
    <b>Exercise</b>: Calling an API
</h4>

To use the SpaceX API you need to update the `LaunchService` and add the following import statements.

```javascript
import { HttpClient } from '@angular/common/http';
import 'rxjs/add/operator/map';
import { Observable } from "rxjs/Observable";
```

Next add methods to make the API calls.

```javascript
public getUpcomingFromAPI(): Observable<Launch[]> {
        return this.http.get<Launch[]>('https://api.spacexdata.com/v2/launches/upcoming'); // upcoming launches
    }

public getPastFromAPI(): Observable<Launch[]> {
    return this.http.get<Launch[]>('https://api.spacexdata.com/v2/launches?start=1-1-2017&final=12-31-2020&order=desc'); // past launches
}
```

> **Where does `this.http` come from?**
>
> This (no pun intended) is an instance of the Angular `HttpClient` which needs to be injected via the constructor. Go ahead and update the constructor of the `LaunchService` to inject the `HttpClient`: `constructor(private http: HttpClient) {`.

The full code listing is below.

```javascript
import { Injectable } from "@angular/core";
import { Launch } from '../models/launch';
import { HttpClient } from '@angular/common/http';
import 'rxjs/add/operator/map';
import { Observable } from "rxjs/Observable";

@Injectable()
export class LaunchService {
    private launches: Launch[];

    constructor(private http: HttpClient) {
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

    public getUpcomingFromAPI(): Observable<Launch[]> {
        return this.http.get<Launch[]>('https://api.spacexdata.com/v2/launches/upcoming'); // upcoming launches
    }

    public getPastFromAPI(): Observable<Launch[]> {
        return this.http.get<Launch[]>('https://api.spacexdata.com/v2/launches?start=1-1-2017&final=12-31-2020&order=desc'); // past launches
    }
}
```

> **NOTE**
>
> Notice that `Observables` are returning from the SpaceX API. Go ahead and wire up the `ListComponent` to call from the API now by updating the `list-component.ts` file to use the new methods you made.

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
    upcoming: Launch[] = [];
    past: Launch[] = [];

    constructor(private launchService: LaunchService) { }

    ngOnInit(): void {
        this.launchService.getUpcomingFromAPI().subscribe(data => {
            data.forEach((model) => {
                this.upcoming.push(model);
            });
        });

        this.launchService.getPastFromAPI().subscribe(data => {
            data.forEach((model) => {   
                
                if (!model.links.mission_patch.includes('https'))
                    model.links.mission_patch = model.links.mission_patch.replace('http', 'https'); // quick fix
                
                this.past.push(model);
            });
        });
    }
}
```

The `subscribe` method is part of RxJX that we discussed earlier. When the call the SpaceX API completes, the subscribe method automatically gets called. Inside the subscribe method you are able to translate the data coming back into an array of launches which the UI already knows how to use and bind to properly.

> **NOTE** 
>
> The if statement inside `getPastFromAPI()` may look a bit strange to you (because it is). This if statement exists because by default iOS blocks non-https calls; therefore, when attempting to load the mission patch images on iOS it will just fail. This limitation of iOS can be turned off in NativeScript, but in the Playground you can't change this setting. Keep in mind that the Playground is gets you running fast, and is not meant for production code. In a production app, we'd fix this issue by ensuring all links were HTTPS in our API (that's not a bad idea), or by disabling the iOS-specific setting.

> **Production Code**
>
> In case you were wondering, moving from the Playground to production code is easy. Use the download button to down any code you've already written, ensure NativeScript is installed on your machine, then follow the online documentation for getting ready for deployment. Alternatively, check out the [chapters in our book](https://nativescript.org/book), which are dedicated to getting your apps into the stores.

The last step to making everything work is to import the `HttpModule` into the app by updating the `app.module.ts`.

```javascript
import { NgModule, NO_ERRORS_SCHEMA } from "@angular/core";
import { NativeScriptModule } from "nativescript-angular/nativescript.module";
import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";
import { HttpClientModule } from "@angular/common/http";

import { HomeComponent } from "./views/home/home.component";
import { ListComponent } from "./views/list/list.component";
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
        ListComponent
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

Save your project and take a look!

<img src="images/chapter5/chapter5-1.jpeg" class="img-small" />

This concludes the exercise.

<div class="exercise-end"></div>

Nice work. Adding remote APIs to your mobile apps isn't too difficult. Normally, we wouldn't go through the trouble of adding live data to a prototype app, but we just couldn't resist.

In the next chapter, you'll finish the SpaceX app by adding a launch details page.