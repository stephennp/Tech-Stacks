# Intro

- MongoDB is a database that stores data records (documents) for use by an application. Mongo is a non-relational, "NoSQL" database. This means Mongo stores all associated data within one record, instead of storing it across many preset tables as in a SQL database. Some benefits of this storage model are:

  - Scalability: by default, non-relational databases are split (or "shared") across many systems instead of only one. This makes it easier to improve performance at a lower cost.
  - Flexibility: new datasets and properties can be added to a document without the need to make a new table for that data.
  - Replication: copies of the database run in parallel so if one goes down, one of the copies becomes the new primary data source.

- While there are many non-relational databases, Mongo's use of JSON as its document storage structure makes it a logical choice when learning backend JavaScript. Accessing documents and their properties is like accessing objects in JavaScript.

- Mongoose.js is an npm module for Node.js that allows you to write objects for Mongo as you would in JavaScript. This can make it easier to construct documents for storage in Mongo.

## Install and Set Up Mongoose

- In this challenge, you will import the required projects, and connect to your Atlas database.

- Add mongodb and mongoose to the project’s package.json. Then, require mongoose as mongoose in myApp.js. Store your MongoDB Atlas database URI in a private .env file as MONGO_URI. Surround the the URI with single or double quotes, and make sure no space exists between both the variable and the =, and the value and =. Connect to the database using the following syntax:

```javascript
mongoose.connect(<Your URI>, { useNewUrlParser: true, useUnifiedTopology: true });
```

## Create a Model

- CRUD Part I - CREATE

- First of all we need a Schema. Each schema maps to a MongoDB collection. It defines the shape of the documents within that collection. Schemas are building block for Models. They can be nested to create complex models, but in this case we'll keep things simple. A model allows you to create instances of your objects, called documents.

- Repl.it is a real server, and in real servers the interactions with the database happen in handler functions. These functions are executed when some event happens (e.g. someone hits an endpoint on your API). We’ll follow the same approach in these exercises. The done() function is a callback that tells us that we can proceed after completing an asynchronous operation such as inserting, searching, updating, or deleting. It's following the Node convention, and should be called as done(null, data) on success, or done(err) on error.

- Warning - When interacting with remote services, errors may occur!

```javascript
/* Example */

const someFunc = function (done) {
  //... do something (risky) ...
  if (error) return done(error);
  done(null, result);
};
```

- Create a person schema called personSchema having this prototype:

- Person Prototype -

---

name : string [required]
age : number
favoriteFoods : array of strings (\*)

## Create and Save a Record of a Model

- In this challenge you will have to create and save a record of a model.

- Within the createAndSavePerson function, create a document instance using the Person model constructor you built before. Pass to the constructor an object having the fields name, age, and favoriteFoods. Their types must conform to the ones in the personSchema. Then, call the method document.save() on the returned document instance. Pass to it a callback using the Node convention. This is a common pattern; all the following CRUD methods take a callback function like this as the last argument.

```javascript
/* Example */

// ...
person.save(function (err, data) {
  //   ...do your stuff here...
});
```

## Create Many Records with model.create()

- Sometimes you need to create many instances of your models, e.g. when seeding a database with initial data. Model.create() takes an array of objects like [{name: 'John', ...}, {...}, ...] as the first argument, and saves them all in the db.

- Modify the createManyPeople function to create many people using Model.create() with the argument arrayOfPeople.

```javascript
/** 1) Install & Set up mongoose */
const mongoose = require("mongoose");
mongoose.connect(process.env.MONGO_URI);

/** 2) Create a 'Person' Model */
var personSchema = new mongoose.Schema({
  name: String,
  age: Number,
  favoriteFoods: [String],
});

/** 3) Create and Save a Person */
var Person = mongoose.model("Person", personSchema);

var createAndSavePerson = function (done) {
  var janeFonda = new Person({
    name: "Jane Fonda",
    age: 84,
    favoriteFoods: ["vodka", "air"],
  });

  janeFonda.save(function (err, data) {
    if (err) return console.error(err);
    done(null, data);
  });
};

/** 4) Create many People with `Model.create()` */
var arrayOfPeople = [
  { name: "Frankie", age: 74, favoriteFoods: ["Del Taco"] },
  { name: "Sol", age: 76, favoriteFoods: ["roast chicken"] },
  { name: "Robert", age: 78, favoriteFoods: ["wine"] },
];

var createManyPeople = function (arrayOfPeople, done) {
  Person.create(arrayOfPeople, function (err, people) {
    if (err) return console.log(err);
    done(null, people);
  });
};
```

## Use model.find() to Search Your Database

- In its simplest usage, Model.find() accepts a query document (a JSON object) as the first argument, then a callback. It returns an array of matches. It supports an extremely wide range of search options. Read more in the docs.

