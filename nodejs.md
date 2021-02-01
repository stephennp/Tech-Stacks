# Intro

- Node.js is a JavaScript runtime that allows developers to write backend (server-side) programs in JavaScript. Node.js comes with a handful of built-in modules - small, independent programs - that help facilitate this purpose. Some of the core modules include:

  - HTTP: a module that acts as a server
  - File System: a module that reads and modifies files
  - Path: a module for working with directory and file paths
  - Assertion Testing: a module that checks code against prescribed constraints
  - Express, while not included with Node.js, is another module often used with it. Express runs between the server created by Node.js and the frontend pages of a web application. Express also handles an application's routing. Routing directs users to the correct page based on their interaction with the application. While there are alternatives to using Express, its simplicity makes it a good place to begin when learning the interaction between a backend powered by Node.js and the frontend.

## Start a Working Express Server

- In the first two lines of the file myApp.js, you can see how easy it is to create an Express app object. This object has several methods, and you will learn many of them in these challenges. One fundamental method is `app.listen(port)`. It tells your server to listen on a given port, putting it in running state. For testing reasons, we need the app to be running in the background so we added this method in the server.js file for you.

- Let’s serve our first string! In Express, routes takes the following structure: app.METHOD(PATH, HANDLER). METHOD is an http method in lowercase. PATH is a relative path on the server (it can be a string, or even a regular expression). HANDLER is a function that Express calls when the route is matched. Handlers take the form function(req, res) {...}, where req is the request object, and res is the response object. For example, the handler

```javascript
function(req, res) {
  res.send('Response String');
}
```

will serve the string 'Response String'.

- Use the `app.get()` method to serve the string "Hello Express" to GET requests matching the `/` (root) path. Be sure that your code works by looking at the logs, then see the results in the preview if you are using Repl.it.

Note: All the code for these lessons should be added in between the few lines of code we have started you off with.

## Serve an HTML File

You can respond to requests with a file using the res.sendFile(path) method. You can put it inside the app.get('/', ...) route handler. Behind the scenes, this method will set the appropriate headers to instruct your browser on how to handle the file you want to send, according to its type. Then it will read and send the file. This method needs an absolute file path. We recommend you to use the Node global variable `\_\_dirname` to calculate the path like this:

absolutePath = \_\_dirname + relativePath/file.ext
Send the /views/index.html file as a response to GET requests to the / path. If you view your live app, you should see a big HTML heading (and a form that we will use later…), with no style applied.

Note: You can edit the solution of the previous challenge or create a new one. If you create a new solution, keep in mind that Express evaluates routes from top to bottom, and executes the handler for the first match. You have to comment out the preceding solution, or the server will keep responding with a string.

```javascript
var express = require("express");
var app = express();

app.get("/", function (req, res) {
  res.sendFile(__dirname + "/views/index.html");
});

module.exports = app;
```

## Serve Static Assets

- Serving static webpages and assets is fairly simple with express. This could be useful for building your own portfolio website or blog, single-page web applications etc.

- To serve static assets from the public folder you can use the express.static() method as the middleware. This method takes the endpoint and the absolute path to the directory containing the static assets as arguments and exposes the files in that folder at the given endpoint. By default, if the endpoint is not passed to the method, the folder is exposed at the root endpoint i.e. `/` for the application.

- The `__dirname` variable is a string containing the absolute path to the root of your project which has to be concatenated with the folder containing the assets.

- Add the following line to your file above all defined routes to achieve the desired result:

```javascript
// Normal usage
app.use(express.static(__dirname + "/public"));

// Assets at the /assets route
app.use("/assets", express.static(__dirname + "/public"));
```

## Serve JSON on a Specific Route

- It is rather simple to serve a JSON object with Node (at the /json route), if we want to deliver an object containing a key message and with the value "Hello json" we can do so as indicated:

```javascript
app.get("/json", (req, res) => {
  res.json({
    message: "Hello json",
  });
});
```

## Use the .env File

- The `.env` file is a hidden file that is used to pass environment variables to your application. This file is secret, no one but you can access it, and it can be used to store data that you want to keep private or hidden. For example, you can store API keys from external services or your database URI. You can also use it to store configuration options. By setting configuration options, you can change the behavior of your application, without the need to rewrite some code.

