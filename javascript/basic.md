# Intro

- Give some tips for a easier life of javascript :) inspired by freeCodeCamp

## Escaping Literal Quotes in StringsPassed

- When you are defining a string you must start and end with a single or double quote. What happens when you need a literal quote: " or ' inside of your string?

- In JavaScript, you can escape a quote from considering it as an end of string quote by placing a backslash (\) in front of the quote.

```javascript
var sampleStr = 'Alan said, "Peter is learning JavaScript".';
```

- This signals to JavaScript that the following quote is not the end of the string, but should instead appear inside the string. So if you were to print this to the console, you would get:
  `Alan said, "Peter is learning JavaScript".`

## Escape Sequences in Strings

- Quotes are not the only characters that can be escaped inside a string. There are two reasons to use escaping characters:
  - To allow you to use characters you may not otherwise be able to type out, such as a carriage return.
  - To allow you to represent multiple quotes in a string without JavaScript misinterpreting what you mean.
- Code Output
  - `\'` single quote
  - `\"` double quote
  - `\\` backslash
  - `\n` newline
  - `\r` carriage return
  - `\t` tab
  - `\b` word boundary
  - `\f` form feed

## Comparison with the Greater Than Operator

- The greater than operator (>) compares the values of two numbers. If the number to the left is greater than the number to the right, it returns true. Otherwise, it returns false.

- Like the equality operator, greater than operator will convert data types of values while comparing.

```javascript
1 > ""; // true
1 > " "; // true
1 > "2"; // false
1 > "abc"; // false
1 < "abc"; // false
5 > 3; // true
7 > "3"; // true
2 > 3; // false
"1" > 9; // false
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

## Testing Objects for Properties

- Sometimes it is useful to check if the property of a given object exists or not. We can use the .`hasOwnProperty(propname)` method of objects to determine if that object has the given property name. .`hasOwnProperty()` returns true or false if the property is found or not.

Example

```javascript
var myObj = {
  top: "hat",
  bottom: "pants",
};
myObj.hasOwnProperty("top"); // true
myObj.hasOwnProperty("middle"); // false
```

## Iterate with JavaScript Do...While LoopsPassed

- The next type of loop you will learn is called a do...while loop. It is called a do...while loop because it will first do one pass of the code inside the loop no matter what, and then continue to run the loop while the specified condition evaluates to true.

```javascript
var ourArray = [];
var i = 0;
do {
  ourArray.push(i);
  i++;
} while (i < 5);
```

- The example above behaves similar to other types of loops, and the resulting array will look like [0, 1, 2, 3, 4]. However, what makes the do...while different from other loops is how it behaves when the condition fails on the first check. Let's see this in action: Here is a regular while loop that will run the code in the loop as long as `i < 5`:

```javascript
var ourArray = [];
var i = 5;
while (i < 5) {
  ourArray.push(i);
  i++;
}
```

- In this example, we initialize the value of ourArray to an empty array and the value of i to 5. When we execute the while loop, the condition evaluates to false because i is not less than 5, so we do not execute the code inside the loop. The result is that ourArray will end up with no values added to it, and it will still look like [] when all of the code in the example above has completed running. Now, take a look at a do...while loop:

```javascript
var ourArray = [];
var i = 5;
do {
  ourArray.push(i);
  i++;
} while (i < 5);
```

- In this case, we initialize the value of i to `5`, just like we did with the while loop. When we get to the next line, there is no condition to evaluate, so we go to the code inside the curly braces and execute it. We will add a single element to the array and then increment i before we get to the condition check. When we finally evaluate the condition `i < 5` on the last line, we see that i is now `6`, which fails the conditional check, so we exit the loop and are done. At the end of the above example, the value of ourArray is [5]. Essentially, a do...while loop ensures that the code inside the loop will run at least once. Let's try getting a do...while loop to work by pushing values to an array.

## Replace Loops using Recursion

- Recursion is the concept that a function can be expressed in terms of itself. To help understand this, start by thinking about the following task: multiply the first n elements of an array to create the product of those elements. Using a for loop, you could do this:

```javascript
function multiply(arr, n) {
  var product = 1;
  for (var i = 0; i < n; i++) {
    product *= arr[i];
  }
  return product;
}
```

- However, notice that multiply(arr, n) == multiply(arr, n - 1) \* arr[n - 1]. That means you can rewrite multiply in terms of itself and never need to use a loop.

```javascript
function multiply(arr, n) {
  if (n <= 0) {
    return 1;
  } else {
    return multiply(arr, n - 1) * arr[n - 1];
  }
}
```

- The recursive version of multiply breaks down like this. In the base case, where n <= 0, it returns 1. For larger values of n, it calls itself, but with n - 1. That function call is evaluated in the same way, calling multiply again until n <= 0. At this point, all the functions can return and the original multiply returns the answer.

- Note: Recursive functions must have a base case when they return without calling the function again (in this example, when n <= 0), otherwise they can never finish executing.


