# The Pug templating engine

[Pug](https://pugjs.org/) is the default templating engine for [Express](/express.md). Pug templates use `.pug` files.

## Hello world!

1. Install Pug with:

```bash
$ npm install pug
```

2. Add Pug in your app, by initializing and setting it:

```js
const express = require("express");
const app = express();

app.set("view engine", "pug");

// Create views here

app.listen(3000, () => console.log("Server ready on port 3000"));
```

3. Create a view (i.e. a page you want rendered on a specific route):

```js
...

app.get("/hello", (req, res) => {
  res.render("hello-world");
});
```

4. Create a template for the view in `/views/hello-world.pug`, and add some content:

```text
p Hello world!
```

5. Launch a browser, and navigate to `localhost:3000/hello` to see the content.

## Formatting

Unlike HTML, Pug doesn't use closing tags (i.e. does not have the equivalent of something like `</h1>`). Instead it uses indentation to achieve the same result.

Also, attributes (such as `href`) are added using brackets.

For example:

```text
ul
  li
    a(href="/") Home
  li
    a(href="/page-1") Page 1
  li
    a(href="/page-2") Page 3
  li
    a(href="/page-3") Page 3

input.search(
  type="text"
  name="search"
  placeholder="Enter your search terms..."
)
```

This is the equivalent to the following HTML:

```html
<ul>
  <li><a href="/">Home</a></li>
  <li><a href="/page-1">Page 1</a></li>
  <li><a href="/page-2">Page 2</a></li>
  <li><a href="/page-3">Page 3</a></li>
</ul>

<input
  class="search"
  type="text"
  name="search"
  placeholder="Enter your search terms..."
/>
```

More information on Pug formatting is available in the **Language Reference** of the [Pug documentation](https://pugjs.org).

To convert bulk HTML to Pug you can use [this converter](https://jsonformatter.org/html-to-jade).

## Using scripts and styles

External JavaScript and CSS can be added as follows:

```text
html
  head
    script(src="script.js")

    link(rel="stylesheet", href="css/main.css")
```

JavaScript can also be added inline:

```text
script
  (console.log("Hello console!");)
```

## Including other Pug files

Other Pug files can be included as follows:

```text
include otherfile.pug
```

## Using blocks

To keep your content clean and organized, you'll typically want to create a base template. All other templates extend from this.

### Creating a base template

Include some `block`s. These are sections of the base template that you want to customize per page.

For example, the `head` (i.e. `block head`) and `body` (i.e. `block body`):

```text
html
    head
        script(src="script.js")

        link(rel="stylesheet", href="css/main.css")
        block head
    body
        block body
            h1 Home page
            p welcome
```

### Extending the base template

To extend from a base template, create a new `.pug` file for your new template.

In the new template, use the `extends` keyword to define the base template being used:

```text
extends home.pug
...
```

Then redefine any `block`s that you want changed from the base template:

```text
...
block body
    h1 Another page
    p Welcome to another page! Here's a list:
    ul
        li Item 1
        li Item 2
```

Any blocks that are not redefined will use the content from the base template.

## Using variables

Variables can be declared in a Pug template as follows:

```text
- var name = "Sam"
- var luckyNumber = 7
```

Or set when creating a route, like this:

```js
app.get("/hello", (req, res) => {
  res.render("hello-world", { name: "Sam", luckyNumber: 7 });
});
```

Variables can be interpolated in a Pug template with `#{variableNameHere}`:

```text
p Hello, my name is #{name}, and my lucky number is #{luckyNumber}!
```

## Using functions

Pug can interpolate the return value of a function like this:

```js
app.get("/about", (req, res) => {
  res.render("about", { getName: () => "Pug" });
});
```

This can be used by a template like this:

```text
p Hello #{getName()} world!
```

## Using conditionals

In addition to `if` and `else`, Pug also offers `unless` (which works like a negated `if`).

```text
if name
  h2 Hello from #{name}
else if anotherName
  h2 Hello from #{anotherName}
else
  h2 Hello
```

For more information on how conditionals can be used, see the [Pug documentation on Conditionals](https://pugjs.org/language/conditionals.html).

## Using loops

Pug supports `for`, `each`, and `while` loops as methods of iteration:

Example of a `for` loop:

```text
- var persons = ["Paul", "Ringo", "John", "George"]

p There are #{persons.length} people in the band:

for person in persons
  li= person
```

Examples of `each` and `while` loops:

```text
ul
  each val in [1, 2, 3, 4, 5]
    li = val
```

```text
- var n = 1;
ul
  while n < 6
    li = n++
```

Both of these will generate the following HTML:

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
```

For more information on how iteration can be used, see the [Pug documentation on Iteration](https://pugjs.org/language/iteration.html).

## Comments

You can add comments to Pug templates.

These can either be visible in the resulting HTML (i.e. the equivalent of `<!-- Comment -->`):

```text
// This comment will be visible in the HTML

//
    This multi-line comment
    will also be visible in the HTML
    via "View Page Source"
```

Or not visible in the resulting HTML (i.e. only visible in the template file):

```text
//- This comment will *not* be visible in the HTML

//-
    It is only visible
    in the .pug file
```