- The environment variables are accessible from the app as `process.env.VAR_NAME`. The `process.env` object is a global Node object, and variables are passed as strings. By convention, the variable names are all uppercase, with words separated by an underscore. The .env is a shell file, so you don’t need to wrap names or values in quotes. It is also important to note that there cannot be space around the equals sign when you are assigning values to your variables, e.g. VAR_NAME=value. Usually, you will put each variable definition on a separate line.

- Let's add an environment variable as a configuration option.

- Store the variable `MESSAGE_STYLE=uppercase` in the `.env` file. Then tell the GET `/json` route handler that you created in the last challenge to transform the response object’s message to uppercase if process.env.MESSAGE_STYLE equals uppercase. The response object should become {"message": "HELLO JSON"}.

```javascript
if (process.env.VAR_NAME === "allCaps") {
  response = "Hello World".toUpperCase();
} else {
  response = "Hello World";
}
```

## Implement a Root-Level Request Logger Middleware

- Earlier, you were introduced to the express.static() middleware function. Now it’s time to see what middleware is, in more detail. Middleware functions are functions that take 3 arguments: the request object, the response object, and the next function in the application’s request-response cycle. These functions execute some code that can have side effects on the app, and usually add information to the request or response objects. They can also end the cycle by sending a response when some condition is met. If they don’t send the response when they are done, they start the execution of the next function in the stack. This triggers calling the 3rd argument, next().

- Look at the following example:

```javascript
function(req, res, next) {
  console.log("I'm a middleware...");
  next();
}
```

- Let’s suppose you mounted this function on a route. When a request matches the route, it displays the string “I’m a middleware…”, then it executes the next function in the stack. In this exercise, you are going to build root-level middleware. As you have seen in challenge 4, to mount a middleware function at root level, you can use the app.use(<mware-function>) method. In this case, the function will be executed for all the requests, but you can also set more specific conditions. For example, if you want a function to be executed only for POST requests, you could use app.post(<mware-function>). Analogous methods exist for all the HTTP verbs (GET, DELETE, PUT, …).

- Build a simple logger. For every request, it should log to the console a string taking the following format: method path - ip. An example would look like this: GET /json - ::ffff:127.0.0.1. Note that there is a space between method and path and that the dash separating path and ip is surrounded by a space on both sides. You can get the request method (http verb), the relative route path, and the caller’s ip from the request object using req.method, req.path and req.ip. Remember to call next() when you are done, or your server will be stuck forever. Be sure to have the ‘Logs’ opened, and see what happens when some request arrives.

- Note: Express evaluates functions in the order they appear in the code. This is true for middleware too. If you want it to work for all the routes, it should be mounted before them.

- To set up your own middleware you can do it like so:

```javascript
app.use(function middleware(req, res, next) {
  // Do something
  // Call the next function in line:
  next();
});
```

## Get Route Parameter Input from the Client

- When building an API, we have to allow users to communicate to us what they want to get from our service. For example, if the client is requesting information about a user stored in the database, they need a way to let us know which user they're interested in. One possible way to achieve this result is by using route parameters. Route parameters are named segments of the URL, delimited by slashes (/). Each segment captures the value of the part of the URL which matches its position. The captured values can be found in the req.params object.

route_path: '/user/:userId/book/:bookId'
actual_request_URL: '/user/546/book/6754'
req.params: {userId: '546', bookId: '6754'}
Build an echo server, mounted at the route GET /:word/echo. Respond with a JSON object, taking the structure {echo: word}. You can find the word to be repeated at req.params.word. You can test your route from your browser's address bar, visiting some matching routes, e.g. your-app-rootpath/freecodecamp/echo.

## Chain Middleware to Create a Time Server

- Middleware can be mounted at a specific route using app.METHOD(path, middlewareFunction). Middleware can also be chained inside route definition.

- Look at the following example:

```javascript
app.get(
  "/user",
  function (req, res, next) {
    req.user = getTheUserSync(); // Hypothetical synchronous operation
    next();
  },
  function (req, res) {
    res.send(req.user);
  }
);
```

