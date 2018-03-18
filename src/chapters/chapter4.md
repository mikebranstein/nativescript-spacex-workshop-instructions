## Displaying Data

Now that you know how to navigate between different views, you can work on making the list component more complex by displaying data. In this chapter you will learn about two new NativeScript elements:

* `ListView`
* `TabView`

### Creating a list view

<h4 class="exercise-start">
    <b>Exercise</b>: Creating a list view
</h4>

As you already know, the NativeScript playground provides numerous components you can drag and drop into your project. Go ahead and find the `ListView` component in the list of components and drag it inside the stack layout.

<img src="images/chapter4/chapter4-1.png" class="img-medium" />

And you're done! you created a list view! Just kidding, but the playground does make it easy to get started learning NativeScript components. Go ahead and save your project and take a look at your app in preview.

<img src="images/chapter4/chapter4-2.jpeg" class="img-small" />

You may have noticed that there is data showing up. That's because when you drag a component in the playground it scaffolds out a lot of code for you. Take a look at `list.component.ts` and you will see the code that is generating the data in the `ListView` that you drag-and-dropped.

<img src="images/chapter4/chapter4-3.png" class="img-medium" />

Before we replace this code, let's just back over the the view code and update it a bit. Replace the current `ScrollView` and `StackLayout` with a single `StackLayout` containing a `Label` and `ListView`.

```xml
<StackLayout class="page">
	<Label class="h2 text-center" text="Upcoming Launches"></Label>
	<ListView [items]="launches" class="list-group">
		<ng-template let-item="item">
			<GridLayout rows="*, *, *" columns="auto, *" [nsRouterLink]="['/detail', item.flight_number]" class="list-group-item">
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

<div class="exercise-end"></div>
Mauris tempor facilisis accumsan. Mauris vitae iaculis risus. Mauris volutpat suscipit neque non bibendum. Phasellus non fringilla enim. Aliquam tempor quam vel ligula porta convallis. In blandit dictum tempus. Nunc at pulvinar justo. Aliquam eu mi eros. Nunc sit amet tellus non lorem malesuada tempus. Vestibulum nunc magna, varius ut aliquam non, fermentum sodales metus. Aliquam sit amet pulvinar lacus. Sed fringilla placerat tempor. Pellentesque id elementum nibh. Interdum et malesuada fames ac ante ipsum primis in faucibus. Donec laoreet, ex eget vulputate tincidunt, enim nisi ullamcorper urna, at scelerisque tellus mi sit amet nisi. Duis ac risus ac odio efficitur dignissim vitae dapibus purus.

### Binding to data from a service

Mauris tempor facilisis accumsan. Mauris vitae iaculis risus. Mauris volutpat suscipit neque non bibendum. Phasellus non fringilla enim. Aliquam tempor quam vel ligula porta convallis. In blandit dictum tempus. Nunc at pulvinar justo. Aliquam eu mi eros. Nunc sit amet tellus non lorem malesuada tempus. Vestibulum nunc magna, varius ut aliquam non, fermentum sodales metus. Aliquam sit amet pulvinar lacus. Sed fringilla placerat tempor. Pellentesque id elementum nibh. Interdum et malesuada fames ac ante ipsum primis in faucibus. Donec laoreet, ex eget vulputate tincidunt, enim nisi ullamcorper urna, at scelerisque tellus mi sit amet nisi. Duis ac risus ac odio efficitur dignissim vitae dapibus purus.

### Adding tabs

Cras massa nulla, feugiat eu pretium in, tempor nec nulla. Nullam vel lobortis felis. Cras varius iaculis ornare. Ut at nisl sit amet leo pulvinar iaculis non ut purus. Morbi luctus magna sed condimentum cursus. Ut accumsan enim ligula, vitae dapibus odio blandit quis. Sed auctor ex non scelerisque vulputate. Nunc feugiat lobortis nisl consequat consectetur. Vivamus consequat sem id consectetur varius. Nam nec erat id est interdum venenatis eu eu felis. Suspendisse potenti. Donec non sapien in est maximus cursus eget eget nunc. Maecenas congue sapien ut tempor facilisis.
