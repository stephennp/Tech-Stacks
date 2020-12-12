# Intro

- Give some tips for a easier life of javascript :)

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

# ES6

## Explore Differences Between the var and let Keywords

- One of the biggest problems with declaring variables with the var keyword is that you can overwrite variable declarations without an error.

```javascript
var camper = "James";
var camper = "David";
console.log(camper);
// logs 'David'
```

- As you can see in the code above, the camper variable is originally declared as James and then overridden to be David. In a small application, you might not run into this type of problem, but when your code becomes larger, you might accidentally overwrite a variable that you did not intend to overwrite. Because this behavior does not throw an error, searching and fixing bugs becomes more difficult.
  A new keyword called let was introduced in ES6 to solve this potential issue with the var keyword. If you were to replace var with let in the variable declarations of the code above, the result would be an error.

```javascript
let camper = "James";
let camper = "David"; // throws an error
```

- This error can be seen in the console of your browser. So unlike var, when using let, a variable with the same name can only be declared once. Note the "use strict". This enables Strict Mode, which catches common coding mistakes and "unsafe" actions. For instance:

```javascript
"use strict";
x = 3.14; // throws an error because x is not declared
```

## Compare Scopes of the var and let Keywords

- When you declare a variable with the `var` keyword, it is declared globally, or locally if declared inside a function.

- The `let` keyword behaves similarly, but with some extra features. When you declare a variable with the let keyword `inside` a block, statement, or expression, its scope is limited to that block, statement, or expression.

For example:

```javascript
var numArray = [];
for (var i = 0; i < 3; i++) {
  numArray.push(i);
}
console.log(numArray);
// returns [0, 1, 2]
console.log(i);
// returns 3
```

- With the `var` keyword, i is declared globally. So when `i++` is executed, it updates the global variable. This code is similar to the following:

```javascript
var numArray = [];
var i;
for (i = 0; i < 3; i++) {
  numArray.push(i);
}
console.log(numArray);
// returns [0, 1, 2]
console.log(i);
// returns 3
```

- This behavior will cause problems if you were to create a function and store it for later use inside a for loop that uses the i variable. This is because the stored function will always refer to the value of the updated global i variable.

```javascript
var printNumTwo;
for (var i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function () {
      return i;
    };
  }
}
console.log(printNumTwo());
// returns 3
```

- As you can see, printNumTwo() prints 3 and not 2. This is because the value assigned to i was updated and the printNumTwo() returns the global i and not the value i had when the function was created in the for loop. The let keyword does not follow this behavior:

```javascript
let printNumTwo;
for (let i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function () {
      return i;
    };
  }
}
console.log(printNumTwo());
// returns 2
console.log(i);
// returns "i is not defined"
```

- `i` is not defined because it was not declared in the global scope. It is only declared within the for loop statement. printNumTwo() returned the correct value because three different i variables with unique values (0, 1, and 2) were created by the let keyword within the loop statement.

## Declare a Read-Only Variable with the const Keyword

- The keyword `let` is not the only new way to declare variables. In ES6, you can also declare variables using the `const` keyword.

- `const` has all the awesome features that let has, with the added bonus that variables declared using const are read-only. They are a constant value, which means that once a variable is assigned with const, it `cannot be reassigned`.

```javascript
const FAV_PET = "Cats";
FAV_PET = "Dogs"; // returns error
```

- As you can see, trying to `reassign` a variable declared with const will `throw an error`. You should always name variables you don't want to reassign using the const keyword.
- This helps when you accidentally attempt to reassign a variable that is meant to stay constant.
- A common practice when naming constants is to use `all uppercase letters`, with words separated by an `underscore`.

- Note: It is common for developers to use `uppercase variable identifiers for immutable values` and `lowercase or camelCase for mutable values (objects and arrays)`. In a later challenge you will see an example of a lowercase variable identifier being used for an array.

## Mutate an Array Declared with const

- The const declaration has many use cases in modern JavaScript.

- Some developers prefer to assign all their variables using `const` by default, unless they know they will need to reassign the value. Only in that case, they use let.

- However, it is important to understand that `objects (including arrays and functions)` assigned to a variable using `const` are still `mutable`.
- Using the const declaration only `prevents reassignment of the variable identifier`.

