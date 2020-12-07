# Intro

# Use Hex Code for Specific Colors

- Did you know there are other ways to represent colors in CSS? One of these ways is called hexadecimal code, or hex code for short.

  - We usually use `decimals`, or base 10 numbers, which use the symbols 0 to 9 for each digit. `Hexadecimals` (or hex) are base 16 numbers.
  - This means it uses `sixteen distinct symbols`. Like decimals, the symbols `0-9` represent the values zero to nine. Then `A,B,C,D,E,F` represent the values ten to fifteen. Altogether, `0 to F` can represent a digit in hexadecimal, giving us 16 total possible values. You can find more information about hexadecimal numbers here.

- Hex codes use `6` hexadecimal digits to represent colors, two each for red (R), green (G), and blue (B) components.
- From these three pure colors (red, green, and blue), we can vary the amounts of each to create over `16 million other colors`!
- In `CSS`, we can use `6 hexadecimal digits` to represent colors, two each for the red (R), green (G), and blue (B) components. For example, #000000 is black and is also the lowest possible value.
  - The digit `0` is the `lowest` number in hex code, and represents a complete `absence of color`.
  - The digit `F` is the `highest` number in hex code, and represents the maximum possible `brightness`.

# Use RGB values to Color Elements

- Instead of using six hexadecimal digits like you do with hex code, with RGB you specify the brightness of each color with a number between `0 and 255`.

- If you do the math, the two digits for one color equal 16 times 16, which gives us 256 total values. So RGB, which starts counting from zero, has the exact same number of possible values as hex code.
- rgba stands for:
  - `r` = red
  - `g` = green
  - `b` = blue
  - `a` = alpha/level of opacity

# Gradual CSS Linear Gradient

- The first argument specifies the direction from which color transition starts - it can be stated as a degree, where 90deg makes a horizontal gradient `(from left to right)` and 45deg makes a diagonal gradient `(from bottom left to top right)`. The following arguments specify the order of colors used in the gradient.

```css
background: linear-gradient(90deg, red, yellow, rgb(204, 204, 255));
```

- The `repeating-linear-gradient()` function is very similar to linear-gradient() with the major difference that it repeats the specified gradient pattern
  - In the example demonstrated in the code editor, the gradient starts with the color yellow at 0 pixels which blends into the second color blue at 40 pixels away from the start. Since the next color stop is also at 40 pixels, the gradient immediately changes to the third color green, which itself blends into the fourth color value red as that is 80 pixels away from the beginning of the gradient.
  - `0px [yellow -- blend -- blue] 40px [green -- blend -- red] 80px`

# Box shadow

- The box-shadow property takes values for in the order:
  - offset-x (how far to push the shadow horizontally from the element),
  - offset-y (how far to push the shadow vertically from the element),
  - blur-radius, spread-radius
  - color.
- Multiple box-shadows can be created by using commas to separate properties of each box-shadow element.

```css
box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
```

# Text transform

- lowercase: "transform me"
- uppercase: "TRANSFORM ME"
- capitalize: "Transform Me"
- initial: Use the default value
- inherit: Use the text-transform value from the parent element
- none: Default: Use the original text

# Positions

## Position: static;

HTML elements are positioned static by default.

Static positioned elements are not affected by the top, bottom, left, and right properties.

An element with position: static; is not positioned in any special way; it is always positioned according to the normal flow of the page:

This <div> element has position: static;
Here is the CSS that is used:

Example

```css
div.static {
  position: static;
  border: 3px solid #73ad21;
}
```

## Position: relative;

An element with position: relative; is positioned relative to its normal position.

Setting the top, right, bottom, and left properties of a relatively-positioned element will cause it to be adjusted away from its normal position. Other content will not be adjusted to fit into any gap left by the element.

This <div> element has position: relative;
Here is the CSS that is used:

Example

```css
div.relative {
  position: relative;
  left: 30px;
  border: 3px solid #73ad21;
}
```

## Position: fixed;

An element with position: fixed; is positioned relative to the `viewport`, which means it always stays in the same place even if the page is scrolled. The top, right, bottom, and left properties are used to position the element.

A fixed element does not leave a gap in the page where it would normally have been located.

Notice the fixed element in the lower-right corner of the page. Here is the CSS that is used:

Example

```css
div.fixed {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 300px;
  border: 3px solid #73ad21;
}
```

## Position: absolute;

An element with position: absolute; is positioned relative to the `nearest positioned ancestor` (instead of positioned relative to the viewport, like fixed).

However; if an absolute positioned element has no positioned ancestors, it uses the document body, and moves along with page scrolling.

Note: A "positioned" element is one whose position is anything except static.

Here is a simple example:

This <div> element has position: relative;This <div> element has position: absolute;
Here is the CSS that is used:

```css
div.relative {
  position: relative;
  width: 400px;
  height: 200px;
  border: 3px solid #73ad21;
}

div.absolute {
  position: absolute;
  top: 80px;
  right: 0;
  width: 200px;
  height: 100px;
  border: 3px solid #73ad21;
}
```

## Position: sticky;

An element with position: sticky; is positioned based on the user's `scroll position`.

A sticky element toggles between relative and fixed, depending on the scroll position. It is positioned relative until a given offset position is met in the viewport - then it "sticks" in place (like position:fixed).
Note: Internet Explorer does not support sticky positioning. Safari requires a -webkit- prefix (see example below). You must also specify at least one of top, right, bottom or left for sticky positioning to work.

In this example, the sticky element sticks to the top of the page (top: 0), when you reach its scroll position.

Example

```css
div.sticky {
  position: -webkit-sticky; /* Safari */
  position: sticky;
  top: 0;
  background-color: green;
  border: 2px solid #4caf50;
}
```

## Overlapping Elements

When elements are positioned, they can overlap other elements.

The z-index property specifies the stack order of an element (which element should be placed in front of, or behind, the others).

An element can have a positive or negative stack order:

This is a headingBecause the image has a `z-index` of -1, it will be placed behind the text.
Example