- Modify the findPeopleByName function to find all the people having a given name, using Model.find() -> [Person]

- Use the function argument personName as the search key.

```javascript
/** 1) Install & Set up mongoose */
const mongoose = require("mongoose");
mongoose.connect(process.env.MONGO_URI);

/** 2) Create a 'Person' Model */
var personSchema = new mongoose.Schema({
  name: String,
  age: Number,
  favoriteFoods: [String],
});

/** 3) Create and Save a Person */
var Person = mongoose.model("Person", personSchema);

var createAndSavePerson = function (done) {
  var janeFonda = new Person({
    name: "Jane Fonda",
    age: 84,
    favoriteFoods: ["vodka", "air"],
  });

  janeFonda.save(function (err, data) {
    if (err) return console.error(err);
    done(null, data);
  });
};

/** 4) Create many People with `Model.create()` */
var arrayOfPeople = [
  { name: "Frankie", age: 74, favoriteFoods: ["Del Taco"] },
  { name: "Sol", age: 76, favoriteFoods: ["roast chicken"] },
  { name: "Robert", age: 78, favoriteFoods: ["wine"] },
];

var createManyPeople = function (arrayOfPeople, done) {
  Person.create(arrayOfPeople, function (err, people) {
    if (err) return console.log(err);
    done(null, people);
  });
};

/** 5) Use `Model.find()` */
var findPeopleByName = function (personName, done) {
  Person.find({ name: personName }, function (err, personFound) {
    if (err) return console.log(err);
    done(null, personFound);
  });
};
```

## Perform New Updates on a Document Using model.findOneAndUpdate()

- Recent versions of Mongoose have methods to simplify documents updating. Some more advanced features (i.e. pre/post hooks, validation) behave differently with this approach, so the classic method is still useful in many situations. findByIdAndUpdate() can be used when searching by id.

- Modify the findAndUpdate function to find a person by Name and set the person's age to 20. Use the function parameter personName as the search key.

-Note: You should return the updated document. To do that, you need to pass the options document { new: true } as the 3rd argument to findOneAndUpdate(). By default, these methods return the unmodified object.

```javascript
const findAndUpdate = (personName, done) => {
  const ageToSet = 20;

  Person.findOneAndUpdate(
    { name: personName },
    { age: ageToSet },
    { new: true },
    (err, updatedDoc) => {
      if (err) return console.log(err);
      done(null, updatedDoc);
    }
  );
};
```

## Delete One Document Using model.findByIdAndRemove

- findByIdAndRemove and findOneAndRemove are like the previous update methods. They pass the removed document to the db. As usual, use the function argument personId as the search key.

- Modify the removeById function to delete one person by the person's \_id. You should use one of the methods findByIdAndRemove() or findOneAndRemove().

```javascript
var removeById = function (personId, done) {
  Person.findByIdAndRemove(personId, (err, removedDoc) => {
    if (err) return console.log(err);
    done(null, removedDoc);
  });
};
```

## Chain Search Query Helpers to Narrow Search Results

- If you don’t pass the callback as the last argument to Model.find() (or to the other search methods), the query is not executed. You can store the query in a variable for later use. This kind of object enables you to build up a query using chaining syntax. The actual db search is executed when you finally chain the method .exec(). You always need to pass your callback to this last method. There are many query helpers, here we'll use the most commonly used.

- Modify the queryChain function to find people who like the food specified by the variable named foodToSearch. Sort them by name, limit the results to two documents, and hide their age. Chain .find(), .sort(), .limit(), .select(), and then .exec(). Pass the done(err, data) callback to exec().

- create but not execute a find query

```javascript
Model.find({ name: "Leah" });
```

- To store the find query into a variable for later use:

```javascript
var findQuery = YourModel.find({ name: "Leah" });
```

- To sort an array:

```javascript
yourArray.sort({ age: 1 }); // Here: 1 for ascending	order and -1 for descending order.
```

- To limit an array’s size:

```javascript
yourArray.limit(5); // return array which has 5 items in it.
```

- To hide certain property from the result:

```javascript
yourArray.select({ name: 0, age: 1 }); // Here: 0 means false and thus hide name property; 1 means true so age property will show.
```

- To execute this query, you can either:

```javascript
YourQuery.exec(function (err, docs) {
  //do something here
});
```

Or

```javascript
Promise;
YourQuery.exec.then(function (err, docs) {
  //do something here
});
```

- Chain it all together:

```javascript
Person.find({ age: 55 })
  .sort({ name: -1 })
  .limit(5)
  .select({ favoriteFoods: 0 })
  .exec(function (error, people) {
    //do something here
  });
```
