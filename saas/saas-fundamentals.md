# Sass fundamentals

## SAAS

Sass (Syntactically Awesome Style Sheets) is a CSS preprocessor that extends the syntax of CSS and adds
powerful features like nesting, variables, and mixins.

## Sass Syntax

Sass syntax is similar to CSS syntax, but it includes a few additional features. One of the most important features of
Sass is the ability to use variables

This is a quite simple but helpful feature that will help us to keep our code clean and improve code readability
Also to keep our design with good guidelines 

```sass
$
primary-color: #f00

;

body {
    background-color: $ primary-color;
}
``` 

the $primary-color variable to set the background color of the body element. This allows us
to easily change the color throughout our stylesheet by updating the variable when necessary.

## Nesting

Sass also allows you to nest CSS rules inside of one another, which can make your code more readable and easier to
maintain.

```sass
nav {

ul {

li {
    display: inline-block;
}

}
}
```

Here We're nesting the li rule inside the ul rule, and the ul rule inside the nav rule. This makes it clear
that the li rule only applies to the ul element inside the nav element.

## Selectors

Sass also includes a variety of selectors that allow you to target specific elements in your HTML. One of the most
powerful selectors is the & selector, which allows you to create nested selectors that inherit properties from their
parent selectors

```css
button {
    background-color: #f00;

&
:hover {
    background-color: #00f;
}

}
```

We're using the & selector to create a nested :hover rule that inherits the background color from the
parent button rule.

## Sass Variables

One of the most important features of Sass is the ability to use variables. Sass variables allow you to define a value
once and use it throughout your stylesheet. 

```sass
$primary-color: #f00;

body {
background-color: $primary-color;
}
```

The $primary-color variable is used to set the background color of the body element. This allows us
to easily change the color throughout our stylesheet by updating the variable.

You can also use Sass variables to define other values, like font sizes, margins, and padding:

```sass
$font-size: 16px;
$margin: 10px;
$padding: 5px;

h1 {
font-size: $font-size;
margin: $margin;
padding: $padding;
}
``` 

Here we're using the $font-size, $margin, and $padding variables to set the font size, margin, and padding
of the h1 element. This allows us to easily update these values throughout our stylesheet by updating the variables.

You can also perform calculations with Sass variables:

```sass
$base-font-size: 16px;
$line-height: 1.5;
$heading-font-size: $base-font-size * 1.5;

h1 {
font-size: $heading-font-size;
line-height: $line-height;
}
```

## Sass Mixins

Sass mixins are a way to group CSS declarations and reuse them throughout your stylesheet. 

```sass
@mixin border-radius($radius) {
-webkit-border-radius: $radius;
-moz-border-radius: $radius;
border-radius: $radius;
}

.box {
@include border-radius(10px);
}
``` 

Sass mixins can also take multiple parameters:

```sass
@mixin box-shadow($x, $y, $blur, $color) {
-webkit-box-shadow: $x $y $blur $color;
-moz-box-shadow: $x $y $blur $color;
box-shadow: $x $y $blur $color;
}

.box {
@include box-shadow(2px, 2px, 5px, #000);
}
``` 

## Sass Functions

Sass functions are a way to write reusable pieces of code that return a value. 

```sass
@function em($px, $base-font-size: 16px) {

@return
(
$px
/
$base-font-size
)
*

1

em

;
}

.box {
font-size: em(24px);
}
```
### Multiple Parameters

Sass functions can also take multiple parameters:

```sass
@function percentage($value, $total) {

@return
(
$value
/
$total
)
*

100%

;
}

.box {
width: percentage(250px, 500px);
}
```

## Control Flow

Sass control flow directives allow you to write conditional and iterative code in your stylesheet.

### @if Directive

The @if directive allows you to write conditional code based on a boolean expression. 

```sass
$color: red;

@if $color == red {

.box {
background-color: $color;
}
}
``` 

### @else Directive

The @else directive allows you to write alternative code for an @if directive. 

```sass
$color: blue;

@if $color == red {

.box {
background-color: $color;
}
}
@else
{
.box {
background-color: #fff;
}
}
``` 

### @for Directive

The @for directive allows you to write iterative code. 

```sass
@for $i from 1 through 3 {

.box-#{$i} {
width: 100px;
height: 100px;
background-color:blue;

float:left;

}
}
``` 

### @each Directive

The @each directive allows you to iterate over a list or a map. 

```sass
$colors: red, blue, green;

@each $color in $colors {

.box-#{$color} {
background-color: $color;
}
}
``` 

## Data Structures

Sass provides several data structures to help you organize your code.

### Lists

Lists are ordered collections of values. 

```sass
$colors: red, blue, green;
```

You can access individual items in a list using the nth function:

```sass
$color: nth($colors, 2);
``` 

### Maps

Maps are collections of key-value pairs. 

```sass
$colors: (
primary: #007bff,
secondary: #6c757d
)
``` 

## BEM

BEM stands for Block, Element, Modifier. It is a naming convention for CSS classes that helps you write modular and
reusable code.

### Block

A block is a standalone entity that represents a reusable component in your UI. A block has a descriptive name that
defines its purpose. For example, a navigation menu, a button, or a card can be considered blocks.

In BEM, block names are written in lowercase and separated by a hyphen. For example:

```css
.nav-menu {
}

.btn {
}

.card {
}
```

### Element

An element is a part of a block that performs a specific function. Elements are always tied to a block and should not be
used outside of it.

In BEM, element names are written after the block name and separated by a double underscore. For example:

```css
.nav-menu__item {
}

.btn__label {
}

.card__title {
}
``` 

### Modifier

A modifier is a variation of a block or an element. Modifiers are used to change the appearance or behavior of a block
or an element without duplicating the code.

In BEM, modifier names are written after the block or element name and separated by a double dash. For example:

```css
.btn--primary {
}

.card__title--large {
}

.nav-menu__item--active {
}
``` 

Modifiers can be combined to create more complex variations. For example:


```css
.btn--primary.btn--large {
    width: "90000px";
}
```