```css
img {
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: -1;
}
```

## Positions for images

- Top left: https://www.w3schools.com/css/tryit.asp?filename=trycss_image_text_top_left
- Top right
- Bottom left
- Bottom right
- Center: https://www.w3schools.com/css/tryit.asp?filename=trycss_image_text_center

## Float

- Floating elements are removed from the normal flow of a document and pushed to either the left or right of `their containing parent element`.
- It's commonly used with the width property to specify how much horizontal space the floated element requires.

## Margin

- Center an Element Horizontally Using the margin Property
  - Set its margin to a value of `auto`.
  - This method works for images, too. Images are inline elements by default, but can be changed to block elements when you set the display property to block.

## Reference:

- Positions: https://www.w3schools.com/css/css_positioning.asp

# Transform

## ::before and ::after pseudo-elements

- These pseudo-elements are used to add something `before or after` a selected element

```css
.heart::before {
  content: "";
  background-color: yellow;
  border-radius: 25%;
  position: absolute;
  height: 50px;
  width: 70px;
  top: -50px;
  left: 5px;
}
```

- For the `::before` and `::after` pseudo-elements to function properly, they must have a defined `content` property
- When the ::before and ::after pseudo-elements are used to make shapes, the content property is still `required`, but it's set to an empty string

## CSS @keyframes and animation Properties Work

- The animation properties control how the animation should behave and the @keyframes rule controls what happens during that animation.
- There are eight animation properties in total.
- `animation-name` sets the name of the animation, which is later used by `@keyframes` to tell CSS which rules go with which animations.
- `animation-duration` sets the length of time for the animation.
- `@keyframes` is how to specify exactly what happens within the animation over the duration. This is done by giving CSS properties for specific "frames" during the animation, with percentages ranging from `0% to 100%`.

```css
#anim {
  animation-name: colorful;
  animation-duration: 3s;
}

@keyframes colorful {
  0% {
    background-color: blue;
  }
  100% {
    background-color: yellow;
  }
}
```

- For the element with the anim id, the code snippet above sets the animation-name to colorful and sets the animation-duration to 3 seconds.
- Then the @keyframes rule links to the animation properties with the name colorful. It sets the color to blue at the beginning of the animation (0%) which will transition to yellow by the end of the animation (100%).
- You aren't limited to only beginning-end transitions, you can set properties for the element for any percentage between 0% and 100%.

## animation-fill-mode with forwards

- Notice how the animation resets after 500ms has passed, causing the button to revert back to the original color. You want the button to stay highlighted.

- This can be done by setting the `animation-fill-mode` property to `forwards`. The animation-fill-mode specifies the style applied to an element when the animation has finished. You can set it like so:

```css
animation-fill-mode: forwards;
```

- Set the `animation-fill-mode` property of button:hover to forwards so the button stays highlighted when a user hovers over it.

## Animate Elements Continually Using an Infinite Animation Count

- Animate Elements Continually Using an `Infinite Animation Count`

```css
animation-iteration-count: 3;
```

- In this case the animation will stop after running `3` times, but it's possible to make the animation run continuously by setting that value to infinite.
- To keep the ball bouncing on the right on a continuous loop, change the animation-iteration-count property to `infinite`.

## Use the CSS Transform scale Property to Change the Size of an Element

- To change the scale of an element, CSS has the transform property, along with its `scale()` function.
- The following code example doubles the size of all the paragraph elements on the page:

```css
p {
  transform: scale(2);
}
```

## Change Animation Timing with Keywords

- The default value is `ease`, which starts `slow`, speeds up in the middle, and then slows down again in the end.
- Other options include `ease-out`, which is quick in the beginning then slows down
- `ease-in`, which is slow in the beginning, then speeds up at the end, or linear, which applies a constant animation speed throughout.

## Use the CSS Transform scale Property to Scale an Element on Hover

- The transform property has a variety of functions that let you scale, move, rotate, skew, etc., your elements. When used with pseudo-classes such as :hover that specify a certain state of an element, the transform property can easily add interactivity to your elements.

```css
p:hover {
  transform: scale(2.1);
}
```

- `Note`: Applying a transform to a div element will also affect any child elements contained in the div.

## How Bezier Curves Work

- Bezier curves are used with the cubic-bezier function.
- The shape of the curve represents how the animation plays out. The curve lives on a 1 by 1 coordinate system.
- The `X-axis` of this coordinate system is the duration of the animation (think of it as a time scale), and the `Y-axis` is the change in the animation.
- The `cubic-bezier` function consists of four main points that sit on this `1 by 1 grid`: `p0, p1, p2, and p3`.
  - p0 and p3 are set for you - they are the beginning and end points which are always located respectively at the origin (0, 0) and (1, 1).
  - You set the `x and y` values for the other two points, and where you place them in the grid dictates the shape of the curve for the animation to follow.
  - This is done in CSS by declaring the x and y values of the p1 and p2 "anchor" points in the form: `(x1, y1, x2, y2)`. Pulling it all together, here's an example of a Bezier curve in CSS code:
  ```css
  animation-timing-function: cubic-bezier(0.25, 0.25, 0.75, 0.75);
  ```
  - In the example above, the x and y values are equivalent for each point (x1 = 0.25 = y1 and x2 = 0.75 = y2), which if you remember from geometry class, results in a line that extends from the origin to point (1, 1).
  - This animation is a linear change of an element during the length of an animation, and is the same as using the linear keyword. In other words, it changes at a constant speed.

## Use the CSS Transform Property skewX to Skew an Element Along the X-Axis, skewY to Skew an Element Along the Y-Axis

- Property is `skewX()`, which skews the selected element along its X (horizontal) axis by a given degree.
- `skewY()` property skews an element along the Y (vertical) axis.

```css
p {
  transform: skewX(-32deg);
  transform: skewX(32deg);
}
```

# Flexbox

## Use the flex-direction Property to Make a Row

