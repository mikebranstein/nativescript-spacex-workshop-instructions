## Getting Started with the NativeScript Playground

In this chapter, you'll learn how to use the NativeScript Playground to get started quickly, build your first app, and run the app on your phone.

### About the NativeScript Playground

The [NativeScript Playground](https://play.nativescript.org) is a browser-based environment for developing simple NativeScript apps. It’s a great place to get started learning NativeScript, as you can develop apps without needing to install the various SDKs and tools needed for native iOS and Android development. All you need is your browser, and an Android or iOS mobile device connected to the internet to get started. 

### Getting Started and Your First App

Now that you know about the NativeScript Playground, let's get started.

<h4 class="exercise-start">
    <b>Exercise</b>: Explore the Playground and Run an App
</h4>

#### Prerequisites

Before we get started, you'll need to install 2 apps on your mobile device: 

* NativeScript Playground: [iOS](https://itunes.apple.com/us/app/nativescript-playground/id1263543946?mt=8), [Android](https://play.google.com/store/apps/details?id=org.nativescript.play&hl=en)
* NativeScript Preview: [iOS](https://itunes.apple.com/us/app/nativescript-preview/id1264484702?mt=8), [Android](https://play.google.com/store/apps/details?id=org.nativescript.preview&hl=en)

In your your respective App Store (Google Play or Apple App Store), locate both apps and install them on your mobile device. If you're haivng troubel finding the app, use the links above.

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

> *NOTE*: Do not scan the QR code in the workshop.

After scanning the QR code, the NativeScript Playground app will open the NativeScript Preview app and dynamically load the code from the Playground Website and launch a native mobile app on your mobile device!

When all of this happens, you should see this on your mobile device:

<img src="images/chapter1/play-2.jpg" class="img-small" />

You should also see the following on the Playground website:

<img src="images/chapter1/play-3.png" class="img-large" />

Congratulations! You just used the Playground to write your first mobile app with Angular. Then, you ran the app on your phone. That was fast - and you didn't need to install anythign on your computer!

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

> *Connected Devices* Hold on...the Playground shows you connected devices. Yes, that's right. When your mobile device connects to the Playground, it registers itself with the website. You can see a variety of information about a connected device. 

Pretty cool, right? Well, there's somethign even cooler about the Playground: LiveSync. LiveSync is a technology that syncs changes made in the Playground down to your mobile device in real time. This means that you can quickly make changes to your app in the Playground and the changes will be instantly pushed to connected devices. If you've ever done mobile development before, you'll understand how useful this is - getting feedback from your code running on real mobile devices usually takes time, but with LiveSync, it's instantaneous.

