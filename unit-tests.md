# Unit test

## Intro

- Unit tests test individual software components and methods.
- Unit tests should only test code within the developer’s control.
- They should not test **infrastructure concerns**.
  - Infrastructure concerns include databases, file systems, and network resources.

## Why unit test?

- There are numerous benefits to writing unit tests; they help with regression, provide documentation, and facilitate good design.

### 1. Less time performing functional tests

- Functional tests are expensive.
- They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior
- These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test
- Unit tests, on the other hand, take milliseconds, can be run at the press of a button, and don't necessarily require any knowledge of the system at large

### 2. Protection against regression

- With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code.
- Giving you confidence that your new code does not break existing functionality.

### 3. Executable documentation

- It may not always be obvious what a particular method does or how it behaves given a certain input.
- You may ask yourself: How does this method behave if I pass it a blank string? Null?
- When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input.
- In addition, it should be able to verify that it actually works.

### 4. Less coupled code

- When code is tightly coupled, it can be difficult to unit test. Without creating unit tests for the code that you're writing, coupling may be less apparent.
- Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.

### 5. Characteristics of a good unit test

- **Fast**
  - It is not uncommon for mature projects to have thousands of unit tests. Unit tests should take very little time to run. Milliseconds.
- **Isolated**
  - Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
- **Repeatable**
  - Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.
- **Self-Checking**
  - The test should be able to automatically detect if it passed or failed without any human interaction.
- **Timely**
  - A unit test should not take a disproportionately long time to write compared to the code being tested.
  - If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.

### 6. Let's speak the same language

- **Fake**
  - A fake is a generic term that can be used to describe either a stub or a mock object.
  - Whether it's a stub or a mock depends on the context in which it's used. So in other words, a fake can be a stub or a mock.
- **Mock**
  - A mock object is a fake object in the system that decides whether or not a unit test has passed or failed.
  - A mock starts out as a Fake until it's asserted against.
- **Stub**
  - A stub is a controllable replacement for an existing dependency (or collaborator) in the system.
  - By using a stub, you can test your code without dealing with the dependency directly.
  - By default, a fake starts out as a stub.
- Examples:

  - Wrong

  ```csharp
  var mockOrder = new MockOrder();
  var purchase = new Purchase(mockOrder);

  purchase.ValidateOrders();

  Assert.True(purchase.CanBeShipped);
  ```

  - Better

  ```csharp
  var stubOrder = new FakeOrder();
  var purchase = new Purchase(stubOrder);

  purchase.ValidateOrders();

  Assert.True(purchase.CanBeShipped);
  ```

  - Another better:

  ```csharp
  var mockOrder = new FakeOrder();
  var purchase = new Purchase(mockOrder);

  purchase.ValidateOrders();

  Assert.True(mockOrder.Validated);
  ```

## Best practices

### 1. Naming your tests

- The name of the method being tested.
- The scenario under which it's being tested.
- The expected behavior when the scenario is invoked.

### 2. Arranging your tests

- **Arrange, Act, Assert** is a common pattern when unit testing. As the name implies, it consists of three main actions:
  - Arrange your objects, creating and setting them up as necessary.
  - Act on an object.
  - Assert that something is as expected.
- Why?
  - Clearly separates what is being tested from the arrange and assert steps.
  - Less chance to intermix assertions with "Act" code.

### 3. Write minimally passing tests

- The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.
- Why?

  - Tests become more resilient to future changes in the codebase.
  - Closer to testing behavior over implementation.
  - Bad:

    ```csharp
    [Fact]
    public void Add_SingleNumber_ReturnsSameNumber()
    {
    	var stringCalculator = new StringCalculator();

    	var actual = stringCalculator.Add("42");

    	Assert.Equal(42, actual);
    }
    ```

  - Better:

    ```csharp
    [Fact]
    public void Add_SingleNumber_ReturnsSameNumber()
    {
    	var stringCalculator = new StringCalculator();

    	var actual = stringCalculator.Add("0");

    	Assert.Equal(0, actual);
    }
    ```

### Avoid magic strings