- This approach is useful to split the server operations into smaller units. That leads to a better app structure, and the possibility to reuse code in different places. This approach can also be used to perform some validation on the data. At each point of the middleware stack you can block the execution of the current chain and pass control to functions specifically designed to handle errors. Or you can pass control to the next matching route, to handle special cases. We will see how in the advanced Express section.

## Get Route Parameter Input from the Client

- When building an API, we have to allow users to communicate to us what they want to get from our service. For example, if the client is requesting information about a user stored in the database, they need a way to let us know which user they're interested in. One possible way to achieve this result is by using route parameters. Route parameters are named segments of the URL, delimited by slashes (/). Each segment captures the value of the part of the URL which matches its position. The captured values can be found in the req.params object.

```javascript
route_path: '/user/:userId/book/:bookId'
actual_request_URL: '/user/546/book/6754'
req.params: {userId: '546', bookId: '6754'}
```

- Build an echo server, mounted at the route GET /:word/echo. Respond with a JSON object, taking the structure {echo: word}. You can find the word to be repeated at req.params.word. You can test your route from your browser's address bar, visiting some matching routes, e.g. your-app-rootpath/freecodecamp/echo.

```javascript
app.post("/:param1/:param2", (req, res) => {
  // Access the corresponding key in the req.params
  // object as defined in the endpoint
  var param1 = req.params.param1;
  // OR use destructuring to get multiple parameters
  var { param1, param2 } = req.params;
  // Send the req.params object as a JSON Response
  res.json(req.params);
});
```

## Get Query Parameter Input from the Client

- Another common way to get input from the client is by encoding the data after the route path, using a query string. The query string is delimited by a question mark `(?)`, and includes field=value couples.
- Each couple is separated by an ampersand `(&)`. Express can parse the data from the query string, and populate the object req.query.
- Some characters, like the percent (%), cannot be in URLs and have to be encoded in a different format before you can send them. If you use the API from JavaScript, you can use specific methods to `encode/decode` these characters.

```javascript
route_path: '/library'
actual_request_URL: '/library?userId=546&bookId=6754'
req.query: {userId: '546', bookId: '6754'}
```

```javascript
app.get("/name", function (req, res) {
  var firstName = req.query.first;
  var lastName = req.query.last;
  // OR you can destructure and rename the keys
  var { first: firstName, last: lastName } = req.query;
  // Use template literals to form a formatted string
  res.json({
    name: `${firstName} ${lastName}`,
  });
});
```

## Use body-parser to Parse POST Requests

- Besides GET, there is another common HTTP verb, it is POST. POST is the default method used to send client data with HTML forms. In REST convention, POST is used to send data to create new items in the database (a new user, or a new blog post). You don’t have a database in this project, but you are going to learn how to handle POST requests anyway.

- In these kind of requests, the data doesn’t appear in the URL, it is hidden in the request body. The body is a part of the HTTP request, also called the payload. Even though the data is not visible in the URL, this does not mean that it is private. To see why, look at the raw content of an HTTP POST request:

```javascript
POST /path/subpath HTTP/1.0
From: john@example.com
User-Agent: someBrowser/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 20

name=John+Doe&age=25
```

- As you can see, the body is encoded like the query string. This is the default format used by HTML forms. With Ajax, you can also use JSON to handle data having a more complex structure. There is also another type of encoding: multipart/form-data. This one is used to upload binary files. In this exercise, you will use a urlencoded body. To parse the data coming from POST requests, you have to install the body-parser package. This package allows you to use a series of middleware, which can decode data in different formats.

- Note: extended=false is a configuration option that tells the parser to use the classic encoding. When using it, values can be only `strings or arrays`. The extended version allows more data flexibility, but it is outmatched by JSON.
- The body-parser should already be added to your project if you used the provided boilerplate, but if not it should be there as:

```json
"dependencies": {
    "body-parser": "^1.19.0",

    "express": "^4.17.1"
}
```

- You can run npm install body-parser to add it as a dependency to your project instead of manually adding it to the package.json file.

- This guide assumes you have imported the body-parser module into your file as bodyParser.

- In order to import the same, you just need to add the following line at the top of your file:

```javascript
var bodyParser = require("body-parser");
```

- All you need to do for this challenge is pass the middleware to app.use(). Make sure it comes before the paths it needs to be used on. Remember that body-parser returns with bodyParser.urlencoded({extended: false}). Use the following as a template:

