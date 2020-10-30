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
	``` csharp
	var mockOrder = new MockOrder();
	var purchase = new Purchase(mockOrder);

	purchase.ValidateOrders();

	Assert.True(purchase.CanBeShipped);
	```
	- Better
	``` csharp
	var stubOrder = new FakeOrder();
	var purchase = new Purchase(stubOrder);

	purchase.ValidateOrders();

	Assert.True(purchase.CanBeShipped);
	```
	- Another better:
	``` csharp
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

Why?
	- Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.
	- Explicitly shows what you're trying to prove rather than trying to accomplish.
	- Bad:
		```csharp
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
			```csharp
			[Fact]
			public void Add_EdgeCases_ThrowsArgumentExceptions()
			{
				Assert.Throws<ArgumentException>(() => stringCalculator.Add(null));
				Assert.Throws<ArgumentException>(() => stringCalculator.Add("a"));
			}
			```
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
## References:
- https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices