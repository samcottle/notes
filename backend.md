# APIs and Microservices

The quickest way to get started with a new Node project is by using the `npm init` command. This walks through the creation of the standard Node files, such as `package.json` and an entry point file (usually `index.js`).

## Standard files and folders

In addition to your entry point file (typically `index.js`), a node project will have at least the following files and folders:

- `package.json` file: When initializing a new project, NPM generates a `package.json` file. This is where you list all the dependencies for your project.

- `node_modules` folder: This is where packages for your project are installed. This folder is automatically generated when you run `npm install` (based on any listed dependencies).

- `.env` file: Used to pass environment variables (API keys, your database URI, etc) to your application. It can also be used to store configuration options, so you can change your application's behaviour without needing to rewrite a lot of code.

### package.json

The `package.json` file is the center of any node.js project (or NPM package). It is analogous to the `<head>` of an HTML document (which describes the content of a webpage).

It is a single JSON object, with key-value pairs. The only required fields are `"name"` and `"version"`, but including other information in here (such as additional information about your project, like a `description` or `keywords`) is standard practice.

It is also where you list all the `dependencies` for your project (in an object). This ensures that NPM gets the correct dependencies for your project when the project is set up. Here's an example, containing the `express` package:

```json
{
  "name": "Node project",
  ...
  "dependencies": {
    "package-name": "version",
    "express": "^4.14.0"
  }
}
```

Once the dependencies have been added, run `npm install` to install them into your project. These are installed into the `node_modules` folder.

#### Dependency versioning

Packages use semantic versioning, with the version format: `"package": "MAJOR.MINOR.PATCH"`. **MAJOR** versions increment when changes are made that cause API incompatibilities. **MINOR** are for when functionality is added in a backwards-compatible manner. A **PATCH** is generally for bugfixes.

You would often want to allow an NPM dependency to update to the latest **PATCH** version (i.e. bugfixes). You can do this by using a `~` character before the version number. For example, to allow for any 1.3.x version of `package` you would use:

```json
"package": "~1.3.8"
```

Similarly, you can use the `^` to allow a package to update to the latest **MINOR** version. For example, to allow for any 1.x.x version of `package` you would use:

```json
"package": "^1.3.8"
```

To go for broke, you can use the absolute latest version of a `package` with:

```json
"package": "*"
```

### /node_modules

This folder is either located in a root `node_modules` folder (if the modules are globally accessible), or a project's own `node_modules` folder (if accessible only to that project). This is because packages are generally made available on a per project basis (creating separation between dependencies for different projects).

The `npm` (Node Package Manager) command line tool is used to manage packages. After adding dependencies to your project (to `package.json`), run `npm install` to install these packages.

### .env