```javascript
const s = [5, 6, 7];
s = [1, 2, 3]; // throws error, trying to assign a const
s[2] = 45; // works just as it would with an array declared with var or let
console.log(s); // returns [5, 6, 45]
```

- As you can see, you can mutate the object [5, 6, 7] itself and the variable s will still point to the altered array [5, 6, 45]. Like all arrays, the array elements in s are mutable, but because const was used, you cannot use the variable identifier s to point to a different array using the assignment operator.

## Prevent Object Mutation

- As seen in the previous challenge, `const` declaration alone doesn't really protect your data from mutation. To ensure your data doesn't change, JavaScript provides a function `Object.freeze` to prevent data mutation.

- Once the object is frozen, you can no longer add, update, or delete properties from it. Any attempt at changing the object will be rejected without an error.

```javascript
let obj = {
  name: "FreeCodeCamp",
  review: "Awesome",
};
Object.freeze(obj);
obj.review = "bad"; // will be ignored. Mutation not allowed
obj.newProp = "Test"; // will be ignored. Mutation not allowed
console.log(obj);
// { name: "FreeCodeCamp", review:"Awesome"}
```

## Use the Rest Parameter with Function Parameters

- In order to help us create more flexible functions, ES6 introduces the `rest parameter` for function parameters. With the rest parameter, you can create functions that take a variable number of arguments. These arguments are stored in an array that can be accessed later from inside the function.

Check out this code:

```javascript
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
```

console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], { })); // You have passed 4 arguments.
The rest parameter eliminates the need to check the args array and allows us to apply map(), filter() and reduce() on the parameters array.

## Use the Spread Operator to Evaluate Arrays In-Place

- ES6 introduces the `spread` operator, which allows us to expand arrays and other expressions in places where multiple parameters or elements are expected.

- The ES5 code below uses apply() to compute the maximum value in an array:

```javascript
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr); // returns 89
```

- We had to use `Math.max.apply(null, arr)` because Math.max(arr) returns NaN. Math.max() expects comma-separated arguments, but not an array. The spread operator makes this syntax much better to read and maintain.

```javascript
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // returns 89
```

- ...arr returns an `unpacked array`. In other words, it spreads the array. However, the spread operator only works in-place, like in an argument to a function or in an array literal. The following code will not work:

```javascript
const spreaded = ...arr; // will throw a syntax error
```

## Use Destructuring Assignment to Extract Values from Objects

- Destructuring assignment is special syntax introduced in ES6, for neatly assigning values taken directly from an object.

- Consider the following ES5 code:

```javascript
const user = { name: "John Doe", age: 34 };

const name = user.name; // name = 'John Doe'
const age = user.age; // age = 34
```

- Here's an equivalent assignment statement using the ES6 destructuring syntax:

```javascript
const { name, age } = user;
// name = 'John Doe', age = 34
```

- Here, the name and age variables will be created and assigned the values of their respective values from the user object. You can see how much cleaner this is.

- You can extract as many or few values from the object as you want.

## Use Destructuring Assignment to Assign Variables from ObjectsPassed

- Destructuring allows you to assign a new variable name when extracting values. You can do this by putting the new name after a colon when assigning the value.

- Using the same object from the last example:

```javascript
const user = { name: 'John Doe', age: 34 };
Here's how you can give new variable names in the assignment:

const { name: userName, age: userAge } = user;
// userName = 'John Doe', userAge = 34
```

- You may read it as "get the value of user.name and assign it to a new variable named userName" and so on.

## Use Destructuring Assignment to Assign Variables from Nested Objects

- You can use the same principles from the previous two lessons to destructure values from nested objects.

- Using an object similar to previous examples:

```javascript
const user = {
  johnDoe: {
    age: 34,
    email: "johnDoe@freeCodeCamp.com",
  },
};
```

- Here's how to extract the values of object properties and assign them to variables with the same name:

```javascript
const {
  johnDoe: { age, email },
} = user;
```

- And here's how you can assign an object properties' values to variables with different names:

```javascript
const {
  johnDoe: { age: userAge, email: userEmail },
} = user;
```

## Use Destructuring Assignment to Assign Variables from Nested Objects