- Naming variables in unit tests is as important
- if not more important, than naming variables in production code. Unit tests should not contain magic strings.

Why? - Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special. - Explicitly shows what you're trying to prove rather than trying to accomplish. - Bad:

````csharp
[Fact]
public void Add_BigNumber_ThrowsException()
{
var stringCalculator = new StringCalculator();

    		Action actual = () => stringCalculator.Add("1001");

    		Assert.Throws<OverflowException>(actual);
    	}
    	```
    - Better:
    	```csharp
    	[Fact]
    	void Add_MaximumSumResult_ThrowsOverflowException()
    	{
    		var stringCalculator = new StringCalculator();
    		const string MAXIMUM_RESULT = "1001";

    		Action actual = () => stringCalculator.Add(MAXIMUM_RESULT);

    		Assert.Throws<OverflowException>(actual);
    	}
    	```

### Avoid logic in tests

- When writing your unit tests avoid manual string concatenation and logical conditions such as if, while, for, switch, etc.
- If logic in your test seems unavoidable, consider splitting the test up into two or more different tests.
- Why?

  - Less chance to introduce a bug inside of your tests.
  - Focus on the end result, rather than implementation details.
  - Bad:
    ```csharp
    [Fact]
    public void Add_MultipleNumbers_ReturnsCorrectResults()
    {
    var stringCalculator = new StringCalculator();
    var expected = 0;
    var testCases = new[]
    {
    "0,0,0",
    "0,1,2",
    "1,2,3"
    };

        	foreach (var test in testCases)
        	{
        		Assert.Equal(expected, stringCalculator.Add(test));
        		expected += 3;
        	}
        }
        ```

    - Better:

      ```csharp
      [Theory]
      [InlineData("0,0,0", 0)]
      [InlineData("0,1,2", 3)]
      [InlineData("1,2,3", 6)]
      public void Add_MultipleNumbers_ReturnsSumOfNumbers(string input, int expected)
      {
      	var stringCalculator = new StringCalculator();

      	var actual = stringCalculator.Add(input);

      	Assert.Equal(expected, actual);
      }
      ```

### Prefer helper methods to setup and teardown

- If you require a similar object or state for your tests, prefer a helper method than leveraging Setup and Teardown attributes if they exist.
- Why?

  - Less confusion when reading the tests since all of the code is visible from within each test.
  - Less chance of setting up too much or too little for the given test.
  - Less chance of sharing state between tests, which creates unwanted dependencies between them.
  - Bad:
    ```csharp
    private readonly StringCalculator stringCalculator;
    public StringCalculatorTests()
    {
    stringCalculator = new StringCalculator();
    }
    [Fact]
    public void Add_TwoNumbers_ReturnsSumOfNumbers()
    {
    var result = stringCalculator.Add("0,1");

        	Assert.Equal(1, result);
        }
        ```

    - Better:

      ```csharp
      [Fact]
      public void Add_TwoNumbers_ReturnsSumOfNumbers()
      {
      	var stringCalculator = CreateDefaultStringCalculator();

      	var actual = stringCalculator.Add("0,1");

      	Assert.Equal(1, actual);
      }
      private StringCalculator CreateDefaultStringCalculator()
      {
      	return new StringCalculator();
      }
      ```

### Avoid multiple asserts

- When writing your tests, try to only include one Assert per test. Common approaches to using only one assert include:
  - Create a separate test for each assert.
  - Use parameterized tests.
- Why?

  - If one Assert fails, the subsequent Asserts will not be evaluated.
  - Ensures you are not asserting multiple cases in your tests.
  - Gives you the entire picture as to why your tests are failing.
  - Bad:
    `csharp [Fact] public void Add_EdgeCases_ThrowsArgumentExceptions() { Assert.Throws<ArgumentException>(() => stringCalculator.Add(null)); Assert.Throws<ArgumentException>(() => stringCalculator.Add("a")); } `

    - Better:

      ```csharp
      [Theory]
      [InlineData(null)]
      [InlineData("a")]
      public void Add_InputNullOrAlphabetic_ThrowsArgumentException(string input)
      {
      	var stringCalculator = new StringCalculator();

      	Action actual = () => stringCalculator.Add(input);

      	Assert.Throws<ArgumentException>(actual);
      }
      ```

### Validate private methods by unit testing public methods

- In most cases, there should not be a need to test a private method. Private methods are an implementation detail.
- You can think of it this way: private methods never exist in isolation.
- At some point, there is going to be a public facing method that calls the private method as part of its implementation.
- What you should care about is the end result of the public method that calls into the private one.
- Bad:
  ```csharp
  public string ParseLogLine(string input)
  {
  var sanitizedInput = TrimInput(input);
  return sanitizedInput;
  }

      	private string TrimInput(string input)
      	{
      		return input.Trim();
      	}
      	```
      - Better:
      	```csharp
      	public void ParseLogLine_StartsAndEndsWithSpace_ReturnsTrimmedResult()
      	{
      		var parser = new Parser();

      		var result = parser.ParseLogLine(" a ");

      		Assert.Equals("a", result);
      	}
      	```

### Stub static references

- One of the principles of a unit test is that it must have full control of the system under test.
- This can be problematic when production code includes calls to static references (for example, DateTime.Now)
- Bad:
  ```csharp
  public int GetDiscountedPrice(int price)
  {
  if (DateTime.Now.DayOfWeek == DayOfWeek.Tuesday)
  {
  return price / 2;
  }
  else
  {
  return price;
  }
  }
  public void GetDiscountedPrice_NotTuesday_ReturnsFullPrice()
  {
  var priceCalculator = new PriceCalculator();

      		var actual = priceCalculator.GetDiscountedPrice(2);

      		Assert.Equals(2, actual)
      	}

      	public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
      	{
      		var priceCalculator = new PriceCalculator();

      		var actual = priceCalculator.GetDiscountedPrice(2);

      		Assert.Equals(1, actual);
      	}
      	```
      - Better:
      	```csharp
      	public interface IDateTimeProvider
      	{
      		DayOfWeek DayOfWeek();
      	}

      	public int GetDiscountedPrice(int price, IDateTimeProvider dateTimeProvider)
      	{
      		if (dateTimeProvider.DayOfWeek() == DayOfWeek.Tuesday)
      		{
      			return price / 2;
      		}
      		else
      		{
      			return price;
      		}
      	}
      	public void GetDiscountedPrice_NotTuesday_ReturnsFullPrice()
      	{
      		var priceCalculator = new PriceCalculator();
      		var dateTimeProviderStub = new Mock<IDateTimeProvider>();
      		dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Monday);

      		var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

      		Assert.Equals(2, actual);
      	}

      	public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
      	{
      		var priceCalculator = new PriceCalculator();
      		var dateTimeProviderStub = new Mock<IDateTimeProvider>();
      		dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Tuesday);

      		var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

      		Assert.Equals(1, actual);
      	}
      	```

# Quality Assurance and Testing with `Chaijs` for nodejs
## Test if a Variable or Function is Defined

```javascript
/** 2 - Use assert.isDefined() or assert.isUndefined() to make the tests pass. **/
test("#isDefined, #isUndefined", function () {
  assert.isDefined(null, "null is not undefined");
  assert.isUndefined(undefined, "undefined IS undefined");
  assert.isDefined("hello", "a string is not undefined");
});
````

