# Intro

## Store Data with Sass Variables

- One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.

- In JavaScript, variables are defined using the let and const keywords. In Sass, variables start with a `$ followed by the variable name`.

Here are a couple examples:

```css
$main-fonts: Arial, sans-serif;
$headings-color: green;

//To use variables:
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}
```

## Nest CSS with Sass

- Sass allows nesting of CSS rules, which is a useful way of organizing a style sheet.

- Normally, each element is targeted on a different line to style it, like so:

```css
nav {
  background-color: red;
}

nav ul {
  list-style: none;
}

nav ul li {
  display: inline-block;
}
```

- For a large project, the CSS file will have many lines and rules. This is where nesting can help organize your code by placing child style rules within the respective parent elements:

```css
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}
```

## Create Reusable CSS with Mixins

- In Sass, a mixin is a group of CSS declarations that can be reused throughout the style sheet.

- Newer CSS features take time before they are fully adopted and ready to use in all browsers. As features are added to browsers, CSS rules using them may need vendor prefixes. Consider "box-shadow":

```css
div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
```

- It's a lot of typing to re-write this rule for all the elements that have a box-shadow, or to change each value to test different effects. Mixins are like functions for CSS. Here is how to write one:

```css
@mixin box-shadow($x, $y, $blur, $c) {
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}
```

- The definition starts with @mixin followed by a custom name. The parameters (the `$x, $y, $blur, and $c` in the example above) are optional. Now any time a box-shadow rule is needed, only a single line calling the mixin replaces having to type all the vendor prefixes. A mixin is called with the @include directive:

```css
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```

## Use @if and @else to Add Logic To Your Styles

- The @if directive in Sass is useful to test for a specific case - it works just like the if statement in JavaScript.

```css
@mixin make-bold($bool) {
  @if $bool == true {
    font-weight: bold;
  }
}
```

- And just like in JavaScript, @else if and @else test for more conditions:

```css
@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  } @else if $val == alert {
    color: yellow;
  } @else if $val == success {
    color: green;
  } @else {
    color: black;
  }
}
```

## Use @for to Create a Sass Loop

- The @for directive adds styles in a loop, very similar to a for loop in JavaScript.

- @for is used in two ways: `start through end` or `start to end`.
- The main difference is that the `start to end` `excludes` the end number as part of the count, and `start through end` `includes` the end number as part of the count.

- Here's a start through end example:

```css
@for $i from 1 through 12 {
  .col-#{$i} {
    width: 100%/12 * $i;
  }
}
```

- The `#{$i}` part is the syntax to combine a variable (i) with text to make a string. When the Sass file is converted to CSS, it looks like this:

```css
.col-1 {
  width: 8.33333%;
}

.col-2 {
  width: 16.66667%;
}

... .col-12 {
  width: 100%;
}
```

- This is a powerful way to create a grid layout. Now you have twelve options for column widths available as CSS classes.

## Use @each to Map Over Items in a List

- The last challenge showed how the @for directive uses a starting and ending value to loop a certain number of times. Sass also offers the @each directive which loops over each item in a list or map. On each iteration, the variable gets assigned to the current value from the list or map.

```css
@each $color in blue, red, green {
  .#{$color}-text {
    color: $color;
  }
}
```

- A map has slightly different syntax. Here's an example:

```css
$colors: (
  color1: blue,
  color2: red,
  color3: green,
);

@each $key, $color in $colors {
  .#{$color}-text {
    color: $color;
  }
}
```

- Note that the `$key` variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have color1, color2... in it. Both of the above code examples are converted into the following CSS:

```css
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
```

- Write an @each directive that goes through a list: blue, black, red and assigns each variable to a .color-bg class, where the "color" part changes for each item. Each class should set the background-color the respective color.

```css
<style type='text/scss'>

@each $color in blue, black, red{
  .#{$color}-bg{
    background-color:$color;
  }
}

  div {
    height: 200px;
    width: 200px;
  }
</style>

<div class="blue-bg"></div>
<div class="black-bg"></div>
<div class="red-bg"></div>
```

## Apply a Style Until a Condition is Met with @while

- The `@while` directive is an option with similar functionality to the JavaScript while loop. It creates CSS rules until a condition is met.

- The @for challenge gave an example to create a simple grid system. This can also work with @while.

```css
$x: 1;
@while $x < 13 {
  .col-#{$x} {
    width: 100%/12 * $x;
  }
  $x: $x + 1;
}
```

- First, define a variable `$x` and set it to 1. Next, use the @while directive to create the grid system while $x is less than 13. After setting the CSS rule for width, $x is incremented by 1 to avoid an infinite loop.

- Use @while to create a series of classes with different font-sizes.

- There should be 5 different classes from text-1 to text-5. Then set font-size to 15px multiplied by the current index number. Make sure to avoid an infinite loop!

```css
<style type='text/scss'>

$x : 1;
@while $x <= 5{
  .text-#{$x}{
    font-size: $x * 15
  }
  $x : $x + 1;
}

</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>
```

## Extend One Set of CSS Styles to Another Element

- Sass has a feature called extend that makes it easy to borrow the CSS rules from one element and build upon them in another.

- For example, the below block of CSS rules style a .panel class. It has a background-color, height and border.

```css
.panel {
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
```

- Now you want another panel called .big-panel. It has the same base properties as .panel, but also needs a width and font-size. It's possible to copy and paste the initial CSS rules from .panel, but the code becomes repetitive as you add more types of panels. The extend directive is a simple way to reuse the rules written for one element, then add more for another:

```css
.big-panel {
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```

- The .big-panel will have the same properties as .panel in addition to the new styles.
