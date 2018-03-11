## Getting Started

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

The `ScrollView` and `StackLayout` elements are two basic layout elements (we'll talk about the `ActionBar` in a later chapter). To display multiple elements on a page, you need to use a layout like the `ScrollView` or `StackLayout` and in most cases you will want to use both. The `ScrollView` functions exactly as you would expect; it makes the content inside of it scrollable. The `StackLayout` element organizes child elements vertically or horizonatally.

>The `StackLayout` organizes child elements stacked on top of each other vertically by default.

Now that we've talked about basic layouts, let's start designing the home view.

### Designing the home view

<h4 class="exercise-start">
    <b>Exercise</b>: Using the StackLayout to organize UI elements in a "stack"
</h4>

First thing is first, go ahead and remove the `ActionBar` element from `home-component.html` because you will not need this on the home view. After deleting the `ActionBar` your app should have a blank home view inside the NativeScript preview app.

<img src="images/chapter2/chapter2-1.jpeg" class="img-small" />


<div class="exercise-end"></div>