```javascript
app.use(bodyParser.urlencoded({ extended: false }));
```

- In order to parse JSON data sent in the POST request, use bodyParser.json() as the middleware as shown below:

```javascript
app.use(bodyParser.json());
```

- The data received in the request is available in the req.body object.

Do not forget that all these statements need to go above any routes that might have been defined.

## Set up a Template Engine (Pug)

- A template engine enables you to use static template files (such as those written in `Pug`) in your app. At runtime, the template engine replaces variables in a template file with actual values which can be supplied by your server. Then it transforms the template into a static HTML file that is sent to the client. This approach makes it easier to design an HTML page and allows for displaying variables on the page without needing to make an API call from the client.

- Add pug@~3.0.0 as a dependency in your package.json file.

- Express needs to know which template engine you are using. We will use the set method to assign pug as the view engine property's value: `app.set('view engine', 'pug')`

- Your page will not load until you correctly render the index file in the views/pug directory.

- Change the argument of the `res.render()` declaration in the / route to be the file path to the `views/pug` directory. The path can be a relative path (relative to views), or an absolute path, and does not require a file extension.

- If all went as planned, your app home page will stop showing the message "Pug template is not defined." and will now display a message indicating you've successfully rendered the Pug template!
- Note: The view engine cache does not cache the contents of the template’s output, only the underlying template itself. The view is still re-rendered with every request even when the cache is on.
- Install module `npm install pug --save`
- Create pug template file `index.pug`

```
html
  head
    title= title
  body
    h1= message
```

````javascript
// template engine with pug
app.set("view engine", "pug");
app.get("/template-engine", function (req, res) {
  res.render("index", { title: "Hey guy", message: "Hello there !!" });
});
```## Use a Template Engine's Powers

- One of the greatest features of using a template engine is being able to pass variables from the server to the template file before rendering it to HTML.

- In your Pug file, you're able to use a variable by referencing the variable name as #{variable_name} inline with other text on an element or by using an equal sign on the element without a space such as p=variable_name which assigns the variable's value to the p element's text.

- We strongly recommend looking at the syntax and structure of Pug here on GitHub's README. Pug is all about using whitespace and tabs to show nested elements and cutting down on the amount of code needed to make a beautiful site.

- Looking at our pug file 'index.pug' included in your project, we used the variables title and message.

- To pass those along from our server, you will need to add an object as a second argument to your res.render with the variables and their values. For example, pass this object along setting the variables for your index view: {title: 'Hello', message: 'Please login'}

- It should look like: res.render(process.cwd() + '/views/pug/index', {title: 'Hello', message: 'Please login'}); Now refresh your page and you should see those values rendered in your view in the correct spot as laid out in your index.pug file!

## Set up Passport

- It's time to set up Passport so we can finally start allowing a user to register or login to an account! In addition to Passport, we will use `Express-session` to handle sessions. Using this `middleware` saves the `session id` as a `cookie` in the client and allows us to access the session data using that `id` on the server. This way we keep personal account information out of the cookie used by the client to verify to our server they are authenticated and just keep the `key` to access the data `stored` on the `server`.

- To set up Passport for use in your project, you will need to add it as a dependency first in your package.json. `"passport": "^0.3.2"`

- In addition, add `Express-session` as a dependency now as well. Express-session has a ton of advanced features you can use but for now we're just going to use the basics! `"express-session": "^1.15.0"`

- You will need to set up the session settings now and initialize Passport. Be sure to first create the variables 'session' and 'passport' to require `'express-session'` and `'passport'` respectively.

- To set up your express app to use the session we'll define just a few basic options. Be sure to add `SESSION_SECRET` to your `.env` file and give it a random value. This is used to compute the hash used to encrypt your cookie!

```javascript
app.use(
  session({
    secret: process.env.SESSION_SECRET,
    resave: true,
    saveUninitialized: true,
    cookie: { secure: false },
  })
);
````

- As well you can go ahead and tell your express app to use 'passport.initialize()' and 'passport.session()'. (For example, app.use(passport.initialize());)

## Serialization and Deserialization of a User Object

