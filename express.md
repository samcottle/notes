# Express

Express is a web framework for Node.js, and can be used to build networking services and applications.

## Installing Express

After installing Node.js, Express can be installed with:

```js
npm install express --save
```

Alternatively, `express` can specified in the `dependencies` in a `package.json` file, and then installed with `npm install -y`.

## Hello world

1. Create a `index.js` file for your code. For example:

```bash
$ touch index.js
```

2. Add the following code to the file:

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => res.send("Hello world!"));
app.listen(3000, () => console.log("Server ready on port 3000"));
```

This will create a server, which serves the text `Hello world!` on port `3000`.

3. Start the Express server:

```bash
$ node index.js
```

4. Launch a browser, and navigate to `localhost:3000` to see the text.

### Hello world explained

So what does the above code actually do?

First, we are importing the `express` package, and assigning it the value `express`. Then, instantiating it. 

```js
const express = require("express");
const app = express();
```

Then, we use the `.get()` method to tell it to listen for GET requests on the path `/`.  The `req` and `res` represent the HTTP request (which can include info such as parameters, headers, a request body, and more) and the response (what we'll send to the client) - both of which we need to handle in this callback.
In this case, the callback is being used is the [`res.send()`](http://expressjs.com/en/api.html#res.send) method, to send the string `"Hello world!"` to the client.
`app.get("/", (req, res) => res.send("Hello world!"));`

Finally, we're telling the app to start a server, to listen on port 3000. We also log some information to the console, so the human starting the server knows which port the app is listening on.
`app.listen(3000, () => console.log("Server ready on port 3000"));`

## HTTP methods

Express has built-in methods representing each HTTP verb:

```js
app.get("/", (req, res) => { /* callback function */ });
app.post("/", (req, res) => { /* callback function */ });
app.put("/", (req, res) => { /* callback function */ });
app.delete("/", (req, res) => { /* callback function */ });
app.patch("/", (req, res) => { /* callback function */ });
```

Each of these accepts a callback function, which is called when the request is started.

## Handling requests

Here we'll cover off some common use cases that relate to handling requests.

A full list of request parameters, and details of each, can be found in the [Express documentation](http://expressjs.com/en/api.html#req).

### Query strings

These are strings that comes after a URL path, and are used to retrieve variables from an HTTP request. They start with a `?`; variables are separated with an `&`, and are assigned values with an `=`:

```
https://www.example.com?name=Sam&username=samcottle
```

#### GET query strings

Express can handle GET query strings using the [`req.query`](http://expressjs.com/en/api.html#req.query) method. Here's the most simple example:

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
	console.log(req.query);
}); 

app.listen(3000, () => console.log("Server ready on port 3000"));
```

When this server is running, any variables specified in a query string after on the path `/` will be logged as a JSON object to the console (unless there are no variables, in which case an empty object will be logged). The example above would log the following:

```
{ name: 'Sam', username: 'samcottle' }
```

##### Other examples

You can access the value of a specific property provided in a query string. For example, the value of `name`:
```

...
app.get("/", (req, res) => {
	console.log(req.query.name);
}); 

...
```

A `for...in` loop can be used to iterate over all the the properties in a query string:

```js
...

app.get("/", (req, res) => {
	for (const key in req.query) {
		console.log(key, req.query[key]);
	}
}); 

...
```

#### POST query strings

These are typically sent by a form (`Content-Type: application/x-www-form-urlencoded`), or by using a POST request to send JSON data (`Content-Type: application/json`).

POSTed data can be accessed by referencing it from the [`req.body`](http://expressjs.com/en/api.html#req.body)(for example, `req.body.name`). 

But depending on how the data was sent, you will need to use middleware to handle the data being POSTed.

```js
const express = require("express");
const app = express();

app.use(express.urlencoded()); // Middleware to handle JSON data sent as `Content-Type: application/x-www-form-urlencoded`
app.use(express.json()); // Middleware to handle JSON data sent as `Content-Type: application/json`

app.post("/post", (req, res) => {
	const name = req.body.name;
	console.log(req.body.name);
}); 

app.listen(3000, () => console.log("Server ready on port 3000"));
```

## Sending responses

TODO
