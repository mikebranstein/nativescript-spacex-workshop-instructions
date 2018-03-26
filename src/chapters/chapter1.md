## Getting Started with the NativeScript Playground

In this chapter, you'll learn how to use the NativeScript Playground to get started quickly, build your first app, and run the app on your phone.

### About the NativeScript Playground

The [NativeScript Playground](https://play.nativescript.org) is a browser-based environment for developing simple NativeScript apps. It’s a great place to get started learning NativeScript, as you can develop apps without needing to install the various SDKs and tools needed for native iOS and Android development. All you need is your browser, and an Android or iOS mobile device connected to the internet to get started. 

### Getting Started and Your First App

Now that you know about the NativeScript Playground, let's get started.

<h4 class="exercise-start">
    <b>Exercise</b>: Explore the Playground and Run an App
</h4>

In this exercise, you'll explore the NativeScript Playground and learn how to run an app built in the Playground on your mobile device.

#### Prerequisites

Before we get started, you'll need to install 2 apps on your mobile device: 

* NativeScript Playground: [iOS](https://itunes.apple.com/us/app/nativescript-playground/id1263543946?mt=8), [Android](https://play.google.com/store/apps/details?id=org.nativescript.play&hl=en)
* NativeScript Preview: [iOS](https://itunes.apple.com/us/app/nativescript-preview/id1264484702?mt=8), [Android](https://play.google.com/store/apps/details?id=org.nativescript.preview&hl=en)

In your your respective App Store (Google Play or Apple App Store), locate both apps and install them on your mobile device. If you're having trouble finding the app, use the links above.

#### Explore the NativeScript Playground

Next, navigate to the [NativeScript Playground](https://play.nativescript.org) in your browser. 

<img src="images/chapter1/playground-1.png" class="img-large" />

Click "Play now" to begin.

<img src="images/chapter1/play-now.png" class="img-small" />

After clicking "Play now" a QR code will appear, and you'll be notified that your Playground is ready:

<img src="images/chapter1/playground-ready.png" class="img-medium" />
 
Open the NativeScript Playground app on your mobile device, and select the "Scan QR code" action.

<img src="images/chapter1/scan-qr.jpg" class="img-small" />

Using the QR code scanner in the NativeScript Playground app, scan the QR code displayed on the NativeScript Playground website. 

> **NOTE**
>
> Do not scan the QR code on *this* page. Scan the QR code in the Playground.

After scanning the QR code, the NativeScript Playground app will open the NativeScript Preview app and dynamically load the code from the Playground Website and launch a native mobile app on your mobile device!

When all of this happens, you should see this on your mobile device:

<img src="images/chapter1/play-2.jpg" class="img-small" />

...and you should also see the following on the Playground website:

<img src="images/chapter1/play-3.png" class="img-large" />

Congratulations! You just used the Playground to write your first mobile app with Angular. Then, you ran the app on your phone. That was fast - and you didn't need to install anything on your computer!

OK, we know you didn't have to do much of anything to write this app, but we promise you'll learn more and build something more advanced during the workshop.

<div class="exercise-end"></div>

Before we move on, let's take a minute to understand what happened and explore the NativeScript Playground UI.

### How the NativeScript Playground Works

The NativeScript Playground is a web-based IDE. You write your Angular code in the browser, then save it. When you scan the QR code, the NativeScript Playground app coordinates with the NativeScript Preview app and reaches out to the Playground website. The code is pulled down, loaded into the NativeScript runtime in the Preview app, and renders native iOS/Android UI on your mobile device.

### Exploring the Playground UI

Now that you've learned how the Playground works, let's explore the UI.

As you'll notice, the Playground UI is similar to a basic IDE, like Visual Studio Code, Visual Studio, Eclipse, or Web Storm.

<img src="images/chapter1/play-3.png" class="img-large" />

On the left is a file explorer, where you can add or update files and folders to your mobile app:

<img src="images/chapter1/play-4.png" class="img-large" />

The large central area is a file editor with Intellisense:

<img src="images/chapter1/play-5.png" class="img-large" />

The bottom central area shows you which mobile devices are connected to the Playground and device/error logs for debugging purposes.

<img src="images/chapter1/play-6.png" class="img-large" />

> **Connected Devices** 
>
> Hold on...the Playground shows you connected devices. Yes, that's right. When your mobile device connects to the Playground, it registers itself with the website. You can see a variety of information about a connected device. 

Pretty cool, right? Well, there's something even cooler about the Playground: *LiveSync*. 

> **LiveSync**
>
> LiveSync is a technology that syncs changes made in the Playground down to your mobile device in real time. This means that you can quickly make changes to your app in the Playground and the changes will be instantly pushed to connected devices. If you've ever done mobile development before, you'll understand how useful this is - getting feedback from your code running on real mobile devices usually takes time, but with LiveSync, it's instantaneous.

### LiveSync in Action

Now that you've learned about LiveSync, let's see it in action. 

<h4 class="exercise-start">
    <b>Exercise</b>: Using LiveSync
</h4>

In this exercise, you'll learn how to use LiveSync by interacting wth the Playground website and seeing the app on your mobile device update automatically.

#### Getting Started

Before we get started with this exercise, be sure to have your Playground app loaded in the NativeScript Preview app.

If your app isn't running, press the "QR code" button in the Playground website, and re-scan the code on your mobile device:

<img src="images/chapter1/qr-code.png" class="img-small" />

#### Understanding Markup

Now that your app is running on your mobile device, let's make a change.

Start by finding the home.component.html file on the left, then open it for editing by clicking on it:

<img src="images/chapter1/home-component.png" class="img-large" />

You'll notice some markup in the home.component.html file. It's not important for you to understand the markup right now, but you should know that any markup you place in this file will affect the native UI generated on the home page of your app.

Even though you may not understand all of the markup, you can probably guess at the meaning on most tags. NativeScript UI markup is can be easy to understand, because it's similar to HTML. 

For example, look at the markup that displays a label on the screen that contains the text "Play with NativeScript!":

```xml
<Label 
    textWrap="true" 
    text="Play with NativeScript!" 
    class="h2 description-label">
</Label>
```

#### Changing markup with LiveSync

Let's change the text in the home.component.html file. 

Change the text that reads "Play with NativeScript!" to somethings else. feel free to use the code snippet below, or your own text.

```xml
<Label 
    textWrap="true" 
    text="Using LiveSync is easy and convenient!" 
    class="h2 description-label">
</Label>
```

After making this change, press the "Save" button:

<img src="images/chapter1/save-button.png" class="img-small" />

Then, look back at your mobile device, and watch the UI of the app change:

<img src="images/chapter1/app-2.jpg" class="img-small" />

Easy and cool! 

We'll continue to rely on LiveSync throughout this workshop to get instant feedback in our apps. 

<div class="exercise-end"></div>

Let's continue on and get our Playground app started.

### Cleaning up the template

In the final portion of chapter 1, you'll be cleaning up the default Angular template in the Playground to get it ready for the SpaceX app. Let's jump in!

<h4 class="exercise-start">
    <b>Exercise</b>: Clean up the default Playground template
</h4>

In this exercise, you'll reorganize files and folders in the Playground website to get ready for the SpaceX app.

#### Why?

You may be wondering why we're cleaning up the default Playground template. The default Playground template works well, but doesn't structure app pages into a "views" folder (which is a preference of ours).

#### Remove the home folder

Let's get started by removing the home folder. Find it in the Explorer, select it, click the "...", and select the "Delete" option:

<img src="images/chapter1/delete.png" />

Confirm the delete:

<img src="images/chapter1/confirm-delete.png" />

Add a folder named "views" to the "app" folder:

<img src="images/chapter1/views-folder.png" />

#### Add a new home folder and component

Now, create a "home" folder inside of the "views" folder:

<img src="images/chapter1/home-folder.png" />

Then add the "home" component by selecting the "..." next to the "home" folder and select "add component". Name the component "home":

<img src="images/chapter1/add-home.png" />

<img src="images/chapter1/add-home-2.png" />

By using the "add component" option, the Playground will scaffold a CSS, TypeScript, and HTML file for you automatically:

<img src="images/chapter1/home-scaffold.png" class="img-small" />

#### Add the home component to the app module

Next, let's add the home component to the app module. Open the app.module.ts file, and add a reference to the home component. 

You can add the home component manually or copy/paste the code below.

```javascript
import { NgModule, NgModuleFactoryLoader, NO_ERRORS_SCHEMA } from "@angular/core";
import { NativeScriptModule } from "nativescript-angular/nativescript.module";

import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";

import { HomeComponent } from "./views/home/home.component";

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
        HomeComponent
    ],
    schemas: [
        NO_ERRORS_SCHEMA
    ]
})
export class AppModule { }
```

#### Route to the new home component

Lastly, update the app-routing.module.ts file to reflect the changes in the home component:

```javascript
import { NgModule } from "@angular/core";
import { Routes } from "@angular/router";
import { NativeScriptRouterModule } from "nativescript-angular/router";
import { HomeComponent } from "./views/home/home.component";

const routes: Routes = [
    { path: "", component: HomeComponent },
    { path: "home", component: HomeComponent }
];

@NgModule({
    imports: [NativeScriptRouterModule.forRoot(routes)],
    exports: [NativeScriptRouterModule]
})
export class AppRoutingModule { }
```

<div class="exercise-end"></div>

You're finished. You replaced the default home component with a new home component located in the views folder. 

Save your Playground project online and let LiveSync do it's work. If your app got disconnected from LiveSync, just re-scan your QR code to load it up.

When you launch your app, you should see a blank page with Home at the top:

<img src="images/chapter1/home-finished.jpg" class="img-small" />

That concludes chapter 1. In the next chapter, you'll pick up from here, build out the home page, and learn about the various NativeScript UI components.