## Use Assert.isOK and Assert.isNotOK

```javascript
/** 3 - Use assert.isOk() or assert.isNotOk() to make the tests pass. **/
// .isOk(truthy) and .isNotOk(falsey) will pass
test("#isOk, #isNotOk", function () {
  assert.isNotOk(null, "null is falsey");
  assert.isOk("I'm truthy", "a string is truthy");
  assert.isOk(true, "true is truthy");
});
```

## Test for Truthiness

- isTrue() will test for the boolean value true and isNotTrue() will pass when given anything but the boolean value of true.

```javascript
assert.isTrue(true, 'this will pass with the boolean value true');
assert.isTrue('true', 'this will NOT pass with the string value 'true');
assert.isTrue(1, 'this will NOT pass with the number value 1');
```

- isFalse() and isNotFalse() also exist, and behave similarly to their true counterparts except they look for the boolean value of false.

## Use the Double Equals to Assert Equality

```javascript
/** 5 - .equal(), .notEqual() **/
// .equal() compares objects using '=='
test("#equal, #notEqual", function () {
  assert.equal(12, "12", "numbers are coerced into strings with == ");
  assert.notEqual({ value: 1 }, { value: 1 }, "== compares object references");
  assert.equal(6 * "2", "12", "no more hints...");
  assert.notEqual(6 + "2", "12", "type your error message if you want");
});
```

