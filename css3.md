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

# Box shadow
- The box-shadow property takes values for in the order:
  - offset-x (how far to push the shadow horizontally from the element),
  - offset-y (how far to push the shadow vertically from the element),
  - blur-radius, spread-radius
  - color.
- Multiple box-shadows can be created by using commas to separate properties of each box-shadow element.
```css
box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
```

# Text transform
- lowercase:	"transform me"
- uppercase:	"TRANSFORM ME"
- capitalize:	"Transform Me"
- initial:	Use the default value
- inherit:	Use the text-transform value from the parent element
- none:	Default: Use the original text

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
  border: 3px solid #73AD21;
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
  border: 3px solid #73AD21;
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
  border: 3px solid #73AD21;
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
  border: 3px solid #73AD21;
}

div.absolute {
  position: absolute;
  top: 80px;
  right: 0;
  width: 200px;
  height: 100px;
  border: 3px solid #73AD21;
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
  border: 2px solid #4CAF50;
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

## Reference:
- Positions: https://www.w3schools.com/css/css_positioning.asp

# Flexbox

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
- !important> style > id > class (top-> bottom class declaration in <style> section)

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
## Reference:
 - Understanding vMin and vMax in CSS: http://thenewcode.com/1137/MinMaxing-Understanding-vMin-and-vMax-in-CSS
 - https://css-tricks.com/simple-little-use-case-vmin/