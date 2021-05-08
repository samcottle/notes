# MongoDB and Mongoose

MongoDB is used to store data records for use by an application. It's a *non-relational* database, meaning it stores all associated data within one record (rather than across many preset tables, like a SQL database).

Mongo uses JSON as its storage structure, which makes it good for a backend database for JavaScript. Mongoose.js is a NPM module that allows you to write Mongo objects as you would in JavasScript.

## Adding MongoDB and Mongoose to your app

To use MongoDB and Mongoose in your app:

1. Add `mongodb` and `mongoose` to your app's `package.json`.
2. Add your Mongo database URI in your `.env` file, using `MONGO_URI="URI_GOES_HERE"`.
3. Require `mongoose` in you app, with `const mongoose = require('mongoose');`.
4. Add `mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true });` to your app to connect it.

## Creating a schema

To create a model, you first need a schema. These are like building blocks for your model. They define the shape of the documents in a collection. Basically, you create instances of your objects, and these are called documents.

Shemas can also be nested to make more complex models.

A schema is defined with Mongoose JS like this:

```js
const mongoose = require('mongoose');
let Schema = mongoose.Schema;

let blogSchema = new Schema({
    title: String, // String is shorthand for {type: String}
    author: String,
    body: String,
    comments: [{body: String, date: Date}],
    date: {type: Date, default: Date.now},
    hidden: Boolean,
    meta: {
        votes: Number,
        favs: Number
    }
});
```

There are several permitted SchemaTypes (i.e. `String`, `Number`, `Date`, `Boolean`, etc.). These are specified in the [Mongoose JS documentation](https://mongoosejs.com/docs/guide.html).

So the schema for a person, with a `name` (required string), `age` (number), and `favoriteFoods` (array of strings) would look like this:

```js
const Schema = mongoose.Schema;

// Define the Schema
const personSchema = new Schema({
    name: { type: String, required: true },
    age: Number,
    favoriteFoods: [String]
});

// Create a Person using the Schema
const Person = mongoose.model("Person", personSchema);
```

## Using handlers

Handler functions are used for interactions between a server and a database. These are executed when some event happens (e.g. someone hits an endpoint on your API). We'll go through a couple of examples below.

### Done

The `done()` function will tell our program to proceed after performing an asynchronous operation, like inserting, searching, updating, or deleting. It should be called as `done(null, data)` on success, or `done(error)` in case of an error.

Here's an example of creating and saving a new person, using the schema we defined earlier, and saving them to a database with `done()`.

```js
var createAndSavePerson = function(done) {

    // Create new person
    let sam = new Person({
        name: "Sam",
        age: 37,
        favoriteFoods: ["pizza", "halloumi"]
    });
  
    // Save new person to database
    sam.save(function(err, data) {
        if(err) return console.err(err);
        done(null, data);
    });
};
```

## Creating models

Models can be compiled using `Schema` definitions.