## Use the Triple Equals to Assert Strict Equality

- strictEqual() compares objects using `===`.

```javascript
/** 6 - .strictEqual(), .notStrictEqual() **/
// .strictEqual() compares objects using '==='
test("#strictEqual, #notStrictEqual", function () {
  assert.notStrictEqual(6, "6");
  assert.strictEqual(6, 3 * 2);
  assert.strictEqual(6 * "2", 12);
  assert.notStrictEqual([1, "a", {}], [1, "a", {}]);
});
```

## Assert Deep Equality with .deepEqual and .notDeepEqual

```javascript
/** 7 - .deepEqual(), .notDeepEqual() **/
// .deepEqual() asserts that two object are deep equal
test("#deepEqual, #notDeepEqual", function () {
  assert.deepEqual(
    { a: "1", b: 5 },
    { b: 5, a: "1" },
    "keys order doesn't matter"
  );
  assert.notDeepEqual(
    { a: [5, 6] },
    { a: [6, 5] },
    "array elements position does matter !!"
  );
});
```

## Compare the Properties of Two Elements

- `isAbove()` compares if the first parameter is greater than the second `(a > b)`
- `isAtMost()` compares if the first parameter is equal to or less than the second `(a <= b)`

```javascript
/** 8 - .isAbove() => a > b , .isAtMost() => a <= b **/
test("#isAbove, #isAtMost", function () {
  assert.isAtMost("hello".length, 5);
  assert.isAbove(1, 0);
  assert.isAbove(Math.PI, 3);
  assert.isAtMost(1 - Math.random(), 1);
});
```

## Test if One Value is Below or At Least as Large as Another

- `isBelow()` compares if the first parameter is less than the second `(a < b)`.
- `isAtLeast()` compares if the first parameter is equal to or less than the second `(a >= b)`.

```javascript
/** 9 - .isBelow() => a < b , .isAtLeast =>  a >= b **/
test("#isBelow, #isAtLeast", function () {
  assert.isAtLeast("world".length, 5);
  assert.isAtLeast(2 * Math.random(), 0);
  assert.isBelow(5 % 2, 2);
  assert.isBelow(2 / 3, 1);
});
```

## Test if a Value Falls within a Specific Range

- `approximately()` requires a range to make the tests pass.
- The expected value for both tests is currently 1, so you need to find a range that allows for all values to be accounted for.

```javascript
/** 10 - .approximately **/
// .approximately(actual, expected, range, [message])
// actual = expected +/- range
// Choose the minimum range (3rd parameter) to make the test always pass
// it should be less than 1
test("#approximately", function () {
  assert.approximately(weirdNumbers(0.5), 1, /*edit this*/ 0.5);
  assert.approximately(weirdNumbers(0.2), 1, /*edit this*/ 0.8);
});
```

## Test if a Value is an Array

- The lines in the test should be changed from `assert.fail()` to either `assert.isArray()` or `assert.isNotArray()`.

```javascript
/** 11 - #isArray vs #isNotArray **/
test("#isArray, #isNotArray", function () {
  assert.isArray(
    "isThisAnArray?".split(""),
    "String.prototype.split() returns an Array"
  );
  assert.isNotArray([1, 2, 3].indexOf(2), "indexOf returns a number.");
});
```

## Test if an Array Contains an Item