- Adding `display: flex` to an element turns it into a flex `container`
- This makes it possible to align any children of that element into `rows` or `columns`.
- You do this by adding the `flex-direction` property to the parent item and setting it to `row or column`.
- Creating a `row` will align the children `horizontally`, and creating a `column` will align the children `vertically`.
- Other options for flex-direction are:
  - row-reverse: invert the order of row direction
  - column-reverse: invert the order of column direction
- `Note`: The default value for the flex-direction property is row.

## Align Elements Using the justify-content Property

- Flex direction terms: https://www.w3.org/TR/css-flexbox-1/images/flex-direction-terms.svg
- Recall that setting a flex container as a row places the flex items side-by-side from left-to-right.
- A flex container set as a column places the flex items in a `vertical` stack from `top-to-bottom`. For each, the direction the flex items are arranged is called the `main axis` . For a row, this is a horizontal line that cuts through each item. And for a column, the main axis is a vertical line through the items.

- There are several options for how to space the flex items along the line that is the `main axis`.
- One of the most commonly used is `justify-content: center;`, which aligns all the flex items to the center inside the flex container. Others options include:
  - **flex-start**: aligns items to the start of the flex container. For a row, this pushes the items to the `left of the container`. For a `column`, this pushes the items to the `top` of the container. This is the `default alignment` if no justify-content is specified.
  - **flex-end**: aligns items to the end of the flex container. For a row, this pushes the items to the `right of the container`. For a `column`, this pushes the items to the `bottom`of the container.
  - **space-between**: aligns items to the `center` of the `main axis`, with extra `space` placed between the items. The `first` and `last` items are pushed to the very `edge` of the flex container. For example, in a row the `first` item is against the `left` side of the container, the `last` item is against the `right` side of the container, then the `remaining` space is distributed `evenly` among the other items.
  - **space-around**: similar to `space-between` but the `first` and `last` items are `not` locked to the edges of the container, the space is distributed around all the items with a half space on either end of the flex container.
  - **space-evenly**: Distributes space evenly between the flex items with a full space at either end of the flex container

## Align Elements Using the align-items Property

- The `align-items` property is similar to `justify-content`. Recall that the justify-content property aligned flex items along the main axis. For rows, the main axis is a horizontal line and for columns it is a vertical line.

- Flex containers also have a `cross axis` which is the `opposite` of the `main axis`. For rows, the cross axis is vertical and for columns, the cross axis is horizontal.

- CSS offers the `align-items` property to `align` flex items along the `cross axis`.

  - For a `row`, it tells CSS how to push the items in the entire `row up or down` within the `container`.
  - And for a `column`, how to push all the items `left or right` within the `container`.

- The different values available for align-items include:
  - **flex-start**: aligns items to the start of the flex container.
    - For `rows`, this aligns items to the top of the container.
    - For `columns`, this aligns items to the left of the container.
  - **flex-end**: aligns items to the end of the flex container.
    - For `rows`, this aligns items to the `bottom` of the container.
    - For `columns`, this aligns items to the `right` of the container.
  - **center**: align items to the center.
    - For `rows`, this vertically aligns items `(equal space above and below the items)`.
    - For `columns`, this horizontally aligns them `(equal space to the left and right of the items)`.
  - **stretch**: stretch the items to fill the flex container. For example, rows items are stretched to fill the flex container top-to-bottom. This is the `default` value if no align-items value is specified.
  - **baseline**: align items to their baselines. Baseline is a text concept, think of it as the line that the letters sit on.

## Use the flex-wrap Property to Wrap a Row or Column

- CSS flexbox has a feature to split a flex item into multiple rows (or columns). By default, a flex container will fit all flex items together. For example, a row will all be on one line.

- However, using the `flex-wrap` property tells CSS to `wrap` items. This means extra items move into a new row or column. The `break point` of where the wrapping happens `depends` on the `size` of the `items` and the size of the `container`.

- CSS also has options for the direction of the wrap:
  - **nowrap**: this is the default setting, and does not wrap items.
  - **wrap**:
    - `wraps` items from `left-to-right` if they are in a `row`
    - or `top-to-bottom` if they are in a column.
  - **wrap-reverse**:
    - wraps items from right-to-left if they are in a row
    - or bottom-to-top if they are in a column.

## Use the flex-shrink Property to Shrink Items

- When it's used, it allows an item to `shrink` if the flex container is too `small`.
- Items shrink when the `width` of the `parent container` is `smaller` than the combined` widths of all the flex items` within it.
- The `flex-shrink` property takes `numbers as values`.
- The `higher` the number, the `more` it will shrink compared to the other items in the container. For example, if one item has a flex-shrink value of 1 and the other has a flex-shrink value of 3, the one with the value of 3 will shrink three times as much as the other.

## Use the flex-grow Property to Expand Items

- The `opposite` of flex-shrink is the `flex-grow` property. Recall that flex-shrink controls the size of the items when the container shrinks. The flex-grow property controls the size of items when the parent container expands.

- Using a similar example from the last challenge, if one item has a flex-grow value of 1 and the other has a flex-grow value of 3, the one with the value of 3 will grow three times as much as the other.

## Use the flex-basis Property to Set the Initial Size of an Item

- The `flex-basis` property specifies the `initial size` of the item before CSS makes adjustments with flex-shrink or flex-grow.

- The units used by the flex-basis property are the same as other size properties (px, em, %, etc.). The value auto sizes items based on the content.

## Use the flex Shorthand Property

- There is a shortcut available to set several flex properties at once.
- The `flex-grow, flex-shrink, and flex-basis` properties can all be set together by using the flex property.

- For example, `flex: 1 0 10px;` will set the item to flex-grow: 1;, flex-shrink: 0;, and flex-basis: 10px;.

  - The `default` property settings are flex: 0 1 auto;.

- Add the CSS property flex to both #box-1 and #box-2. Give #box-1 the values so its flex-grow is 2, its flex-shrink is 2, and its flex-basis is 150px. Give #box-2 the values so its flex-grow is 1, its flex-shrink is 1, and its flex-basis is 150px.
- These values will cause #box-1 to grow to fill the extra space at twice the rate of #box-2 when the container is greater than 300px and shrink at twice the rate of #box-2 when the container is less than 300px. 300px is the combined size of the flex-basis values of the two boxes.

