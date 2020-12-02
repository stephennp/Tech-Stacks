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