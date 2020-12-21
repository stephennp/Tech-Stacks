# Intro

## Singleton VS Static Class
- Both static class and singleton class can have only one instance of a copy that is available in memory throughout the whole application. They both are used for holding the global state of an application.
- Both static classes and singleton classes can be implemented as thread-safe.
- What are the differences between Singleton vs Static class in C#?
  - We `cannot` create an instance of a static class in C#. But we can create a single instance of a singleton class and then can reuse that singleton instance.
  - When the compiler compiles the static class then internally it treats the static class as an `abstract and sealed class`. This is the reason why `neither we create an instance nor extend a static class` in C#.
  - The Singleton class constructor is always marked as `private`. This is the reason why we cannot create an instance from outside the singleton class. It provides either `public static property or a public static method` whose job is to create the singleton instance only once and then return that singleton instance each and every time when we called that public static property/method from outside the singleton class.
  - `A Singleton class` can be `initialized lazily or can be loaded automatically by CLR` (Common Language Runtime) when the program or namespace containing the Singleton class is loaded. Whereas a `static class` is generally initialized when it is `first loaded for the first time and it may lead to potential classloader issues`.
  - It is `not possible` to pass the `static` class as a method `parameter` whereas we can pass the `singleton instance as a method parameter` in C#.
  - In C#, it is `possible` to implement `interfaces, inherit from other classes and allow inheritance with Singleton class`. These are `not` possible with a `static` class. So the Singleton class is more flexible as compared to static classes.
  - We `can clone` the `Singleton` class object whereas it is `not possible` to clone a `static` class. It is possible to `dispose` of the objects of a `singleton` class whereas it is `not possible` to dispose of a `static` class.
  - We cannot implement the Dependency Injection design pattern using Static class because the static class is not interface driven.

## Compare two string ignoring case
- https://stackoverflow.com/questions/6371150/comparing-two-strings-ignoring-case-in-c-sharp

## Overview of C# Async Programming
- https://dzone.com/articles/overview-of-c-async-programming-with-thread-pools