```javascript
/** 12 - #include vs #notInclude **/
test("Array #include, #notInclude", function () {
  assert.notInclude(winterMonths, "jul", "It's summer in july...");
  assert.include(backendLanguages, "javascript", "JS is a backend language !!");
});
```

## Test if a Value is a String

```javascript
/** 13 - #isString asserts that the actual value is a string. **/
test("#isString, #isNotString", function () {
  assert.isNotString(Math.sin(Math.PI / 4), "a float is not a string");
  assert.isString(process.env.PATH, "env vars are strings (or undefined)");
  assert.isString(JSON.stringify({ type: "object" }), "a JSON is a string");
});
```

## Test if an Object has a Property

```javascript
/** 16 - #property asserts that the actual object has a given property. **/
// Use #property or #notProperty where appropriate
test("#property, #notProperty", function () {
  assert.notProperty(myCar, "wings", "A car has not wings");
  assert.property(airlinePlane, "engines", "planes have engines");
  assert.property(myCar, "wheels", "Cars have wheels");
});
```

## Test if a Value is of a Specific Data Structure Type

```javascript
test("#typeof, #notTypeOf", function () {
  /** 17 #typeOf asserts that value’s type is the given string, **/
  // as determined by Object.prototype.toString.
  // Use #typeOf or #notTypeOf where appropriate
  assert.typeOf(myCar, "object");
  assert.typeOf(myCar.model, "string");
  assert.notTypeOf(airlinePlane.wings, "string");
  assert.typeOf(airlinePlane.engines, "array");
  assert.typeOf(myCar.wheels, "number");
});
```

## Test if an Object is an Instance of a Constructor

```javascript
test("#instanceOf, #notInstanceOf", function () {
  /** 18 #instanceOf asserts that an object is an instance of a constructor **/
  // Use #instanceOf or #notInstanceOf where appropriate
  assert.notInstanceOf(myCar, Plane);
  assert.instanceOf(airlinePlane, Plane);
  assert.instanceOf(airlinePlane, Object, "everything is an Object");
  assert.notInstanceOf(myCar.wheels, String);
});
```

# Zombie.JS

- Zombie.js is a lightweight framework for testing client-side JavaScript code in a simulated environment. No browser required.
- You can use Zombie.js to create a set of tests; these tests `load, query, manipulate`, and provide inputs to any given web page. Given that Zombie.js simulates a browser and does not depend on the actual rendering of the HTML page, the tests run much faster than they would if you instrumented a real browser

```javascript
const Browser = require("zombie");

// We're going to make requests to http://example.com/signup
// Which will be routed to our test server localhost:3000
Browser.localhost("example.com", 3000);

describe("User visits signup page", function () {
  const browser = new Browser();

  before(function (done) {
    browser.visit("/signup", done);
  });

  describe("submits form", function () {
    before(function (done) {
      browser
        .fill("email", "zombie@underworld.dead")
        .fill("password", "eat-the-living")
        .pressButton("Sign Me Up!", done);
    });

    it("should be successful", function () {
      browser.assert.success();
    });

    it("should see welcome page", function () {
      browser.assert.text("title", "Welcome To Brains Depot");
    });
  });
});
```

## Simulate Actions Using a Headless Browser

- A headless browser is a web browser without a graphical user interface. This kind of tool is particularly useful for `testing web pages`, as it is able to render and understand HTML, CSS, and JavaScript the same way a browser would.

F- or these challenges we are using `Zombie.JS`. It's a lightweight browser which is totally based on JS, without relying on additional binaries to be installed. This feature makes it usable in an environment such as Repl.it. There are many other (more powerful) options.

- Mocha allows you to prepare the ground running some code before the actual tests. This can be useful for example to create items in the database, which will be used in the successive tests.

W- ith a headless browser, before the actual testing, we need to visit the page we are going to inspect. The suiteSetup 'hook' is executed only once at the suite startup. Other different hook types can be executed before each test, after each test, or at the end of a suite. See the Mocha docs for more information.

- Within tests/2_functional-tests.js, immediately after the Browser declaration, add your project URL to the site property of the variable:

```javascript
Browser.site = "https://sincere-cone.gomix.me"; // Your URL here
```

