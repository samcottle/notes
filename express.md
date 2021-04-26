# Express

[Express](http://expressjs.com/) is a web framework for Node.js, and can be used to build networking services and applications.

## Installing Express

After [installing Node.js](https://nodejs.org/en/download/package-manager/), Express can be installed with:

```bash
$ npm install express --save
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

This will create a server on port `3000`, that will serve the text `Hello world!` on the path `/`.

3. Start the Express server:

```bash
$ node index.js
```

4. Launch a browser, and navigate to `localhost:3000/` to see the text.

### Hello world explained

So what does the above code actually do?

First, we are importing the `express` package into our application (assigning it the value `express`), and instantiating it.

```js
const express = require("express");
const app = express();
```

Then, we use the `.get()` method to tell the application to listen for GET requests on the path `/`. The `req` and `res` represent the HTTP request and response - both of which can be handled using a callback.
In this case, the callback being used is the [`res.send()`](http://expressjs.com/en/api.html#res.send) method, to send the string `"Hello world!"` to the client.

```js
app.get("/", (req, res) => res.send("Hello world!"));
```

Finally, we're telling the app to start a server, to listen on port 3000. We also log some information to the console, so the human starting the server can see which port the app is listening on.

```js
app.listen(3000, () => console.log("Server ready on port 3000"));
```

## HTTP methods

Express has built-in methods representing each [HTTP verb](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods). For example:

```js
app.get("/", (req, res) => {
  /* callback */
});
app.post("/", (req, res) => {
  /* callback */
});
app.put("/", (req, res) => {
  /* callback */
});
app.delete("/", (req, res) => {
  /* callback */
});
app.patch("/", (req, res) => {
  /* callback */
});
```

Each of these accepts a callback function, which is called when the request is started.

## Handling requests

Requests can include data such as parameters, headers, a request body, and more. Here we'll cover off some common use cases that relate to handling requests.

A full list of request callbacks, and details of each, can be found in the [Express documentation](http://expressjs.com/en/api.html#req).

### Query strings

These are strings that come after a URL path, and are used to pass variables from an HTTP request. Query strings start with a `?`; variables are assigned a value with an `=`; multiple variables are separated with an `&`. For example:

```text
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

```js
{ name: "Sam", username: "samcottle" }
```

##### Other examples

You can access the value of a specific property provided in a query string. For example, the value of `name`:

```js

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

These are typically sent from a form (`Content-Type: application/x-www-form-urlencoded`), or a POST request that sent JSON data (`Content-Type: application/json`).

POSTed data can be accessed by referencing it from the [`req.body`](http://expressjs.com/en/api.html#req.body)(for example, `req.body.name`).

Depending on how the data was sent, you will need to use middleware to handle the data being POSTed.

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

Response types can include data such as objects or arrays, text, and more. Here we'll cover off some of the common use cases that relate to sending responses.

A full list of response callbacks, and details of each, can be found in the [Express documentation](http://expressjs.com/en/api.html#res).

### Sending a basic response

The Hello world example used [`res.send()`](https://expressjs.com/en/api.html#res.send) to send a HTTP response, the text string `"Hello world!"`, to the client.

When passing a text string or some HTML into this method, Express automatically sets the `Content-Type` as `text/html`. Similarly, by passing in a JSON object or array the `Content-Type` is set to `application/json` (although `res.json()` should really be used instead).

Once `res.send()` has done its thing, it closes the connection.

### Sending the HTTP response status

The [`res.status()`](https://expressjs.com/en/api.html#res.status) method can be used to send a [HTTP status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) to the client:

```js
const express = require("express");
const app = express();

app.get("/404", (req, res) => res.status(404).send("File not found"));

app.listen(3000, () => console.log("Server ready on port 3000"));
```

If you don't need to send a fancy message to the client then [`res.sendStatus()`](https://expressjs.com/en/api.html#res.sendStatus) can be used instead. This sends a string representation of the HTTP status to the client. For example:

```js
res.sendStatus(200); // Is equivalent to res.status(200).send('OK')
res.sendStatus(403); // Is equivalent to res.status(403).send('Forbidden')
res.sendStatus(404); // Is equivalent to res.status(404).send('Not Found')
res.sendStatus(500); // Is equivalent to res.status(500).send('Internal Server Error')
```

### Sending JSON

The advised way to send a JSON response is with the [`res.json()`](https://expressjs.com/en/api.html#res.json) method (as opposed to `res.send({/* JSON here */})`). Any JSON object, array, string, Boolean, number, or `null` can be sent - and any other content will be automatically converted to JSON using [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify).

```js
...

app.get("/user", (req, res) =>
  res.json({ "name": "Sam", "username": "samcottle" })
);

...
```

### Sending an empty response

If you don't have anything to send to the client, the [`res.end()`](https://expressjs.com/en/api.html#res.end) method can be used to close the connection to the client:

```js
...

app.get("/", (req, res) => {
  console.log(req.query);
  res.end();
});

...
```

### Managing cookies

The [`res.cookie()`](https://expressjs.com/en/api.html#res.cookie) method can be used to set or manipulate a cookie.

A basic example of this is to create a cookie containing a username:

```js
...

res.cookie("name", "sam");

...
```

Additional parameters can be passed in an object when setting the cookie, such as the `domain`, whether the cookie should only be used for `secure` sessions, and a date the cookie `expires` (this can also be done with `maxAge`):

```js
...

res.cookie("name", "sam", { domain: ".github.com", path: "/account", secure: true });
res.cookie("name", "sam", { expires: new Date(Date.now() + 900000) });

...
```

The example above set two cookies: one with account details, and another with the expiry date.

Objects can also be passed in the `value` parameter, which can be useful for use cases like tracking the items in a user's shopping cart:

```js
...

res.cookie("cart", { items: [7, 4, 5] }, { maxAge: 900000 });

...
```

For a full list of parameters that can be used when setting cookies, see the [Express documentation](https://expressjs.com/en/api.html#res.cookie).

#### Clearing a cookie

Cookies can be cleared with `res.clearCookie()`, by passing in the name of the cookie (from the example above, this would be `name`):

```js
...

app.get("/admin", (req, res) =>
  res.clearCookie("name");
);

...
```

## Working with HTTP headers

[HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) let a client and server pass additional information in a request or response.

Express can use this to determine authentication information, the type of content that is being transmitted, the client's user agent, and more.

### Accessing request headers

To access _all_ headers included in a request, use the `req.headers` property. For example, to log all the request headers to the console:

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  console.log(req.headers);
});

app.listen(3000, () => console.log("Server ready on port 3000"));
```

Specific headers can be accessed with `req.header`. For example, to log just the `User-Agent` to the console:

```js
...

app.get("/", (req, res) => {
  console.log(req.header("User-Agent"));
});

...
```

### Setting response headers

The `res.set()` method can be used to specify the HTTP header type of a response. For example, to set the `Content-Type` as `text/html`:

```js
...

res.set("Content-Type", "text/html");

...
```

If you don't need to set anything more than the `Content-Type` header, then [`res.type()`](https://expressjs.com/en/api.html#res.type) can also be used:

```js
...

res.type(".html"); // Is equivalent to 'text/html'
res.type("html"); // Is equivalent to 'text/html'
res.type("json"); // Is equivalent to 'application/json'
res.type("application/json"); // Is equivalent to 'application/json'
res.type("png"); // Is equivalent to 'image/png'

...
```

In many cases Express will set a `Content-Type` automatically. In this case, `res.type()` can be used to set a different `Content-Type`.