- `Serialization and deserialization` are important concepts in regards to authentication. To serialize an object means to convert its contents into a small key that can then be deserialized into the original object. This is what allows us to know who has communicated with the server without having to send the authentication data, like the username and password, at each request for a new page.
- Serialization:

  - Determines which data of the user object should be stored in the session. The result of the serializeUser method is attached to the session as req.session.passport.user = {}.
  - Here for instance, it would be (as we provide the user id as the key) req.session.passport.user = {id: 'xyz'}

- To set this up properly, we need to have a serialize function and a deserialize function. In Passport, we create these with passport.`serializeUser( OURFUNCTION )` and `passport.deserializeUser( OURFUNCTION )`

- The serializeUser is called with 2 arguments, the full user object and a callback used by passport. A unique key to identify that user should be returned in the callback, the easiest one to use being the user's \_id in the object. It should be unique as it generated by MongoDB. Similarly, deserializeUser is called with that key and a callback function for passport as well, but, this time, we have to take that key and return the full user object to the callback. To make a query search for a Mongo \_id, you will have to create const ObjectID = require('mongodb').ObjectID;, and then to use it you call new ObjectID(THE_ID). Be sure to add MongoDB as a dependency. You can see this in the examples below:

```javascript
passport.serializeUser((user, done) => {
  done(null, user._id);
});

passport.deserializeUser((id, done) => {
  myDataBase.findOne({ _id: new ObjectID(id) }, (err, doc) => {
    done(null, null);
  });
});
```

- NOTE: This deserializeUser will throw an error until we set up the DB in the next step, so for now comment out the whole block and just call done(null, null) in the function deserializeUser.

## Implement the Serialization of a Passport User

- Right now, we're not loading an actual user object since we haven't set up our database. This can be done many different ways, but for our project we will connect to the database once when we start the server and keep a persistent connection for the full life-cycle of the app. To do this, add your database's connection string (for example: mongodb+srv://:@cluster0-jvwxi.mongodb.net/?retryWrites=true&w=majority) to the environment variable MONGO_URI. This is used in the connection.js file.

- You can set up a free database on MongoDB Atlas.

- Now we want to connect to our database then start listening for requests. The purpose of this is to not allow requests before our database is connected or if there is a database error. To accomplish this, you will want to encompass your serialization and your app routes in the following code:

```javascript
myDB(async (client) => {
  const myDataBase = await client.db("database").collection("users");

  // Be sure to change the title
  app.route("/").get((req, res) => {
    //Change the response to render the Pug template
    res.render("pug", {
      title: "Connected to Database",
      message: "Please login",
    });
  });

  // Serialization and deserialization here...

  // Be sure to add this...
}).catch((e) => {
  app.route("/").get((req, res) => {
    res.render("pug", { title: e, message: "Unable to login" });
  });
});
// app.listen out here...
```

