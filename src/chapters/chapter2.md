## The Home View

Now that you understand the basics of NativeScript and how the Playground you're ready to start creating your first (or maybe not your first) NativeScript app. Over the course of this chapter and the next few chapters you will be creating an app the reads and displays [SpaceX](http://www.spacex.com) flight data.

In this chapter will focus on designing the home page and learn to use the following NativeScript elements:
* `<Button>`
* `<StackLayout>`
* `<ScrollView>`

### Layouts

Before we go too much further, I need to introduce you to something called a layout. Layouts are UI elements (similar to the `<Label />` element) that allow you to organize the UI of each page.

If you look at the `home-component` that you scaffolded in the previous chapter, you will see there is already code added to the `home-component.html` for you.

```xml
<ActionBar title="Home" class="action-bar">
</ActionBar>

<ScrollView class="page">
	<StackLayout class="home-panel">
		<!--Add your page content here-->
	</StackLayout>
</ScrollView>
```

The `ScrollView` and `StackLayout` elements are two basic layout elements (we'll talk about the `ActionBar` in a later chapter). To display multiple elements on a page, you need to use a layout like the `ScrollView` or `StackLayout` and in most cases you will want to use both. The `ScrollView` functions exactly as you would expect, it makes the content inside of it scrollable. The `StackLayout` element organizes child elements vertically or horizonatally.

>The `StackLayout` organizes child elements stacked on top of each other vertically by default.

Now that we've talked about basic layouts, let's start designing the home view.

### Designing the home view

<h4 class="exercise-start">
    <b>Exercise</b>: Using the StackLayout to organize UI elements in a "stack"
</h4>

First thing is first, go ahead and remove the `ActionBar` element from `home-component.html` because you will not need this on the home view. After deleting the `ActionBar` your app should have a blank home view inside the NativeScript preview app.

<img src="images/chapter2/chapter2-1.jpeg" class="img-small" />

Next, let's create a class to style the home view called `base` to create a nice background image for our view. Add the `base` class to the `home-component.css` file (you can remove the existing `home-panel` class because you will not be using that).

```css
.base {
    background-image: url("https://raw.githubusercontent.com/mikebranstein/nativescript-spacex-workshop/master/app/views/home/spacex_home.png");
    background-repeat: no-repeat;
    background-size: contain;
    background-color: black;
    background-position: center;
}
```

Update the `home-component.html` to utilize your new `base` class.

```xml
<ScrollView class="base">
	<StackLayout>
		
	</StackLayout>
</ScrollView>
```

You app should now have a SpaceX background image in the preview app.

<img src="images/chapter2/chapter2-2.jpeg" class="img-small" />

The last step in creating your home view is to add a button. Add a `<Button>` element inside of the `<StackLayout>` in the `home-component.html` file.

```xml
<ScrollView class="base">
	<StackLayout>
		<Button text="View Launches" class="btn btn-primary"></Button>
	</StackLayout>
</ScrollView>
```

<img src="images/chapter2/chapter2-3.jpeg" class="img-small" />

> **What are those CSS class names?**
>
> You may have noticed that you added the `btn` and `btn-primary` classes to the `<Button>` that you created and that the button styled blue. The `btn` and `btn-primary` classes are part of the [NativeScript Themes](https://docs.nativescript.org/ui/theme#buttons) that NativeScript provides to you out of the box to help style your app.

You're almost done with the home view. To make the home view look more complete we should move the button we added to the bottom of view so that it looks more polished. To complete the view, update the `home-component.html` to set the vertical alignment property of the `<StackLayout>`.

```xml
<ScrollView class="base">
	<StackLayout verticalAlignment="bottom">
		<Button text="View Launches" class="btn btn-primary"></Button>
	</StackLayout>
</ScrollView>
```

Next add a margin to the `<Button>` element by updating the `home-component.css` file.

```css
button {
    margin-bottom: 100;
}
```

You should now be able to view the completed home view in the NativeScript preview app. In the next chapter you will work on implementing an event handler when the view launches button is tapped.

<img src="images/chapter2/chapter2-4.jpeg" class="img-small" />
<div class="exercise-end"></div>