```html
<style>
  #box-container {
    display: flex;
    height: 500px;
  }
  #box-1 {
    background-color: dodgerblue;
    flex: 2 2 150px;
    height: 200px;
  }

  #box-2 {
    background-color: orangered;
    flex: 1 1 150px;
    height: 200px;
  }
</style>

<div id="box-container">
  <div id="box-1"></div>
  <div id="box-2"></div>
</div>
```

## Use the order Property to Rearrange Items

- The order property is used to tell CSS the order of how flex items appear in the flex container.
- By default, items will appear in the same order they come in the source HTML. The property takes numbers as values, and negative numbers can be used.

```html
<style>
  #box-container {
    display: flex;
    height: 500px;
  }
  #box-1 {
    background-color: dodgerblue;
    order: 2;
    height: 200px;
    width: 200px;
  }

  #box-2 {
    background-color: orangered;
    order: 1;
    height: 200px;
    width: 200px;
  }
</style>

<div id="box-container">
  <div id="box-1"></div>
  <div id="box-2"></div>
</div>
```

# Grid

- Turn any HTML element into a grid container by setting its display property to grid. This gives you the ability to use all the other properties associated with CSS Grid.

- Note: In CSS Grid, the parent element is referred to as the container and its children are called items.
## Add Columns with grid-template-columns
- Define the structure of the grid by adding some columns to the grid, use the `grid-template-columns` property on a grid container as demonstrated below:
```css
.container {
  display: grid;
  grid-template-columns: 50px 50px;
}
```

- This will give your grid `two columns` that are `each 50px wide`.
- The number of parameters given to the grid-template-columns property indicates the number of columns in the grid, and the value of each parameter indicates the width of each column.

## Add Rows with grid-template-rows
- The grid you created in the last challenge will set the number of rows automatically. To adjust the rows manually, use the `grid-template-rows` property

## Use CSS Grid units to Change the Size of Columns and Rows
- You can use `absolute and relative` units like px and em in CSS Grid to define the size of rows and columns. You can use these as well:
  - `fr`: sets the column or row to a fraction of the available space,
  - `auto`: sets the column or row to the width or height of its content automatically,
  - `%`: adjusts the column or row to the percent width of its container.

- Here's the code that generates the output in the preview:
  - `grid-template-columns: auto 50px 10% 2fr 1fr`;
  - This snippet creates `five` columns.
    - The `first` column is as wide as its content
    - the `second` column is 50px
    - the `third` column is 10% of its container
    - for the `last two` columns; the remaining space is divided into three sections, two are allocated for the fourth column, and one for the fifth.

## Create a Column Gap Using grid-column-gap
- The columns have all been tight up against each other. Sometimes you want a gap in between the columns. To add a gap between the columns, use the grid-column-gap property like this:`grid-column-gap: 10px;`
- This creates `10px of empty space` between `all` of our columns.

## Create a Row Gap using grid-row-gap
- You can add a gap in between the rows of a grid using `grid-row-gap`

## Add Gaps Faster with grid-gap
- `grid-gap` is a shorthand property for `grid-row-gap` and `grid-column-gap` from the previous two challenges that's more convenient to use.
- If grid-gap has `one` value, it will create a `gap` between `all rows and columns`.
- However, if there are `two` values, it will use the `first` one to set the gap between the `rows` and the `second` value for the `columns`.
```css
grid-gap: 10px 20px;
```
## Use grid-column/grid-row to Control Spacing
- The hypothetical `horizontal and vertical` lines that create the grid are referred to as `lines`.
- These lines are numbered starting with `1` at the `top left corner` of the grid and `move right` for `columns` and `down` for `rows`, counting `upward`.

- This is what the lines look like for a 3x3 grid:
  - https://www.freecodecamp.org/learn/responsive-web-design/css-grid/use-grid-column-to-control-spacing

- To control the amount of columns an item will consume, you can use the `grid-column` property in `conjunction` with `the line numbers` you want the item to start and stop at.

- Here's an example:
  - `grid-column: 1 / 3`;
  - This will make the item `start` at the `first vertical line` of the grid on the `left` and span to the `3rd line` of the grid, consuming two columns.

## Align an Item Horizontally using justify-self
- In CSS Grid, the content of each item is located in a box which is referred to as a `cell`.
- You can `align` the content's position within its cell `horizontally` using the `justify-self` property on a grid item.
- By default, this property has a `value of stretch`, which will make the content `fill the whole width of the cell`. This CSS Grid property accepts other values as well:
  - `start`: aligns the content at the left of the cell,
  - `center`: aligns the content in the center of the cell,
  - `end`: aligns the content at the right of the cell.

## Align an Item Vertically using align-self
- Just as you can align an item `horizontally`, there's a way to align an item vertically as well.
- To do this, you use the `align-self` property on an item.
- This property accepts all of the same values as `justify-self` from the last challenge.

## Align All Items Horizontally using justify-items
- Sometimes you want all the items in your CSS Grid to share the same alignment.
- You can use the previously learned properties and align them individually, or you can align them all at once horizontally by using `justify-items` on your grid container. 
- This property can accept all the same values you learned about in the previous two challenges, the difference being that it will `move all the items` in our grid to the desired alignment.
```css
justify-items:center;
```
## Divide the Grid Into an Area Template
- You can group cells of your grid together into an area and give the area a custom name. Do this by `using grid-template-areas` on the container like this:
  - grid-template-areas:
    - "header header header"
    - "advert content content"
    - "footer footer footer";
- The code above merges the top three cells together into an area named header, the bottom three cells into a footer area, and it makes two areas in the middle row; advert and content.
- **Note**: Every word in the code represents a cell and every pair of quotation marks represent a row. In addition to custom labels, you can use a period (.) to designate an empty cell in the grid.

