# Intro

## Escaping Literal Quotes in StringsPassed
- When you are defining a string you must start and end with a single or double quote. What happens when you need a literal quote: " or ' inside of your string?

- In JavaScript, you can escape a quote from considering it as an end of string quote by placing a backslash (\) in front of the quote.
```javascript
var sampleStr = "Alan said, \"Peter is learning JavaScript\".";
```
- This signals to JavaScript that the following quote is not the end of the string, but should instead appear inside the string. So if you were to print this to the console, you would get:
`Alan said, "Peter is learning JavaScript".`

## Escape Sequences in Strings
- Quotes are not the only characters that can be escaped inside a string. There are two reasons to use escaping characters:
  -  To allow you to use characters you may not otherwise be able to type out, such as a carriage return.
  - To allow you to represent multiple quotes in a string without JavaScript misinterpreting what you mean.
- Code	Output
  - `\'`	single quote
  - `\"`	double quote
  - `\\`	backslash
  - `\n`	newline
  - `\r`	carriage return
  - `\t`	tab
  - `\b`	word boundary
  - `\f`	form feed

## Comparison with the Greater Than Operator
- The greater than operator (>) compares the values of two numbers. If the number to the left is greater than the number to the right, it returns true. Otherwise, it returns false.

- Like the equality operator, greater than operator will convert data types of values while comparing.

```javascript
1 > ''     // true
1 > ' '    // true
1 > '2'    // false
1 > 'abc'  // false
1 < 'abc'  // false
5   >  3   // true
7   > '3'  // true
2   >  3   // false
'1' >  9   // false
```

## Introducing Else If Statements
- If you have multiple conditions that need to be addressed, you can chain if statements together with else if statements.
```javascript
if (num > 15) {
  return "Bigger than 15";
} else if (num < 5) {
  return "Smaller than 5";
} else {
  return "Between 5 and 15";
}
```