- Be sure to uncomment the myDataBase code in deserializeUser, and edit your done(null

## Authentication Strategies

- A strategy is a way of authenticating a user. You can use a strategy for allowing users to authenticate based on locally saved information (if you have them register first) or from a variety of providers such as `Google or GitHub`.
- For this project, we will set up a local strategy. To see a list of the hundreds of strategies, visit Passport's site here.

- Add `passport-local` as a dependency and add it to your server as follows:

```javascript
const LocalStrategy = require("passport-local");
```

- Now you will have to tell passport to use an instantiated LocalStrategy object with a few settings defined. Make sure this (as well as everything from this point on) is encapsulated in the database connection since it relies on it!

```javascript
passport.use(
  new LocalStrategy(function (username, password, done) {
    myDataBase.findOne({ username: username }, function (err, user) {
      console.log("User " + username + " attempted to log in.");
      if (err) {
        return done(err);
      }
      if (!user) {
        return done(null, false);
      }
      if (password !== user.password) {
        return done(null, false);
      }
      return done(null, user);
    });
  })
);
```

- This is defining the process to use when we try to authenticate someone locally. First, it tries to find a user in our database with the username entered, then it checks for the password to match, then finally, if no errors have popped up that we checked for, like an incorrect password, the user's object is returned and they are authenticated.

- Many strategies are set up using different settings, but generally it is easy to set it up based on the README in that strategy's repository. A good example of this is the GitHub strategy where we don't need to worry about a username or password because the user will be sent to GitHub's auth page to authenticate. As long as they are logged in and agree then GitHub returns their profile for us to use.

## How to Use Passport Strategies

- In the `index.pug` file supplied, there is actually a login form.
- It has previously been hidden because of the inline JavaScript if showLogin with the form indented after it. Before showLogin as a variable was never defined, so it never rendered the code block containing the form. Go ahead and on the res.render for that page add a new variable to the object showLogin: true. When you refresh your page, you should then see the form! This form is set up to POST on `/login`, so this is where we should set up to accept the POST and authenticate the user.

- For this challenge you should add the route `/login` to accept a POST request. To authenticate on this route, you need to add a `middleware` to do so before then sending a response. This is done by just passing another argument with the middleware before your function(req,res) with your response! The middleware to use is `passport.authenticate('local')`.

- `passport.authenticate` can also take some options as an argument such as: `{ failureRedirect: '/' }` which is incredibly useful, so be sure to add that in as well. The response after using the middleware (which will only be called if the authentication middleware passes) should be to redirect the user to `/profile` and that route should render the view `profile.pug`.

- If the authentication was successful, the user object will be saved in req.user.

- At this point, if you enter a username and password in the form, it should redirect to the home page /, and the console of your server should display `User {USERNAME} attempted to log in.`, since we currently cannot login a user who isn't registered.

## Create New Middleware

- As is, any user can just go to `/profile` whether they have `authenticated or not`, by typing in the url. We want to prevent this, by checking if the user is authenticated first before rendering the profile page. This is the perfect example of when to create a `middleware`.

- The challenge here is creating the middleware function `ensureAuthenticated(req, res, next)`, which will check if a user is authenticated by calling passport's isAuthenticated method on the request which, in turn, checks if req.user is defined. If it is, then `next()` should be called, otherwise, we can just respond to the request with a redirect to our homepage to login. An implementation of this middleware is:

```javascript
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect("/");
}
```

- Now add ensureAuthenticated as a middleware to the request for the profile page before the argument to the get request containing the function that renders the page.

```javascript
app.route("/profile").get(ensureAuthenticated, (req, res) => {
  res.render(process.cwd() + "/views/pug/profile");
});
```

## How to Put a Profile Together

- Now that we can ensure the user accessing the /profile is authenticated, we can use the information contained in req.user on our page!

- Pass an object containing the property username and value of req.user.username as the second argument for the render method of the profile view. Then, go to your profile.pug view, and add the following line below the existing h1 element, and at the same level of indentation:

```pug
h2.center#welcome Welcome, #{username}!
```

- This creates an h2 element with the class 'center' and id 'welcome' containing the text 'Welcome,' followed by the username.

- Also, in `profile.pug`, add a link referring to the `/logout` route, which will host the logic to unauthenticate a user.

```pug
a(href='/logout') Logout
```

## Logging a User Out

- Creating the logout logic is easy. The route should just unauthenticate the user and redirect to the home page instead of rendering any view.

- In passport, unauthenticating a user is as easy as just calling req.logout(); before redirecting.

```javascript
app.route("/logout").get((req, res) => {
  req.logout();
  res.redirect("/");
});
```

- You may have noticed that we're not handling missing pages (404). The common way to handle this in Node is with the following middleware. Go ahead and add this in `after all your other routes`:

```javascript
app.use((req, res, next) => {
  res.status(404).type("text").send("Not Found");
});
```

## Registration of New Users

- Now we need to allow a new user on our site to register an account. On the res.render for the home page add a new variable to the object passed along--showRegistration: true. When you refresh your page, you should then see the registration form that was already created in your index.pug file! This form is set up to POST on /register, so this is where we should set up to accept the POST and create the user object in the database.

- The logic of the registration route should be as follows: Register the new user > Authenticate the new user > Redirect to /profile

- The logic of step 1, registering the new user, should be as follows: Query database with a findOne command > if user is returned then it exists and redirect back to home OR if user is undefined and no error occurs then 'insertOne' into the database with the username and password, and, as long as no errors occur, call next to go to step 2, authenticating the new user, which we've already written the logic for in our POST /login route.

```javascript
app.route("/register").post(
  (req, res, next) => {
    myDataBase.findOne({ username: req.body.username }, function (err, user) {
      if (err) {
        next(err);
      } else if (user) {
        res.redirect("/");
      } else {
        myDataBase.insertOne(
          {
            username: req.body.username,
            password: req.body.password,
          },
          (err, doc) => {
            if (err) {
              res.redirect("/");
            } else {
              // The inserted document is held within
              // the ops property of the doc
              next(null, doc.ops[0]);
            }
          }
        );
      }
    });
  },
  passport.authenticate("local", { failureRedirect: "/" }),
  (req, res, next) => {
    res.redirect("/profile");
  }
);
```

## Hashing Your Passwords

= Going back to the information security section, you may remember that storing plaintext passwords is never okay. Now it is time to implement BCrypt to solve this issue.

- Add `BCrypt` as a dependency, and require it in your server. You will need to handle hashing in 2 key areas: where you handle registering/saving a new account, and when you check to see that a password is correct on login.

- Currently on our registration route, you insert a user's password into the database like so: password: req.body.password. An easy way to implement saving a hash instead is to add the following before your database logic const hash = bcrypt.hashSync(req.body.password, 12);, and replacing the req.body.password in the database saving with just password: hash.

- Finally, on our authentication strategy, we check for the following in our code before completing the process: if (password !== user.password) { return done(null, false); }. After making the previous changes, now user.password is a hash. Before making a change to the existing code, notice how the statement is checking if the password is not equal then return non-authenticated. With this in mind, your code could look as follows to properly check the password entered against the hash:

```javascript
if (!bcrypt.compareSync(password, user.password)) {
  return done(null, false);
}
```

- That is all it takes to implement one of the most important security features when you have to store passwords!
- Notes about salt of password:

  - A note about the cost. When you are hashing your data the module will go through a series of rounds to give you a secure hash. The value you submit there is not just the number of rounds that the module will go through to hash your data. The module will use the value you enter and go through 2^rounds iterations of processing.

  - From @garthk, on a 2GHz core you can roughly expect:

  ```javascript
  rounds=8 : ~40 hashes/sec
  rounds=9 : ~20 hashes/sec
  rounds=10: ~10 hashes/sec
  rounds=11: ~5  hashes/sec
  rounds=12: 2-3 hashes/sec
  rounds=13: ~1 sec/hash
  rounds=14: ~1.5 sec/hash
  rounds=15: ~3 sec/hash
  rounds=25: ~1 hour/hash
  rounds=31: 2-3 days/hash
  ```

## Clean Up Your Project with Modules

- Right now, everything you have is in your server.js file. This can lead to hard to manage code that isn't very expandable. Create 2 new files: routes.js and auth.js

- Both should start with the following code:

```javascript
module.exports = function (app, myDataBase) {};
```

- Now, in the top of your server file, require these files like so: const routes = require('./routes.js'); Right after you establish a successful connection with the database, instantiate each of them like so: routes(app, myDataBase)

- Finally, take all of the routes in your server and paste them into your new files, and remove them from your server file. Also take the ensureAuthenticated function, since it was specifically created for routing. Now, you will have to correctly add the dependencies in which are used, such as const passport = require('passport');, at the very top, above the export line in your routes.js file.

- Keep adding them until no more errors exist, and your server file no longer has any routing (except for the route in the catch block)!

- Now do the same thing in your auth.js file with all of the things related to authentication such as the serialization and the setting up of the local strategy and erase them from your server file. Be sure to add the dependencies in and call auth(app, myDataBase) in the server in the same spot.

## Implementation of Social Authentication

- The basic path this kind of authentication will follow in your app is:

- User clicks a button or link sending them to our route to authenticate using a specific strategy (e.g. GitHub).
  Your route calls passport.authenticate('github') which redirects them to GitHub.
- The page the user lands on, on GitHub, allows them to login if they aren't already. It then asks them to approve access to their profile from our app.
- The user is then returned to our app at a specific callback url with their profile if they are approved.
  They are now authenticated, and your app should check if it is a returning profile, or save it in your database if it is not.
- Strategies with OAuth require you to have at least a Client ID and a Client Secret which is a way for the service to verify who the authentication request is coming from and if it is valid. These are obtained from the site you are trying to implement authentication with, such as GitHub, and are unique to your app--THEY ARE NOT TO BE SHARED and should never be uploaded to a public repository or written directly in your code. A common practice is to put them in your .env file and reference them like so: process.env.GITHUB_CLIENT_ID. For this challenge we're going to use the GitHub strategy.

- Obtaining your Client ID and Secret from GitHub is done in your account profile settings under 'developer settings', then 'OAuth applications'. Click 'Register a new application', name your app, paste in the url to your Repl.it homepage (Not the project code's url), and lastly, for the callback url, paste in the same url as the homepage but with /auth/github/callback added on. This is where users will be redirected for us to handle after authenticating on GitHub. Save the returned information as 'GITHUB_CLIENT_ID' and 'GITHUB_CLIENT_SECRET' in your .env file.

- In your routes.js file, add showSocialAuth: true to the homepage route, after showRegistration: true. Now, create 2 routes accepting GET requests: `/auth/github and /auth/github/callback`. The first should only call passport to authenticate 'github'. The second should call passport to authenticate 'github' with a failure redirect to /, and then if that is successful redirect to /profile (similar to our last project).

- An example of how /auth/github/callback should look is similar to how we handled a normal login:

```javascript
app
  .route("/login")
  .post(
    passport.authenticate("local", { failureRedirect: "/" }),
    (req, res) => {
      res.redirect("/profile");
    }
  );
```

## Implementation of Social Authentication II

- The last part of setting up your GitHub authentication is to create the strategy itself. For this, you will need to add the dependency of 'passport-github' to your project and require it in your auth.js as GithubStrategy like this: const GitHubStrategy = require('passport-github').Strategy;. Do not forget to require and configure dotenv to use your environment variables.

- To set up the GitHub strategy, you have to tell Passport to use an instantiated GitHubStrategy, which accepts 2 arguments: an object (containing clientID, clientSecret, and callbackURL) and a function to be called when a user is successfully authenticated, which will determine if the user is new and what fields to save initially in the user's database object. This is common across many strategies, but some may require more information as outlined in that specific strategy's GitHub README. For example, Google requires a scope as well which determines what kind of information your request is asking to be returned and asks the user to approve such access. The current strategy we are implementing has its usage outlined here, but we're going through it all right here on freeCodeCamp!

- Here's how your new strategy should look at this point:

```javascript
passport.use(new GitHubStrategy({
  clientID: process.env.GITHUB_CLIENT_ID,
  clientSecret: process.env.GITHUB_CLIENT_SECRET,
  callbackURL: /*INSERT CALLBACK URL ENTERED INTO GITHUB HERE*/
},
  function(accessToken, refreshToken, profile, cb) {
    console.log(profile);
    //Database logic here with callback containing our user object
  }
));
```
## Implementation of Social Authentication III
- The final part of the strategy is handling the profile returned from GitHub. We need to load the user's database object if it exists, or create one if it doesn't, and populate the fields from the profile, then return the user's object. GitHub supplies us a unique id within each profile which we can use to search with to serialize the user with (already implemented). Below is an example implementation you can use in your project--it goes within the function that is the second argument for the new strategy, right below where console.log(profile); currently is:
```javascript
myDataBase.findOneAndUpdate(
  { id: profile.id },
  {
    $setOnInsert: {
      id: profile.id,
      name: profile.displayName || 'John Doe',
      photo: profile.photos[0].value || '',
      email: Array.isArray(profile.emails)
        ? profile.emails[0].value
        : 'No public email',
      created_on: new Date(),
      provider: profile.provider || ''
    },
    $set: {
      last_login: new Date()
    },
    $inc: {
      login_count: 1
    }
  },
  { upsert: true, new: true },
  (err, doc) => {
    return cb(null, doc.value);
  }
);
```
- `findOneAndUpdate` allows you to search for an object and update it. If the object doesn't exist, it will be`inserted `and made available to the callback function. In this example, we always set last_login, increment the login_count by 1, and only populate the majority of the fields when a new object (new user) is inserted. Notice the use of default values. Sometimes a profile returned won't have all the information filled out or the user will keep it private. In this case, you handle it to prevent an error.
# References:

- https://stackoverflow.com/questions/27637609/understanding-passport-serialize-deserialize# References

- Middleware : https://expressjs.com/en/guide/using-middleware.html