## Align All Items Vertically using align-items
- Using the `align-items` property on a grid container will set the `vertical alignment` for all the items in our grid.

## Place Items in Grid Areas Using the grid-area Property
- After creating an area's template for your grid container, you can place an item in your custom area by referencing the name you gave it. To do this, you use the grid-area property on an item like this:
```css
.item1 {
  grid-area: header;
}
```
- This lets the grid know that you want the item1 class to go in the area named header. In this case, the item will use the entire top row because that whole row is named as the header area.

## Use grid-area Without Creating an Areas Template
- The grid-area property you learned in the last challenge can be used in another way. If your grid doesn't have an areas template to reference, you can create an area on the fly for an item to be placed like this:
```css
.item1 { grid-area: 1/1/2/4; }
```
- This is using the line numbers you learned about earlier to define where the area for this item will be. The numbers in the example above represent these values:
```css
grid-area: horizontal line to start at / vertical line to start at / horizontal line to end at / vertical line to end at;
```

## Reduce Repetition Using the repeat Function
- When you used grid-template-columns and grid-template-rows to define the structure of a grid, you entered a value for each row or column you created.

- Let's say you want a grid with 100 rows of the same height. It isn't very practical to insert 100 values individually. Fortunately, there's a better way - by using the repeat function to specify the number of times you want your column or row to be repeated, followed by a comma and the value you want to repeat.

- Here's an example that would create the 100 row grid, each row at 50px tall.
```css
grid-template-rows: repeat(100, 50px);
```
- You can also repeat multiple values with the repeat function and insert the function amongst other values when defining a grid structure. Here's what that looks like:

```css
grid-template-columns: repeat(2, 1fr 50px) 20px;
```
This translates to:
```css
grid-template-columns: 1fr 50px 1fr 50px 20px;
```
- **Note**: The 1fr 50px is repeated `twice` followed by `20px`.

## Limit Item Size Using the minmax Function
- There's another built-in function to use with grid-template-columns and grid-template-rows called `minmax`.
- It's used to limit the size of items when the grid container changes size. To do this you need to specify the acceptable size range for your item. Here is an example:
```css
grid-template-columns: 100px minmax(50px, 200px);
```
In the code above, grid-template-columns is set to create two columns; the first is 100px wide, and the second has the minimum width of 50px and the maximum width of 200px.

## Create Flexible Layouts Using auto-fill
- The repeat function comes with an option called auto-fill. This allows you to automatically insert as many rows or columns of your desired size as possible depending on the size of the container. You can create flexible layouts when combining auto-fill with minmax, like this:
```css
repeat(auto-fill, minmax(60px, 1fr));
```
- When the container changes size, this setup keeps inserting 60px columns and stretching them until it can insert another one.
- **Note**: If your container `can't` fit all your items on one row, it will `move them down to a new one`.

## Create Flexible Layouts Using auto-fit
- `auto-fit` works almost `identically` to `auto-fill`.
- The only difference is that when the container's size `exceeds` the size of all the items combined, `auto-fill` keeps inserting empty rows or columns and pushes your items to the side, while `auto-fit collapses` those empty rows or columns and stretches your items to fit the size of the container.

- **Note**: If your container can't fit all your items on one row, it will move them down to a new one.

## Use Media Queries to Create Responsive LayoutsPassed
- CSS Grid can be an easy way to make your site more responsive by using media queries to rearrange grid areas, change dimensions of a grid, and rearrange the placement of items.

- In the preview, when the viewport width is 300px or more, the number of columns changes from 1 to 2. The advertisement area then occupies the left column completely.
```html
<style>
  .item1 {
    background: LightSkyBlue;
    grid-area: header;
  }

  .item2 {
    background: LightSalmon;
    grid-area: advert;
  }

  .item3 {
    background: PaleTurquoise;
    grid-area: content;
  }

  .item4 {
    background: lightpink;
    grid-area: footer;
  }

  .container {
    font-size: 1.5em;
    min-height: 300px;
    width: 100%;
    background: LightGray;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 50px auto 1fr auto;
    grid-gap: 10px;
    grid-template-areas:
      "header"
      "advert"
      "content"
      "footer";
  }

  @media (min-width: 300px){
    .container{
      grid-template-columns: auto 1fr;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "advert header"
        "advert content"
        "advert footer";
    }
  }

  @media (min-width: 400px){
    .container{
      grid-template-areas:
      /* Only change code below this line */
        "advert header"
        "advert content"
        "advert footer";
      /* Only change code above this line */
    }
  }
</style>

<div class="container">
  <div class="item1">header</div>
  <div class="item2">advert</div>
  <div class="item3">content</div>
  <div class="item4">footer</div>
</div>

```
## Create Grids within Grids
- Turning an element into a grid only affects the behavior of its direct descendants. So by turning a direct descendant into a grid, you have a grid within a grid.

- For example, by setting the display and grid-template-columns properties of the element with the item3 class, you create a grid within your grid.
# Flexbox vs Grid

## Grid is `Container-Based`, Flexbox is `Content-Based`

- the size of a cell `(flex-item)` is defined inside the flex-item itself
- `cell’s size` using grid-template-columns inside the grid-container `(.row)`, not the grid-item
- Flexbox layout is `calculated after` its content is loaded , whereas the grid layout is calculated `regardless` of the content inside it

## Grid Has a `Gap` Property, Flexbox Doesn’t

- In order to achieve the same result in `flexbox` we would have to use `padding` and `nested containers`, or increase the `width` of the flex-container and use the `justify-content` property to spread the flex-items.

## Flexbox is `One Dimensional`, Grid is `Two Dimensional`

