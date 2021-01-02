## Verify an Object's Constructor with instanceof

- Anytime a constructor function creates a new object, that object is said to be an instance of its constructor. JavaScript gives a convenient way to verify this with the instanceof operator.
- `instanceof` allows you to compare an object to a constructor, returning `true or false` based on whether or not that object was created with the constructor. Here's an example:

```javascript
let Bird = function (name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
};

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // => true
```

- If an object is created without using a constructor, instanceof will verify that it is not an instance of that constructor:

```javascript
let canary = {
  name: "Mildred",
  color: "Yellow",
  numLegs: 2,
};

canary instanceof Bird; // => false
```

## Understand Own Properties

- The Bird constructor defines two properties: name and numLegs:

```javascript
function Bird(name) {
  this.name = name;
  this.numLegs = 2;
}

let duck = new Bird("Donald");
let canary = new Bird("Tweety");
```

- name and numLegs are called own properties, because they are defined directly on the instance object. That means that duck and canary each has its own separate copy of these properties. In fact every instance of Bird will have its own copy of these properties. The following code adds all of the own properties of duck to the array ownProps:

```javascript
let ownProps = [];

for (let property in duck) {
  if (duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}

console.log(ownProps); // prints [ "name", "numLegs" ]
```

## Use Prototype Properties to Reduce Duplicate Code

- Since numLegs will probably have the same value for all instances of Bird, you essentially have a duplicated variable numLegs inside each Bird instance.

- This may not be an issue when there are only two instances, but imagine if there are millions of instances. That would be a lot of duplicated variables.

- A better way is to use `Bird’s prototype`. Properties in the prototype are shared among ALL instances of Bird. Here's how to add numLegs to the Bird prototype:

```javascript
Bird.prototype.numLegs = 2;
```

- Now all instances of Bird have the numLegs property.

```javascript
console.log(duck.numLegs); // prints 2
console.log(canary.numLegs); // prints 2
```

- Since all instances automatically have the properties on the prototype, think of a prototype as a `recipe` for creating objects. Note that the prototype for duck and canary is part of the Bird constructor as Bird.prototype. Nearly every object in JavaScript has a prototype property which is part of the constructor function that created it.

## Change the Prototype to a New Object

- Up until now you have been adding properties to the prototype individually:

```javascript
Bird.prototype.numLegs = 2;
```

- This becomes tedious after more than a few properties.

```javascript
Bird.prototype.eat = function () {
  console.log("nom nom nom");
};

Bird.prototype.describe = function () {
  console.log("My name is " + this.name);
};
```

- A more efficient way is to set the prototype to a new object that already contains the properties. This way, the properties are added all at once:

```javascript
Bird.prototype = {
  numLegs: 2,
  eat: function () {
    console.log("nom nom nom");
  },
  describe: function () {
    console.log("My name is " + this.name);
  },
};
```

## Remember to Set the Constructor Property when Changing the Prototype

= There is one `crucial side effect` of manually setting the prototype to a new object. It erases the constructor property! This property can be used to check which constructor function created the instance, but since the property has been overwritten, it now gives false results:

```javascript
duck.constructor === Bird; // false -- Oops
duck.constructor === Object; // true, all objects inherit from Object.prototype
duck instanceof Bird; // true, still works
```

- To fix this, whenever a prototype is manually set to a new object, remember to define the constructor property:

```javascript
Bird.prototype = {
  constructor: Bird, // define the constructor property
  numLegs: 2,
  eat: function () {
    console.log("nom nom nom");
  },
  describe: function () {
    console.log("My name is " + this.name);
  },
};
```

## Understand Where an Object’s Prototype Comes From

- Just like people inherit genes from their parents, an object inherits its prototype directly from the constructor function that created it. For example, here the Bird constructor creates the duck object:

```javascript
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald");
```

- duck inherits its prototype from the Bird constructor function. You can show this relationship with the isPrototypeOf method:

```javascript
Bird.prototype.isPrototypeOf(duck);
// returns true
```

## Inherit Behaviors from a Supertype
- In the previous challenge, you created a supertype called Animal that defined behaviors shared by all animals:
```javascript
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
```
- This and the next challenge will cover how to reuse Animal's methods inside Bird and Dog without defining them again. It uses a technique called inheritance. This challenge covers the first step: make an instance of the supertype (or parent). You already know one way to create an instance of Animal using the new operator:
```javascript
let animal = new Animal();
```
- There are some disadvantages when using this syntax for inheritance, which are too complex for the scope of this challenge. Instead, here's an alternative approach without those disadvantages:
```javascript
let animal = Object.create(Animal.prototype);
```
- Object.create(obj) creates a new object, and sets obj as the new object's prototype. Recall that the prototype is like the "recipe" for creating an object. By setting the prototype of animal to be Animal's prototype, you are effectively giving the animal instance the same "recipe" as any other instance of Animal.
```javascript
animal.eat(); // prints "nom nom nom"
animal instanceof Animal; // => true
```
##  Set the Child's Prototype to an Instance of the Parent
- In the previous challenge you saw the first step for inheriting behavior from the supertype (or parent) Animal: making a new instance of Animal.

- This challenge covers the next step: set the prototype of the subtype (or child)—in this case, Bird—to be an instance of Animal.
```javascript
Bird.prototype = Object.create(Animal.prototype);
```
- Remember that the prototype is like the "recipe" for creating an object. In a way, the recipe for Bird now includes all the key "ingredients" from Animal.
```javascript
let duck = new Bird("Donald");
duck.eat(); // prints "nom nom nom"
```
- duck inherits all of Animal's properties, including the eat method.

## Use a Mixin to Add Common Behavior Between Unrelated Objects
- As you have seen, behavior is shared through inheritance. However, there are cases when inheritance is not the best solution. Inheritance does not work well for unrelated objects like Bird and Airplane. They can both fly, but a Bird is not a type of Airplane and vice versa.

- For unrelated objects, it's better to use mixins. A mixin allows other objects to use a collection of functions.
```javascript
let flyMixin = function(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  }
};
```
- The flyMixin takes any object and gives it the fly method.
```javascript
let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
```
- Here bird and plane are passed into flyMixin, which then assigns the fly function to each object. Now bird and plane can both fly:
```javascript
bird.fly(); // prints "Flying, wooosh!"
plane.fly(); // prints "Flying, wooosh!"
```
- Note how the mixin allows for the same fly method to be reused by unrelated objects bird and plane.