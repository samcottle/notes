# Functional programming

This is a programming approach where the program is broken down into small, testable parts (i.e. functions). Each functional solution should be:

- Simple and isolated
- Without any side effects happening outside the scope of the function (i.e. functions should be _pure functions_)
- Don't alter a variable or object - instead create new variables and objects and return these from a function (for example, use `.slice` instead of `.splice`).
- Declare dependencies explicitly (if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.)

In other words:

**Input** => **Process** => **Output**

Some key terms for functional programming:

- _Callbacks_: Functions that are passed into another function, to decide whether that function should be invoked. For example, `filter` is a callback that tells a function how to filter an array.
- _First class functions_: These can be assigned to a variable, passed into another function, or returned from another function like any other value can be. In JavaScript, all functions are first class functions.
- _Higher order functions_: Functions that take a function as an argument, or return a function as a return value. The functions that are are passed or returned are called a _lambda_.

## Functional programming methods

The common methods are commonly used to achieve this are:

- `map`: Iterates over each element in an array, and returns a new array containing the result of calling the callback function on each element. For example, take an array of numbers, and double the value of each.
- `filter`: Iterates over each element in an array, and runs a conditional statement over them. If the condition returns true, it gets added to the new array. For example, filtering out the odd numbers from an array.
- `reduce`: Iterates over the array and reduces them down to an array with just one value. For example, adding every number together in the array.

The reason these methods fit in with the concept of functional programming is that none of them mutate the original array.

Below is some pseudo-pseudo code demonstrating how these methods can be used, in combination with a function, on an array of agricultural raw materials. By `map`ping these using the function `cook()`, they are converted to a new array of edible foods. This array is then `filter`ed with the function `isVegetarian()`, creating a new array of edible foods that are vegetarian-friendly. The method `reduce` is used with the function `eat()`, to convert the food into... human waste.

```js
map([🌽, 🐮, 🐔], cook())
// [🍿, 🍔, 🍳]

filter([🍿, 🍔, 🍳], isVegetarian())
// [🍿, 🍳]

reduce([🍿, 🍳], eat())
// 💩
```

## Examples

Below are some examples showing how functional programming can be used in JavaScript.

### Functions and lambdas

Here's an example of how a higher order function, `getTea`, can be used to accept the lambdas `prepareGreenTea` and `prepareBlackTea`:

```js
const prepareGreenTea = () => "greenTea";

const prepareBlackTea = () => "blackTea";

const getTea = (prepareTea, numOfCups) => {
  const teaCups = [];

  for (let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }

  return teaCups;
};

const tea4GreenTeamFCC = getTea(prepareGreenTea, 27);
const tea4BlackTeamFCC = getTea(prepareBlackTea, 13);

console.log(tea4GreenTeamFCC, tea4BlackTeamFCC);
```

### Incrementer

This example is of an incrementer that does not alter the variable it is incrementing (in this case, `fixedValue`):

```js
var fixedValue = 4;

function incrementer() {
  return fixedValue + 1;
}

var newValue = incrementer(); // Returns 5
console.log(fixedValue); // Returns 4
```

### Booklist

This example shows how modified `bookList`s can be returned without altering the original `bookList` variable:

```js
var bookList = [
  "The Hound of the Baskervilles",
  "On The Electrodynamics of Moving Bodies",
  "Philosophiæ Naturalis Principia Mathematica",
  "Disquisitiones Arithmeticae",
];

function add(arr, bookName) {
  var newArr = [...arr];
  newArr.push(bookName);
  return newArr;
}

function remove(arr, bookName) {
  var book_index = bookList.indexOf(bookName);
  var newArr = [...arr];
  if (book_index >= 0) {
    newArr.splice(book_index, 1);
    return newArr;
  }
}

var newBookList = add(bookList, "A Brief History of Time");
var newerBookList = remove(bookList, "On The Electrodynamics of Moving Bodies");
var newestBookList = remove(
  add(bookList, "A Brief History of Time"),
  "On The Electrodynamics of Moving Bodies"
);

console.log(bookList); // Returns ["The Hound of the Baskervilles", "On The Electrodynamics of Moving Bodies", "Philosophiæ Naturalis Principia Mathematica", "Disquisitiones Arithmeticae"]

console.log(newerBookList); // Returns ["The Hound of the Baskervilles", "Philosophiæ Naturalis Principia Mathematica", "Disquisitiones Arithmeticae"]
```

### Map method

This example shows how to use `.map` instead of a `for` loop, to log the `Title` and `imdbRating` of movies in an IMDB `watchList` object:

```js
var watchList = [
  {
    Title: "Inception",
    Year: "2010",
    Rated: "PG-13",
    Released: "16 Jul 2010",
    Runtime: "148 min",
    Genre: "Action, Adventure, Crime",
    Director: "Christopher Nolan",
    Writer: "Christopher Nolan",
    Actors: "Leonardo DiCaprio, Joseph Gordon-Levitt, Ellen Page, Tom Hardy",
    Plot:
      "A thief, who steals corporate secrets through use of dream-sharing technology, is given the inverse task of planting an idea into the mind of a CEO.",
    Language: "English, Japanese, French",
    Country: "USA, UK",
    Awards: "Won 4 Oscars. Another 143 wins & 198 nominations.",
    Poster:
      "http://ia.media-imdb.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
    Metascore: "74",
    imdbRating: "8.8",
    imdbVotes: "1,446,708",
    imdbID: "tt1375666",
    Type: "movie",
    Response: "True",
  },
  {
    Title: "Interstellar",
    Year: "2014",
    Rated: "PG-13",
    Released: "07 Nov 2014",
    Runtime: "169 min",
    Genre: "Adventure, Drama, Sci-Fi",
    Director: "Christopher Nolan",
    Writer: "Jonathan Nolan, Christopher Nolan",
    Actors: "Ellen Burstyn, Matthew McConaughey, Mackenzie Foy, John Lithgow",
    Plot:
      "A team of explorers travel through a wormhole in space in an attempt to ensure humanity's survival.",
    Language: "English",
    Country: "USA, UK",
    Awards: "Won 1 Oscar. Another 39 wins & 132 nominations.",
    Poster:
      "http://ia.media-imdb.com/images/M/MV5BMjIxNTU4MzY4MF5BMl5BanBnXkFtZTgwMzM4ODI3MjE@._V1_SX300.jpg",
    Metascore: "74",
    imdbRating: "8.6",
    imdbVotes: "910,366",
    imdbID: "tt0816692",
    Type: "movie",
    Response: "True",
  },
];

// For loop
var ratings = [];
for (var i = 0; i < watchList.length; i++) {
  ratings.push({
    title: watchList[i]["Title"],
    rating: watchList[i]["imdbRating"],
  });
}

// The same result, but using map
const ratings = watchList.map((item) => ({
  title: item["Title"],
  rating: item["imdbRating"],
}));

console.log(JSON.stringify(ratings));
// Logs "[{'title':'Inception','rating':'8.8'},{'title':'Interstellar','rating':'8.6'}]"
```