- `Flexbox` is best for arranging elements in either a single row, or a single column.

  ```html
  <ul class="social-icons">
    <li>
      <a href="#"><i class="fab fa-facebook-f"></i></a>
    </li>
    <li>
      <a href="#"><i class="fab fa-twitter"></i></a>
    </li>
    <li>
      <a href="#"><i class="fab fa-instagram"></i></a>
    </li>
    <li>
      <a href="#"><i class="fab fa-github"></i></a>
    </li>
    <li>
      <a href="#"><i class="fas fa-envelope"></i></a>
    </li>
    <li>
      <a href="#"><i class="fas fa-rss"></i></a>
    </li>
  </ul>
  ```

  ```css
  .social-icons {
    display: flex;
    list-style: none;
    justify-content: space-around;
  }
  ```

- `Grid` is best for arranging elements in multiple rows and columns.

  ```html
  <div class="container">
    <header>Header</header>
    <main>Main</main>
    <aside>Aside</aside>
    <footer>Footer</footer>
  </div>
  ```

  ```css
  .container {
    max-width: 800px;
    margin: 2em auto;
    display: grid;
    grid-template-columns: 3fr 1fr;
    grid-template-rows: repeat(3, auto);
    grid-gap: 1rem;
  }

  .container header {
    grid-area: 1/1/2/3;
  }

  .container main {
    grid-area: 2/1/3/2;
  }

  .container aside {
    grid-area: 2/2/3/3;
  }

  .container footer {
    grid-area: 3/1/4/3;
  }

  .container > * {
    background-color: #ddd;
    padding: 1rem;
  }
  ```

  - We are creating two columns using the grid-template-columns property, and three rows using grid-template-rows property. The repeat() function creates 3 rows with auto height.

  - Then, inside the grid-items (header, main, aside, and footer) we define how much area those grid-items will cover using the grid-area property.

## Flexbox Wraps vs Grid Wraps

- When the total width of items inside the container is greater than the width of the container, in that case both the layout models have the option to wrap the items to a new row. However, the way both handle wrapping is different.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      /* Flexbox row styles */
      .row-flex {
        margin: 40px auto;
        max-width: 600px;
        display: flex;
        flex-wrap: wrap;
      }

      .row-flex div {
        border: 1px dashed gray;
        flex: 1 1 100px;
        text-align: center;
        padding: 12px;
      }

      /* Grid row styles */
      .row-grid {
        margin: 40px auto;
        max-width: 600px;
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
      }

      .row-grid div {
        border: 1px dashed gray;
        text-align: center;
        padding: 12px;
      }
    </style>
  </head>

  <body>
    <h2>Flexbox</h2>
    <div class="row-flex">
      <div>1 2 3 4 5 6 7 8 9 0</div>
      <div>2</div>
      <div>3</div>
      <div>4</div>
      <div>5</div>
      <div>6</div>
    </div>

    <h2>Grid</h2>
    <div class="row-grid">
      <div>1 2 3 4 5 6 7 8 9 0</div>
      <div>2</div>
      <div>3</div>
      <div>4</div>
      <div>5</div>
      <div>6</div>
    </div>
  </body>
</html>
```
- Flexbox `outperforms` Grid in this use case. Yes, you could use some hack to get CSS Grid replicate this behavior using minmax() function, but Flexbox is well-suited for this kind of single dimensional layouts.

## Will CSS Grid make Flexbox Obsolete in the Future?
- Absolutely not.

- In fact, that’s what this article was about. CSS grid and Flexbox, both are designed to solve a `different` set of problems.

- Currently, CSS `Grid doesn’t` have enough support across the `browsers` to make production ready websites.
- The `general rule of thumb` I use is that a feature must cover more than `95% of global usage`. Only then I use that feature in real websites. 
- Currently, `Flexbox covers 95% of global usage`, and `Grid covers 87% of global usage`.

- Soon Grid will also get good support among the browsers, and we will use a mix of Grids and Flexboxes to make amazing website layouts that previously weren’t possible.
# Box Sizing

# Use CSS Variables

- Syntax: `var(name, value)`
- CSS variables can have a `global or local` scope.
  - To create a variable with global scope, declare it inside the `:root` selector.
  ```css
  :root {
    --blue: #1e90ff;
    --white: #ffffff;
  }
  ```

# Override styles order

- !important> style > id > class (top-> bottom class declaration in `<style> section`)

# Units

## Absolute lengths

- The absolute length units are fixed and a length expressed in any of these will appear as exactly that size.
- Absolute length units are `not recommended` for use on screen, because screen sizes vary so much.
- However, they can be used if the output medium is known, such as for print layout.

  - `cm` - centimeters
  - `mm` - millimeters
  - `in` - inches (1in = 96px = 2.54cm)
  - `px \*` - pixels (1px = 1/96th of 1in)

  - `pt` - points (1pt = 1/72 of 1in)

  - `pc` - picas (1pc = 12 pt)

- Note\*: Pixels (px) are relative to the viewing device. For low-dpi devices, 1px is one device pixel (dot) of the display. For printers and high resolution screens 1px implies multiple device pixels.

## Relative lengths

- Relative length units specify a length relative to another length property.
- Relative length units scale better between different rendering medium.
  - `em` - Relative to the font-size of the element (2em means 2 times the size of the current font)
  - `ex` - Relative to the x-height of the current font (rarely used)
  - `ch` - Relative to the width of the "0" (zero)
  - `rem` - Relative to font-size of the root element
  - `vw` - Relative to 1% of the width of the viewport\*
  - `vh` - Relative to 1% of the height of the viewport\*
  - `vmin` - Relative to 1% of viewport's\* smaller dimension
    - vmin uses the ratio of the smallest side. That is, if the height of the browser window is less than its width, 1vmin will be equivalent to 1vh. If the width of the browser is less than it’s height, 1vmin is equvialent to 1vw.
  - `vmax` - Relative to 1% of viewport's\* larger dimension
    - vmax is the opposite: it uses the largest side. So 1vmax is equivalent to 1vw if the viewport is wider than it is tall; if the browser is taller than it is wide, 1vmax will be equivalent to 1vh.
  - `%` - Relative to the parent element

## What they used for?

- `vmin and vmax` is an excellent substitute for, or addition to, CSS `orientation` media queries (@media screen and (orientation : `portrait`) or @media screen and (orientation : `landscape`)), since they respond immediately to the aspect ratio of the screen.

# Applied Accessibility

## Alt

- `Alt` text describes the content of the image and provides a text-alternative for it. This helps in cases where the image fails to load or can't be seen by a user.
- It's also used by search engines to understand what an image contains to include it in search results. Here's an example:

```html
<img src="importantLogo.jpeg" alt="Company logo" />
```

- People with visual impairments rely on screen readers to convert web content to an audio interface. They won't get information if it's only presented visually. For images, screen readers can access the alt attribute and read its contents to deliver key information
- Good alt text provides the reader a brief description of the image. You should always include an alt attribute on your image. Per HTML5 specification, this is now considered mandatory.

## Jump Straight to the Content Using the main Element

- The main element is used to wrap (you guessed it) the main content, and there should be only one per page. It's meant to surround the information that's related to the central topic of your page. It's not meant to include items that repeat across pages, like navigation links or banners.

- The main tag also has an embedded landmark feature that assistive technology can use to quickly navigate to the main content. If you've ever seen a "Jump to Main Content" link at the top of a page, using a main tag automatically gives assistive devices that functionality.

## Wrap Content in the article Element

- `article` is another one of the new HTML5 elements that adds semantic meaning to your markup. article is a sectioning element, and is used to wrap independent, self-contained content. The tag works well with blog entries, forum posts, or news articles
- Determining whether content can stand alone is usually a judgement call, but there are a couple simple tests you can use. Ask yourself if you removed all surrounding context, would that content still make sense? Similarly for text, would the content hold up if it were in an `RSS` feed?
- `Note about section and div`
  - The section element is also new with HTML5, and has a slightly different semantic meaning than article. An article is for standalone content, and a section is for grouping thematically related content. They can be used within each other, as needed.
  - For example, if a book is the article, then each chapter is a section. When there's no relationship between groups of content, then use a div.

```html
<div>
  - groups content
  <section>
    - groups related content
    <article>- groups independent, self-contained content</article>
  </section>