- If you are testing on a local environment replace the line above with

```javascript
Browser.localhost("example.com", process.env.PORT || 3000);
```

- Within tests/2_functional-tests.js, at the root level of the 'Functional Tests with Zombie.js' suite, instantiate a new instance of the Browser object with the following code:

```javascript
const browser = new Browser();
```

- Then, use the suiteSetup hook to direct the browser to the / route with the following code:

```javascript
suiteSetup(function (done) {
  return browser.visit("/", done);
});
```

## Run Functional Tests using a Headless Browser

- In the HTML main view we provided a input form. It sends data to the PUT /travellers endpoint that we used above with an Ajax request. When the request successfully completes, the client code appends a <div> containing the info returned by the call to the DOM. Here is an example of how to interact with this form:

```javascript
test('#test - submit the input "surname" : "Polo"', function (done) {
  browser.fill('surname', 'Polo').pressButton('submit', function () {
    browser.assert.success();
    browser.assert.text('span#name', 'Marco');
    browser.assert.text('span#surname', 'Polo');
    browser.assert.element('span#dates', 1);
    done();
  });
}
```

- First, the fill method of the browser object fills the surname field of the form with the value 'Polo'. Immediately after, the pressButton method invokes the submit event listener of the form. The pressButton method is asynchronous.

- Then, once a response is received from the AJAX request, a few assertions are made confirming:

  - The status of the response is 200
  - The text within the <span id='name'></span> element matches 'Marco'
  - The text within the <span id='surname'></span> element matches 'Polo'
  - The there is 1 <span id='dates'></span> element.
  - Finally, the done callback is invoked, which is needed due to the asynchronous test.

- Within tests/2_functional-tests.js, in the 'submit "surname" : "Colombo" - write your e2e test...' test (// #5), automate filling-in and submitting the form:

  - Fill in the form
  - Submit it pressing 'submit' button.

- Within the callback:

  - assert that status is OK 200
  - assert that the text inside the element span#name is 'Cristoforo'
  - assert that the text inside the element span#surname is 'Colombo'
  - assert that the element(s) span#dates exist and their count is 1

- Do not forget to to remove the assert.fail() call.

```javascript
test('submit "surname" : "Colombo" - write your e2e test...', function (done) {
  // fill the form...
  // then submit it pressing 'submit' button.
  //
  // in the callback...
  // assert that status is OK 200
  // assert that the text inside the element 'span#name' is 'Cristoforo'
  // assert that the text inside the element 'span#surname' is 'Colombo'
  // assert that the element(s) 'span#dates' exist and their count is 1
  browser.fill("surname", "Colombo").pressButton("submit", function () {
    /** YOUR TESTS HERE, Don't forget to remove assert.fail() **/

    // pressButton is Async.  Waits for the ajax call to complete...

    // assert that status is OK 200
    browser.assert.success();
    // assert that the text inside the element 'span#name' is 'Cristoforo'
    browser.assert.text("span#name", "Cristoforo");
    // assert that the text inside the element 'span#surname' is 'Colombo'
    browser.assert.text("span#surname", "Colombo");
    // assert that the element(s) 'span#dates' exist and their count is 1
    browser.assert.element("span#dates", 1);

    done(); // It's an async test, so we have to call 'done()''
  });
});
```

## Run Functional Tests Using a Headless Browser II

```javascript
test('submit "surname" : "Vespucci" - write your e2e test...', function (done) {
  // fill the form, and submit.
  browser.fill("surname", "Vespucci").pressButton("submit", function () {
    // assert that status is OK 200
    browser.assert.success();
    // assert that the text inside the element 'span#name' is 'Amerigo'
    browser.assert.text("span#name", "Amerigo");
    // assert that the text inside the element 'span#surname' is 'Vespucci'
    browser.assert.text("span#surname", "Vespucci");
    // assert that the element(s) 'span#dates' exist and their count is 1
    browser.assert.element("span#dates", 1);

    done();
  });
});
```

# References:

- https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices
- zombiejs : https://hub.packtpub.com/getting-started-zombiejs/