This is a hidden file, stored in the root of your application. It is hidden because it should *only* be accessible by you (don't forget to add it to `.gitignore`!).

A basic `.env` file looks like this:

```bash
API_KEY="[YOUR_API_KEY_GOES_HERE]"
DATABASE_URI="[URI_OF_YOUR_DATABASE_GOES_HERE]"
MESSAGE_STYLE=uppercase
```

After specifying environment variables in the `.env` file, they are accessable/usable from your app by referring to them in the format `process.env.VAR_NAME`.

## Basic Node and Express

Node allows developers to build server-side programs using JavaScript. It comes with a bunch of built-in modules that can help do this. For example:

- HTTP: Module that acts as a server.
- File system: Reads and modifies files.
- Path: Navigating directories and file paths.
- Assertion testing: Checks code against prescribed constraints.

The module often used with Node is *Express*. It runs between the Node server and the frontend pages of a web application. It also handles an application's routing, directing users to the correct page of a web application. **A lot of the code shown below is specific to Express**.

### Using dependencies

To use a dependency in your app, declare it as a variable (in an entry point file, typically called `index.js`). For example, to use `express` and `body-parser` in the app, and instantiate `express`:

```js
const express = require('express');
const app = express();
const bodyParser = require('body-parser');
```

### Starting your server

To run your app, you can use either of these commands:
- `npm start`
- `node index.js` (or replace `index.js` with the name of your app entry point)

But before doing this, you will need to create the app.

### Setting a port

A fundamental Express method is `app.listen(port)`. This tells your server to listen on a given port (putting it in a running state). For example, by specifying `app.listen(3000);` in your app, it would set up a server to listen on port `8080`:

```js
app.listen(8080, () => {
   console.log("Server running on port 8080");
});
```

You can also use `app.listen(process.env.PORT || 8080);` to set up a server to listen on *any* port or (`||`) port `8080`.

### Routing and handling

In Express, routes take the structure `app.METHOD(PATH, HANDLER)`, where **METHOD** is an http method (e.g. `get`), **PATH** is a relative server path (can be a string or RegEx), **HANDLER** is a function that Express will call when the route is matched.

Handlers take the format `function(req, res) {...}`, where `req` is the request object and `res` is the response object. For example, the following handler will serve `"Response string"`:

```js
function(req, res) {
    res.send("Response string");
}
```

So to serve the string `"Hello Express"` to any GET requests to the root path (`/`) of a website, for example, you would use:

```js
app.get("/", function(req, res) {
  res.send("Hello Express");
});
```

#### Serving files

You can respond to requests with a file using the `res.sendFile(path)` method. You can specify the file you want to respond with in the `app.get("/", ...)` route handler.

This method needs to have an absolute path, and it's recommended you use the Node global variable `__dirname` to calculate this, in this format: `__dirname + "relativePath/file.ext"`

For example, to serve the file at `/views/index.html` in response to GET requests to the root path (`/`) you would use:

```js
app.get("/", function(req, res) {
  res.sendFile(__dirname + "/views/index.html");
});
```

#### Serving JSON

Serving JSON is similar to serving files, but you use the `res.json()` method as the route handler (passing in the JSON object you want to serve as the handler). Here's an example showing how you would serve a basic JSON object at the path (i.e. endpoint) `/json`:

```js
app.get("/json", function(req, res) {
  res.json({"message": "Hello json"})
});
```

#### Adding environment variables to an app

To use environment variables, you first need to store them in the `.env` file of your project. In the `.env` file, add variables using the format `VAR_NAME=value` (note the lack of spaces around the `=`). For example, to set the `MESSAGE_STYLE` of **uppercase**:

```bash
MESSAGE_STYLE=uppercase
```

You can then load and use the environment variable in your app using by referring to it in the format `process.env.VAR_NAME`. For example, the following code will serve the `"Hello JSON"` messages (from the previous section) as `"HELLO JSON"` when the `MESSAGE_STYLE` of **uppercase** is present:

```js
app.get("/json", function(req, res) {
  if (process.env.MESSAGE_STYLE === "uppercase") {
    res.json({"message": "HELLO JSON"});
  } else {
    res.json({"message": "Hello json"});
  }  
});
```

### Middleware

*Middleware* functions are functions that intercept route handlers, and add some functionality. They take three arguments: a request object, a response object, and the next function in your application's request-response cycle. These execute some code that has some 'side effect' on the app (usually adding information to the request or response object/s).

They can also be used to end the cycle by sending a response when a condition is met. If they don't send the response when they're done, they start the execution of the next function in the stack (by calling `next()`).

So with the following example:

```js
function(req, res, next) {
  console.log("Hello middleware");
  next();
}
```

If you mounted this on a route, when a request matches its route it:

1. Displays the `"Hello middleware"`.

2. Executes the next function in the stack.

#### Using middleware at the root level

To mount a middleware function at the root level, use the `app.use(MIDDLEWARE_FUNCTION)` method. This would execute the middleware for all requests. If you only wanted to execute it for POST requests, for example, you would use `app.post(MIDDLEWARE_FUNCTION)` instead (ditto GET, DELETE, PUT, etc.).

So let's say you wanted to build a root level logger. This would log a string with the format `method path - ip` to the console, when someone accessed any path on your server.

First you would mount the logger:

```js
function logger(req, res, next) {
  console.log(req.method + " " + req.path + " - " + req.ip);
  next();
}
```

Then to use it:

```js
app.use(logger);
```

This logs the following message in the console:

```js
GET /json - ::ffff:127.0.0.1
```

#### Using middleware at a specific path

To use middleware at a specific path, you can mount it a specific route (i.e. `app.METHOD(path, middlewareName)`).

Middleware can also be chained togther inside a route definition. For example, to respond to requests at `/now` with a JSON object containing the time, you could chain the following together:

```js
app.get('/now', (req, res, next) => {
    req.time = new Date().toString();
    next();
  },
  (req, res) => {
    res.send({"time": req.time});
  }
);
```

In practice, the main reason for using chaining is that you can have functions perform validation on some data, handle errors, or handle other conditions or special cases.

### Serving static assets

Static assets (such as stylesheets, scripts, and images) can use the Express `static` middleware: `express.static(path)`

This needs to be mounted first, using the method `app.use(path, middlewareName)`. The `path` argument is optional, but if you don't the middleware will be passed for all requests.

So to mount the `static` middleware, and serve static assets in the folder `/public` to the root path, you would use:

```js
app.use("/", express.static(__dirname + "/public"));
```

### Using route parameters

When building an API, we have to let users let us know what they want to get from our service. For example, if they want to get information on a `user` they've stored, they need a way to specify which user they're interested in.

Instead of building a static response for each user, you can use *route parameters* to make dynamic responses.  So instead of a building a static response for each user ID, you could use the dynamic response `/user/:id` (so in this case the route parameter is `:id`).

Can then access this using `req.params.PARAMETER_ID` (so for the above example, this would be `req.params.id`).

Here's a really simple example, showing what they look like. In this example, the server will take a word specified in a GET request URL, and respond by echoing it in a JSON object. For example, `/awesome/echo` responds with `{"echo": "awesome"}`:

```js
app.get('/:word/echo', (req, res) => {
  res.send({echo: req.params.word});
});
```

### Using query strings

A common way to get input from a client is by encoding this data after the route path, using a query string. These are delimited by a `?`, with keys-values separated by a `=`. Each key-value pair is separated by a `&`. Here's an example of `/user` with a query string: `/user?firstName=Sam&lastName=Cottle`.

Express will parse the data provided in this string, and populate an object called `req.query` (i.e. `{"firstName": "Sam", "lastName": "Cottle"}`).

For example, to take a query string with a `firstName` and a `lastName`, and return an object in the format `{"name": "firstName lastName"}`:

```js
app.get('/name', (req, res) => {
  res.send({"name": req.query.first + " " + req.query.last});
});
```

### Parsing POST requests

POST is a common HTTP method, and is used to send data and create a new item in a database (such as client data from within an HTML form).

For these requests the data you want to POST doesn't appear in the URL, but instead is hidden in the request body (i.e. *payload*). The request body looks a bit like this:

```html
POST /path/subpath HTTP/1.0
From: john@example.com
User-Agent: someBrowser/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 20
name=John+Doe&age=25
```

Using the `body-parser` package, you can decode the data in the request body.

```js
// Include body-parser in app
const bodyParser = require("body-parser")

// Mount body-parser
app.use(bodyParser.urlencoded({ extended: false }));

// Parse JSON sent in the POST request
app.use(bodyParser.json());

// Return an object with an object containing the name
app.post('/name', (req, res) => {
  res.send({"name": req.body.first + " " + req.body.last});
});
```