</div>
```

```html
<h1>Deep Thoughts with Master Camper Cat</h1>
<main>
  <div>
    <h2>The Garfield Files: Lasagna as Training Fuel?</h2>
    <p>
      The internet is littered with varying opinions on nutritional paradigms,
      from catnip paleo to hairball cleanses. But let's turn our attention to an
      often overlooked fitness fuel, and examine the protein-carb-NOM trifecta
      that is lasagna...
    </p>
  </div>

  <img src="samuraiSwords.jpeg" alt="" />

  <article>
    <h2>Defeating your Foe: the Red Dot is Ours!</h2>
    <p>
      Felines the world over have been waging war on the most persistent of
      foes. This red nemesis combines both cunning stealth and lightning speed.
      But chin up, fellow fighters, our time for victory may soon be near...
    </p>
  </article>

  <img src="samuraiSwords.jpeg" alt="" />

  <article>
    <h2>Is Chuck Norris a Cat Person?</h2>
    <p>
      Chuck Norris is widely regarded as the premier martial artist on the
      planet, and it's a complete coincidence anyone who disagrees with this
      fact mysteriously disappears soon after. But the real question is, is he a
      cat person?...
    </p>
  </article>
</main>
```

## Section combined with article tags

- `header` shares the embedded landmark feature you saw with main, allowing assistive technologies to quickly navigate to that content.

```html
<body>
  <header><h1>Training with Camper Cat</h1></header>
  <main>
    <section id="stealth">
      <h2>Stealth &amp; Agility Training</h2>
      <article>
        <h3>Climb foliage quickly using a minimum spanning tree approach</h3>
      </article>
      <article><h3>No training is NP-complete without parkour</h3></article>
    </section>
    <section id="combat">
      <h2>Combat Training</h2>
      <article>
        <h3>Dispatch multiple enemies with multithreaded tactics</h3>
      </article>
      <article>
        <h3>Goodbye world: 5 proven ways to knock out an opponent</h3>
      </article>
    </section>
    <section id="weapons">
      <h2>Weapons Training</h2>
      <article>
        <h3>Swords: the best tool to literally divide and conquer</h3>
      </article>
      <article>
        <h3>Breadth-first or depth-first in multi-weapon training?</h3>
      </article>
    </section>
  </main>
</body>
```

## Use Nav

- The `nav` element is another HTML5 item with the embedded landmark feature for easy screen reader navigation. This tag is meant to wrap around the main navigation links in your page.

```html
<body>
  <header>
    <h1>Training with Camper Cat</h1>

    <nav>
      <ul>
        <li><a href="#stealth">Stealth &amp; Agility</a></li>
        <li><a href="#combat">Combat</a></li>
        <li><a href="#weapons">Weapons</a></li>
      </ul>
    </nav>
  </header>
  <main>
    <section id="stealth">
      <h2>Stealth &amp; Agility Training</h2>
      <article>
        <h3>Climb foliage quickly using a minimum spanning tree approach</h3>
      </article>
      <article><h3>No training is NP-complete without parkour</h3></article>
    </section>
    <section id="combat">
      <h2>Combat Training</h2>
      <article>
        <h3>Dispatch multiple enemies with multithreaded tactics</h3>
      </article>
      <article>
        <h3>Goodbye world: 5 proven ways to knock out an opponent</h3>
      </article>
    </section>
    <section id="weapons">
      <h2>Weapons Training</h2>
      <article>
        <h3>Swords: the best tool to literally divide and conquer</h3>
      </article>
      <article>
        <h3>Breadth-first or depth-first in multi-weapon training?</h3>
      </article>
    </section>
  </main>
</body>
```

## Improve Accessibility of Audio Content with the audio Element

- HTML5's audio element gives semantic meaning when it wraps sound or audio stream content in your markup. Audio content also needs a text alternative to be accessible to people who are deaf or hard of hearing. This can be done with nearby text on the page or a link to a transcript.

- The audio tag supports the controls attribute. This shows the browser default play, pause, and other controls, and supports keyboard functionality. This is a boolean attribute, meaning it doesn't need a value, its presence on the tag turns the setting on.

```html
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