- You can use the same principles from the previous two lessons to destructure values from nested objects.

- Using an object similar to previous examples:

```javascript
const user = {
  johnDoe: {
    age: 34,
    email: "johnDoe@freeCodeCamp.com",
  },
};
```

- Here's how to extract the values of object properties and assign them to variables with the same name:

```javascript
const {
  johnDoe: { age, email },
} = user;
```

- And here's how you can assign an object properties' values to variables with different names:

```javascript
const {
  johnDoe: { age: userAge, email: userEmail },
} = user;
```

## Use Destructuring Assignment to Assign Variables from Arrays

- ES6 makes destructuring arrays as easy as destructuring objects.

- One key difference between the `spread operator and array destructuring` is

  - The `spread` operator `unpacks` all contents of an array into a `comma-separated list`. Consequently, you `cannot` pick or choose which elements you want to assign to variables.

- Destructuring an array lets us do exactly that:

```javascript
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b); // 1, 2
```

- The variable `a` is assigned the first value of the array, and `b` is assigned the second value of the array. We can also access the value at any index in an array with destructuring by using commas to reach the desired index:

```javascript
const [a, b, , , c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c); // 1, 2, 5
```

## Use Destructuring Assignment with the Rest Parameter to Reassign Array Elements

- In some situations involving array destructuring, we might want to collect the rest of the elements into a separate array.

- The result is similar to `Array.prototype.slice()`, as shown below:

```javascript
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b); // 1, 2
console.log(arr); // [3, 4, 5, 7]
```

- Variables `a` and `b` take the first and second values from the array. After that, because of the rest parameter's presence, arr gets the rest of the values in the form of an array. The rest element only works correctly as the last variable in the list. As in, you cannot use the rest parameter to catch a subarray that leaves out the last element of the original array.

## Use Destructuring Assignment to Pass an Object as a Function's Parameters

- In some cases, you can destructure the object in a function argument itself.

- Consider the code below:

```javascript
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;
  // do something with these variables
};
```

- This effectively destructures the object sent into the function. This can also be done in-place:

```javascript
const profileUpdate = ({ name, age, nationality, location }) => {
  /* do something with these fields */
};
```

- When profileData is passed to the above function, the values are destructured from the function parameter for use within the function.

## Create Strings using Template Literals

- `Template literals` allow you to create multi-line strings and to use string interpolation features to create strings.

Consider the code below:

```javascript
const person = {
  name: "Zodiac Hasbro",
  age: 56,
};

// Template literal with multi-line and string interpolation
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting); // prints
// Hello, my name is Zodiac Hasbro!
// I am 56 years old.
```

- A lot of things happened there. Firstly, the example uses backticks (`), not quotes (' or "), to wrap the string. Secondly, notice that the string is multi-line, both in the code and the output. This saves inserting \n within strings.\
- The `${variable}` syntax used above is a placeholder. Basically, you won't have to use concatenation with the + operator anymore. To add variables to strings, you just drop the variable in a template string and wrap it with `${ and }`. Similarly, you can include other expressions in your string literal, for example `${a + b}`. This new way of creating strings gives you more flexibility to create robust strings.

- Use template literal syntax with backticks to create an array of list element (li) strings. Each list element's text should be one of the array elements from the failure property on the result object and have a class attribute with the value text-warning. The makeList function should return the array of list item strings.

## Use getters and setters to Control Access to an Object

- You can obtain values from an object and set the value of a property within an object.

- These are classically called getters and setters.

- `Getter` functions are meant to simply return (get) the value of an object's private variable to the user without the user directly accessing the private variable.

- `Setter` functions are meant to modify (set) the value of an object's private variable based on the value passed into the setter function. This change could involve calculations, or even overwriting the previous value completely.

```javascript
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book("anonymous");
console.log(novel.writer); // anonymous
novel.writer = "newAuthor";
console.log(novel.writer); // newAuthor
```

- Notice the syntax used to invoke the getter and setter. They do not even look like functions. Getters and setters are important because they hide internal implementation details.
- Note: It is convention to precede the name of a private variable with an underscore `(\_)`. However, the practice itself does not make a variable private.

## Create a Module Script