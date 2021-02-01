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

```javascript
// template engine with pug
app.set("view engine", "pug");
app.get("/template-engine", function (req, res) {
  res.render("index", { title: "Hey guy", message: "Hello there !!" });
});
```
##  Use a Template Engine's Powers
One of the greatest features of using a template engine is being able to pass variables from the server to the template file before rendering it to HTML.

In your Pug file, you're able to use a variable by referencing the variable name as #{variable_name} inline with other text on an element or by using an equal sign on the element without a space such as p=variable_name which assigns the variable's value to the p element's text.

We strongly recommend looking at the syntax and structure of Pug here on GitHub's README. Pug is all about using whitespace and tabs to show nested elements and cutting down on the amount of code needed to make a beautiful site.

Looking at our pug file 'index.pug' included in your project, we used the variables title and message.

To pass those along from our server, you will need to add an object as a second argument to your res.render with the variables and their values. For example, pass this object along setting the variables for your index view: {title: 'Hello', message: 'Please login'}

It should look like: res.render(process.cwd() + '/views/pug/index', {title: 'Hello', message: 'Please login'}); Now refresh your page and you should see those values rendered in your view in the correct spot as laid out in your index.pug file!
# References

- Middleware : https://expressjs.com/en/guide/using-middleware.html