## Improve Chart Accessibility with the figure Element

- HTML5 introduced the `figure` element, along with the related figcaption.
- Used together, these items wrap a visual representation (like an image, diagram, or chart) along with its caption. This gives a two-fold accessibility boost by both semantically grouping related content, and providing a text alternative that explains the figure.
- For data visualizations like charts, the caption can be used to briefly note the trends or conclusions for users with visual impairments. Another challenge covers how to move a table version of the chart's data off-screen (using CSS) for screen reader users.

```html
<figure>
  <img
    src="roundhouseDestruction.jpeg"
    alt="Photo of Camper Cat executing a roundhouse kick"
  />
  <br />
  <figcaption>
    Master Camper Cat demonstrates proper form of a roundhouse kick.
  </figcaption>
</figure>
```

## Improve Form Field Accessibility with the label Element

- Improving accessibility with semantic HTML markup applies to using both appropriate tag names as well as attributes. The next several challenges cover some important scenarios using attributes in forms.

- The label tag wraps the text for a specific form control item, usually the name or label for a choice. This ties meaning to the item and makes the form more readable. The `for` attribute on a `label` tag explicitly associates that label with the form control and is used by screen readers.

## Wrap Radio Buttons in a fieldset Element for Better Accessibility

- The `fieldset` tag surrounds the entire grouping of radio buttons to achieve this. It often uses a legend tag to provide a description for the grouping, which is read by screen readers for each choice in the fieldset element.

- The `fieldset` wrapper and legend tag are not necessary when the choices are self-explanatory, like a gender selection.
- Using a `label` with the for attribute for each radio button is sufficient.

```html
<body>
  <header>
    <h1>Deep Thoughts with Master Camper Cat</h1>
  </header>
  <section>
    <form>
      <p>Sign up to receive Camper Cat's blog posts by email here!</p>
      <label for="email">Email:</label>
      <input type="text" id="email" name="email" />

      <!-- Only change code below this line -->
      <fieldset>
        <legend>What level ninja are you?</legend>
        <input id="newbie" type="radio" name="levels" value="newbie" />
        <label for="newbie">Newbie Kitten</label><br />
        <input
          id="intermediate"
          type="radio"
          name="levels"
          value="intermediate"
        />
        <label for="intermediate">Developing Student</label><br />
        <input id="master" type="radio" name="levels" value="master" />
        <label for="master">Master</label>
      </fieldset>
      <!-- Only change code above this line -->

      <input type="submit" name="submit" value="Submit" />
    </form>
  </section>
  <article>
    <h2>The Garfield Files: Lasagna as Training Fuel?</h2>
    <p>
      The internet is littered with varying opinions on nutritional paradigms,
      from catnip paleo to hairball cleanses. But let's turn our attention to an
      often overlooked fitness fuel, and examine the protein-carb-NOM trifecta
      that is lasagna...
    </p>
  </article>
  <img src="samuraiSwords.jpeg" alt="" />
  <article>
    <h2>Defeating your Foe: the Red Dot is Ours!</h2>
    <p>
      Felines the world over have been waging war on the most persistent of
      foes. This red nemesis combines both cunning stealth and lightning speed.
      But chin up, fellow fighters, our time for victory may soon be near...
    </p>
  </article>
  <img src="samuraiSwords.jpeg" alt="" />
  <article>
    <h2>Is Chuck Norris a Cat Person?</h2>
    <p>
      Chuck Norris is widely regarded as the premier martial artist on the
      planet, and it's a complete coincidence anyone who disagrees with this
      fact mysteriously disappears soon after. But the real question is, is he a
      cat person?...
    </p>
  </article>
  <footer>&copy; 2018 Camper Cat</footer>
</body>
```

## Use the align-self Property

- This property allows you to `adjust` each item's alignment individually, instead of setting them all at once. This is useful since other common adjustment techniques using the CSS properties float, clear, and vertical-align do not work on flex items.

- `align-self` accepts the same values as align-items and will override any value set by the align-items property.

# Responsive

## Use a Retina Image for Higher Resolution Displays

- Pixel density is an aspect that could be different on one device from others and this density is known as `Pixel Per Inch(PPI)` or `Dots Per Inch(DPI)`.
- The most famous such display is the one known as a `Retina Display` on the latest Apple MacBook Pro notebooks, and recently iMac computers.
- Due to the difference in pixel density between a "Retina" and "Non-Retina" displays, some images that have not been made with a High-Resolution Display in mind could look "pixelated" when rendered on a High-Resolution display.
- The simplest way to make your images properly appear on High-Resolution Displays, such as the MacBook Pros "retina display" is to define their `width` and `height` values as `only half` of what the original file is. Here is an example of an image that is only using half of the original height and width:

```html
<style>
  img {
    height: 250px;
    width: 250px;
  }
</style>
<img src="coolPic500x500" alt="A most excellent picture" />
```

## Make Typography Responsive

- Instead of using `em` or `px` to size text, you can use `viewport units` for `responsive` typography.
- Viewport units, like percentages, are relative units, but they are based off different items.
- Viewport units are relative to the viewport dimensions (width or height) of a device, and percentages are relative to the size of the parent container element.

- The four different viewport units are:
  - `vw` (viewport width): 10vw would be 10% of the viewport's width.
  - `vh` (viewport height): 3vh would be 3% of the viewport's height.
  - `vmin` (viewport minimum): 70vmin would be 70% of the viewport's smaller dimension (height or width).
  - `vmax` (viewport maximum): 100vmax would be 100% of the viewport's bigger dimension (height or width).
- Here is an example that sets a body tag to 30% of the viewport's width.
  ```css
  body {
    width: 30vw;
  }
  ```

# Reference:

- Understanding vMin and vMax in CSS: http://thenewcode.com/1137/MinMaxing-Understanding-vMin-and-vMax-in-CSS
- https://css-tricks.com/simple-little-use-case-vmin/
