# What is Flexbox?

Flexbox is a layout model in CSS that allows for the creation of flexible and responsive layouts. It is designed to make
it easier to create complex layouts without having to use floats, positioning, or table layouts.

## Flex containers

To use flexbox, you need to define a flex container which is going to be the parent and its child elements . 
You can set the container as follows:
```css
.container {
    display: flex;
}
```

This sets the display property of the container to flex, which makes it a flex container. The child elements of this
container will become flex items.

## Important Properties
In order to be able to use and customize your components as you need you will have to take into account certain properties
like:

### Flex Direction

The direction in which the flex items are laid out is controlled by the flex-direction property. This property can take
four different values: row, row-reverse, column, and column-reverse. Here's an example of how to set the direction to
row:

```css
.container {
    display: flex;
    flex-direction: row;
}
```

### Justify Content

The justify-content property is used to align the flex items along the main axis of the flex container. This property
can take five different values: flex-start, flex-end, center, space-between, and space-around. Here's an example of how
to set the justify-content property to center:

```css
.container {
    display: flex;
    justify-content: center;
}
```


### Align Items

The align-items property is used to align the flex items along the cross axis of the flex container. This property can
take five different values: flex-start, flex-end, center, baseline, and stretch. Here's an example of how to set the
align-items property to center:

```css
.container {
    display: flex;
    align-items: center;
}
```

### Flex Wrap

The flex-wrap property is used to determine whether the flex items should wrap to a new line if they don't fit within
the container. This property can take three different values: nowrap, wrap, and wrap-reverse. Here's an example of how
to set the flex-wrap property to wrap:

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```


### Flex Grow and Flex Shrink
The flex-grow and flex-shrink properties are used to define how much the flex items should grow or shrink to fill the
available space. The flex-grow property determines how much the flex item should grow relative to the other flex items
in the container, while the flex-shrink property determines how much the flex item should shrink relative to the other
flex items in the container. Here's an example of how to set the flex-grow property to 1:

```css
.item {
    flex-grow: 1;
}
```

# Flexbox Grid System
A flexbox grid system is a layout system that uses flexbox to create a grid of rows and columns. It provides a simple
way to create responsive layouts that adapt to different screen sizes and device types.

## Creating Rows and Columns

To create rows and columns in the grid, you'll need to use the row and col classes. Here's an example of how to create a
row with three columns:

```html

<div class="row">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
    <div class="col">Column 3</div>
</div>
```
## Responsive Layouts

The flexbox grid system makes it easy to create responsive layouts that adapt to different screen sizes and device
types. To create a responsive layout, you'll need to use the col-xs, col-sm, col-md, and col-lg classes. Here's an
example of how to create a row with two columns that stack on smaller screens:

```html

<div class="row">
    <div class="col-md-6 col-xs-12">Column 1</div>
    <div class="col-md-6 col-xs-12">Column 2</div>
</div>
```

## Offsetting Columns

You can also offset columns in the grid using the offset class. Here's an example of how to create a row with two
columns, where the second column is offset by one column:

```html

<div class="row">
    <div class="col">Column 1</div>
    <div class="col offset">Column 2</div>
</div>
```
# CSS Grid System

CSS Grid is a layout system that allows you to create complex grid layouts with a few lines of code. In this README,
we'll explain how to use CSS Grid to create a responsive grid system for your website.

## Creating the Grid

To create a grid with CSS Grid, you'll need to use the display: grid property on the container element. Here's an
example:

```html

<div class="grid-container">
    <div class="grid-item">Item 1</div>
    <div class="grid-item">Item 2</div>
    <div class="grid-item">Item 3</div>
    <div class="grid-item">Item 4</div>
</div>
``` 

In this example, we're using a div element as the container for our grid. We're also using div elements with a class of
grid-item as the individual items in the grid.

To create the grid, we'll add the following styles to the container element:

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 1em;
}
```

In this example, we're using the grid-template-columns property to create a grid with four columns that are evenly
spaced. We're also using the grid-gap property to add a 1em gap between each item in the grid.

## Responsive Grids

CSS Grid also makes it easy to create responsive grids that adapt to different screen sizes and device types. To create
a responsive grid, you'll need to use the @media rule to apply different styles based on the screen size. Here's an
example:

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 1em;
}

@media screen and (max-width: 768px) {
    .grid-container {
        grid-template-columns: repeat(2, 1fr);
    }
}
``` 

We're using the @media rule to apply a different grid-template-columns property when the screen size is
768px or smaller. This will create a grid with two columns instead of four on smaller screens.