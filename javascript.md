# Basic JavaScript

## General

- JavaScript is case-sensitive. `myVar` != `MYVAR` or `myvar`.
- Recommend using camelCase.

## Comments

Put `//` before text to make it a comment.

For multi-line comments, put the text like this `/* This is a
multi-line comment */`.

## Working with the console

- `console.log()`: Logs data to the console.
- `console.clear()`: Clears the console.

## Values and types

JavaScript has the following types of values:

- string (`"hello"`)
- number (`6`)
- boolean (`true`)
- `null` and `undefined`
- object (`a = { b: "c" };`)
- symbol (as of ECMAScript 6)

The `typeof` operator can be used to find the type of a particular variable:

```js
var a = "hello";

console.log(typeof a); // Logs "hello" to the console.
```

## Working with variables

These are how computers store and manipulate data dynamically. Basically, you use a label to point to some specific data, rather than use the data itself. Can think of them as being similar to x and y values in algebra, but also capable of representing more than just numbers.

Creating a variable is referred to as "declaring" a variable. To declare a variable, you'd usually put `var` in front of it, and a `;` after it. In ECMAScript 6, a variable can instead be preceded with:

- `let`: to declare a variable within a very specific scope.
- `const`: to declare a variable that will never be changed.

So, for example, `var ourName;` declares a variable called ourName.

Variable names can be made up of numbers, letters, and `$` or `_`, but can't contain spaces or start with a number.

### Assigning values to variables

Values are stored with an *assignment* operator. Basically an `=`. So `myVar = 5` could also be described as "assigning the number 5 to `myVar`.

Example: `var myVar = 5;` creates a variable called `myVar` and assigns a value of `5` to it. This is also referred to as *initializing* the variable.

*Note:* when you get `NaN` (Not a Number) as an error code, this means you've forgotten to declare a variable, and it's tried to initialize... nothing. Similarly, `"undefined"` means that you've tried to concatenate a string that hasn't been defined.

### Built-in methods

In addition to `typeof`, there are several built-in methods that can be used to manipulate variables:

- `.length`: Returns the number of characters of a variable.
- `.toUpperCase()`: If the variable is a string, returns the string in upper case.
- `.toFixed()`: If the variable is an integer, returns the integer to the number of decimals specified.

For example:

```js
var a = "hello";
var b = 3.14159;

console.log(a.length); // 5
console.log(a.toUpperCase()); // HELLO
console.log(b.toFixed(4)); // 3.1416
```

## Working with numbers

The `number` data type represents numeric data.

### Adding numbers

You can probably guess: `var sum = 10 + 10;` gives you a `sum` of `20`.

### Subtracting numbers

Ditto: `var difference = 45 - 33;` gives you a `difference` of `12`.

### Multiplying numbers

`var product = 8 * 10;` gives a `product` of `80`.
Can also multiply decimals: `var product = 2.0 * 2.5;` would give a `product` of `5`.

### Dividing numbers

`var quotient = 66 / 33;` gives a `quotient` of `2`.
Can also divide decimals: `var quotient = 4.4 / 2.0;` gives a `quotient` of `2.2`.

#### Remainders

Remainders operator is `%`. Unsurprisingly, it gives you the remainder. Basically, whatever is left over after dividing two numbers. Example: `5 % 2 = 1` (because it's what's left over afterwards).

This is often used to determine whether a number is even or odd (because if a `number % 2` has a remainder of `0` then that `number` is even).

### Increments (adding/subtracting 1 to/from a number)

Use `++` at the end of the number is basically n+1. But you don't even need to specify it in full, for example:
`n = n + 1` == `n++`.

Similarly, `--` also works to subtract 1.

### Compound assignment

Compounds are when you'd use, for example, `myVar += 5` in place of `myVar = myVar + 5;`. It performs the addition, etc., as well as the =.

Can be used for `+`, `-`, `*`, and `/`.

## Strings

A *literal string* is another name for your bog standard string.

A *template literal* is a string surrounded in backticks. This can be useful if you need to span multiple lines, and also if you want to compute a value within a string (using `${}`). For example:

```js
console.log(`half of 100 is ${100 / 2}`) // Logs `half of 100 is 50`
```

### Using quotes in strings

The simplest way to do this is to use both single quotes (`'`) and double quotes (`"`). If you use `"`s for the string then use `'`s for the quotes within it.

Alternatively, you can use a `\"` within the string to specify where quotes start and finish. Example: `var sampleStr = "Alan said, \"Peter is learning JavaScript\".";`
Which would `print` as `"Alan said, "Peter is learning JavaScript"."`

The `\` is referred to as an *escape string*, *escape sequences*, or *escapes*. Here's some more...

### Escape sequences

The following can be used:

- `\'`: single quote.
- `\"`: double quote.
- `\\`: backslash.
- `\n`: newline.
- `\r`: carriage return.
- `\t`: tab.
- `\b`: backspace.
- `\f`: form feed.

**Note:** There shouldn't be any spaces around escape sequences.

### Concatenating strings

`"My name is " + "Sam"` is the same as `My name is Sam`.

Can also do this with `+=` operator. So:

```js
var myName = "My name is ";
myName += "Sam";

console.log(myName); // Prints "My name is Sam"
```

### Getting a string length

Get the number of characters in a string using `.length`. So if `varName = "string"` then `varName.length` would output `6`.

### Bracket notation

This is how you get a character at a specific index in a string. JavaScript uses *zero-based indexing*, meaning the indexing starts at `0`, not `1`. Square brackets, `[` and `]` , and a number in between which is used to fetch the character you want. Example:

```js
word = "string";
firstLetterOfWord = word[0];
```

#### Using bracket notation to get the last letter of a string

Easiest way to do this is to combine `.length` and bracket notation. But remember zero-based indexing!
Example:

```js
word = string;
var lastLetterOfString = word[word.length - 1];
```

Similar logic can be used to get the second/third/fourth/nth to last character of a string.

## Working with functions

*Functions* are used for dividing up code into usable parts (like a mini-program within the script).

They're usually used to:

- Section off pieces of code, making it easier to manage.
- Run repeated operations.
- Or both.

They wrap around code blocks that contain *statements*, which will be run. They usually involve a combination of variables, operations, and conditions.

When run, a function will either:

- Give you an immediate result.
- Provide an output, a *return value* that can be used by other functions.

### Building a function

Functions follow a standard structure:

1. The word `function`.
2. A name, such as `myFunction`.
3. Parentheses `()`, that define the parameters that will be used in the function.
4. Curly brackets, `{}`, that wrap around the code that will be run. Whatever is stored here is *called* (or *invoked*) when the function is used.

**Note**: Functions can access any variables (`var`, `let`, `const`) declared in the scope outside it, but any variables that you declare inside a function won't be available outside that function (i.e. they are *local*).

Basic example for defining (or *storing*) a function:

```js
function functionName() {
  console.log("Hello World");
}
```

They're usually defined just before they're called, which makes it easier for other people to read. To use (or *invoke* or *call*) a function:

```js
functionName(); // This would print "Hello World" in the console.
```

### Using parameters, for *arguments* sake

*Parameters* are variables that act as placeholders for values you want to input to a function when it is called. The act of inputting is also referred to as *passing*, and the act of calling a function is known as an *argument*. They're great for making functions reusable.

Here's an example, showing a function that is defined, which is then re-used a few times by calling additional arguments:

```js
function functionWithArgs(arg1, arg2) {
  console.log(arg1 + arg2);
}
functionWithArgs(3, 6); // Prints 9 in the console (the sum of 3 and 6).
functionWithArgs(7, 2); // Prints 14 in the console.
functionWithArgs(3, 7); //Prints 21 in the console.
```

**Note:** If you don't have a parameter/argument, `undefined` will be returned.

#### Default parameters

You can write an`=` operator after a parameter, followed by an expression. The value of this expression will be the default parameter, used in situations where a parameter is not specified. For example, to make `2` the default `exponent` (in case it is not specified) you would use:

```js
function power(base, exponent = 2) {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
}

console.log(power(4));
// 16
console.log(power(2, 6));
// 64
```

### Returning a value from a function

Basically a reverse-argument, `return` sends a value back out of a function (instead of passing it in).
Example:

```js
function plusThree(num) {
  return num + 3;
}
var answer = plusThree(5); // In this case, 8. So plusThree takes an argument for num, and returns a value equal to num + 3.`
```

Without *returning* a value you'll end up with *undefined* in the `console.log`.

### Defining the scope for functions

*Scope* is basically the visibility of variables. Variables defined outside of a function, with `var`, have *global scope* (are visible everywhere in the JavaScript code). Variables defined within a `function` have *local* scope (are only visible to that function).
Can have local and global variables with the same name, and the local variable will take precedence in this scenario. For example, :

```js
var outerWear = "T-Shirt";
function myOutfit() {
  var outerWear = "sweater";
  return outerWear;
}
myOutfit();
```

### Queues

A `queue` is a data structure (i.e. array) where items are kept in order. Can add new items to the back of the queue, and remove old items from the front of the queue.

#### Shifting items in a queue

To remove the first item from the queue and return it, use `.shift()`.

#### Pushing items in a queue

To add a new item to the back of the queue, us `.push()`. Here's an example of both `.shift` and `.push()`:

```js
function nextInLine(arr, item) {
  arr.push(item);
  return arr.shift();
}

var testArr = [1,2,3,4,5];

console.log(nextInLine(testArr, 6)) // This would log 1 to the console, and testArr would then be 2,3,4,5,6.
```

## Working with booleans

Either `true` (on) or `false` (off) (and without quotes). Here's how booleans become really useful...

### If statements

Used to make decisions in code, and act a bit like a switch. `if` statements will only execute the code under certain conditions (for example, when a statement is `true`).

#### Comparison operators

##### Equality operators

Basically the `==` things (not to be confused with a plain old `=`, which is for assigning values to variables, etc).
Compares two values, and returns `true` if they're equivalent, or `false` if they're not. Useful for If statements because they can be used to execute code under certain conditions. For example:

```js
function equalityTest(myVal) {
  if (myVal == 10) {
     return "Equal";
  }
  return "Not Equal";
}

console.log(equalityTest(10)) // Would log "Equal" in the console.
```

Would execute the code in curly braces (returning "Equal") if myVal is equal to `10`.

##### Inequality operators

Basically, the `!=` (not equal) thing. There's also a *strict inequality* operator, which is `!==`.

##### Greater than operators

It's the `>` thing. Can also use `>=` for *greater than or equal to*.

##### Less than operators

It's the `<` thing. Can also use `<=` for *less than or equal to*.

Comparison can also be done between integers `5` and strings `"5"`, which is called *type conversion*. There's also strict equality (`===`), which means the two have to be exactly the same (i.e. both integers, or both strings).

##### Using multiple operators

This is often referred to as the *logical and* operator. For JavaScript, this is a `&&`. Useful for scenarios like this, where you want to find the number between 5 and 10, but don't want to write out multiple *if* statements:

```js
if (num > 5 && num < 10) {
  return "Yes";
}
return "No";
```

Similarly, there's the *logical or*, which is `||` (each of these is apparently referred to as a *pipe symbol*):

```js
if (num > 10 || num < 5) {
  return "No";
}
return "Yes";
```

This will return "Yes" only if num is between 5 and 10 (**5 and 10 included**).

### Else statements

So if the conditions inside an `if` statement are `false`, then what happens? Use an  `else` statement to take care of this:

```js
if (num > 10) {
  return "Bigger than 10";
} else {
  return "10 or Less";
}
```

### Else if statements

Use this when there are multiple conditions that need to be addressed:

```js
if (num > 15) {
  return "Bigger than 15";
} else if (num < 5) {
  return "Smaller than 5";
} else {
  return "Between 5 and 15";
}
```

Keep in mind that these statements run in order from top to bottom, so be careful which statement goes first, etc.

#### Switch statements

Similar to `if`, `else`, and `else if` statements, but good if you have lots of statements. Example:

```js
function caseInSwitch(val) {
  var answer = "";
  switch(val) {
    case 1:
      return("alpha");
      break;
    case 2:
      return("beta");
      break;
    case 3:
      return("gamma");
      break;
    case 4:
      return("delta");
      break;
  }
  return answer;  
}
```

Here, each `case` is a possible statement. Adding `caseInSwitch(3);` to the end, for example, would result in `"gamma"` being logged in the console.
The code for each `case` is run until a `break;` is encountered. If there's no `break`, all the statements will be run, as a group, until there is a break (if that makes sense). So for:

```js
switch(val) {
  case 1:
  case 2:
  case 3:
    result = "1, 2, or 3";
    break;
  case 4:
    result = "4 alone";
}
```

`case`s 1, 2, and 3 will produce the same result.

Can also make a `switch` statement default, which effectively makes it the final `else` statement. In other words, if there's no matching `case` then the default is used:

```js
function switchOfStuff(val) {
  var answer = "";
  switch(val) {
    case "a":
      return("apple");
      break;
    case "b":
      return("bird");
      break;
    case "c":
      return("cat");
      break;
    default:
      return("stuff");
      break;
  }
  return answer;  
}
```

#### Return

`return` is used to end a function. So for this:

```js
function myFun() {
  console.log("Hello");
  return "World";
  console.log("byebye")
}
myFun();
```

`"byebye"` will never be logged, because the `return` essentially ends/exits the function.

## Working with arrays

An array is a special type of *object*, which stores data (known as *elements*) in one place. Arrays fit between square brackets `[` and `]`. Example: `var sandwich = ["peanut butter", "jelly", "bread"]`.

Unlike other objects, the elements in an array are accessible using a numerically indexed position. Arrays can be nested inside other arrays, which is referred to as a *multi-dimensional array*. Example: `[["Bulls", 23], ["White Sox", 45]]`.

Accessing the data in an array is done with bracket notation, for example:

```js
var arr = [
  [1,2,3],
  [4,5,6],
  [7,8,9],
  [[10,11,12], 13, 14]
];
arr[3]; // equals [[10,11,12], 13, 14]
arr[3][0]; // equals [10,11,12]
arr[3][0][1]; // equals 11
```

Unlike strings, array entries are *mutable* and can be changed freely. In other words, you can change the data at index `0` of ourArray with, for example:

```js
var ourArray = [50,40,30];
ourArray[0] = 15; // and ourArray now equals [15,40,30]
```

### Indexes

Data within an array is accessed using an index. These are also *zero-based* (i.e. start at `0` rather than `1`). Example:

```js
var array = [50,60,70];
array[0]; // equals 50
var data = array[1]; // equals 60.
```

**Note:** As above, don't put any spaces between the array name and the square brackets.

### Manipulating arrays

Data can be both added or removed from an array.

#### Appending data

To append data to the end of an array use `.push()`. Basically pushes parameters to the end of the array. Example:

```js
var arr = [1,2,3];
arr.push(4); // And arr is now [1,2,3,4].
```

To append to the beginning of an array, use `unshift()`. Example:

```js
var myArray = [["John", 23], ["dog", 3]];
myArray.unshift(["Paul", 35]); // Adds an array with ["Paul", 25] to the start of myArray.
```

#### Removing data

`.pop()` takes data element off the end of the array and returns that data element (so it can be used to store that last data element in another variable).
Example:

```js
var threeArr = [1, 4, 6];
var oneDown = threeArr.pop();
console.log(oneDown); // Returns 6
console.log(threeArr); // Now returns [1, 4]
```

Similarly, `.shift()` takes it from the first data element in an array. Example:

```js
var myArray = [["John", 23], ["dog", 3]];
var removedFromMyArray = myArray.shift();
```

This takes `["John", 23]` out of the array and stores it as a variable called `removedFromMyArray`.

## Working with objects

An *object* is a compound value, similar to an *array*, but data is accessed using *properties* (or *locations*). They're for storing structured data. For example, this cat (with the properties of the `cat` stored as strings):

```js
var cat = {
  "name": "Whiskers",
  "legs": 4,
  "tails": 1,
  "enemies": ["Water", "Dogs"]
};
```

**Note:**

- For single-word string properties you don't need the quotes (i.e. `"name"` can be `name`).
- Use a comma between each property, instead of a semi-colon.

### Accessing properties

Properties within an array can be accessed with:

- Dot notation: a `.` (this is shorter, and more human readable).
- Bracket notation: the `[` and `]`, like you would for an array. You'll also need to use this one if the object has a space in it.

#### With dot notation

```js
var testObj = {
  "hat": "ballcap",
  "shirt": "jersey",
  "shoes": "cleats"
};

var hatValue = testObj.hat;
var shirtValue = testObj.shirt;
```

#### With bracket notation

```js
var testObj = {
  "an entree": "hamburger",
  "my side": "veggies",
  "the drink": "water"
};

var entreeValue = testObj["an entree"];
var drinkValue = testObj["the drink"];
```

#### Accessing properties with variables

Very similar to bracket notation, but with values stored as variables. This can be really useful for tasks like accessing a lookup table.

```js
var dogs = {
  Fido: "Mutt", Hunter: "Doberman", Snoopie: "Beagle"
};
var myDog = "Hunter";
var myBreed = dogs[myDog];
console.log(myBreed); // "Doberman"
```

#### Updating an object property

Take an object like `ourDog`:

```js
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};
```

Properties, such as the `name`, can be updated using either:

- Dot notation: `ourDog.name = "Doggy";`
- Bracket notation: `ourDog["name"] = "Doggy";`

So now if we accessed `ourDog.name`, it will have changed from `"Camper"` to `"Doggy"`.

#### Adding properties to an object

Take an object like `ourDog`:

```js
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};
```

We can add a property, such as `bark`, to the object using either:

- Dot notation: `ourDog.bark = "Bow-wow";`
- Bracket notation: `ourDog["bark"] = "Bow-wow";`

So now we can access `ourDog.bark`, which has a value of `"Bow-wow"`.

#### Deleting properties from an object

Take an object like `ourDog`:

```js
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"],
  "bark": "Woof"
};
```

To delete the `bark` property, we would use `delete ourDog.bark;`.

### Object lookups

Objects work a bit like an index, using keys:values to store data. Here's an example of a lookup:

```js
var alpha = {
  1:"Z",
  2:"Y",
  3:"X",
  4:"W",
  ...
  24:"C",
  25:"B",
  26:"A"
};
alpha[2]; // "Y"
alpha[24]; // "C"

var value = 2;
alpha[value]; // "Y"
```

### Checking an object for a property

To check whether a property exists within an object you can use the `.hasOwnProperty(propertyname)` method. This returns either `true` or `false`, depending on whether the property was found. For example:

```js
var myObj = {
  top: "hat",
  bottom: "pants"
};
myObj.hasOwnProperty("top"); // true
myObj.hasOwnProperty("middle"); // false
```

### Handling complex objects

JavaScript Object Notation (JSON) is often used to handle more complex data objects, where you can nest arrays within arrays, such as the `formats` here:

```js
{
  "artist": "Daft Punk",
  "title": "Homework",
  "release_year": 1997,
  "formats": [
    "CD",
    "Cassette",
    "LP"
  ],
  "gold": true
}
```

When using JSON, a comma needs to be placed after each object in the array, except the last one.

#### Accessing nested objects

This can be done with either dot or bracket notation, as shown below:

```js
var ourStorage = {
  "desk": {
    "drawer": "stapler"
  },
  "cabinet": {
    "top drawer": {
      "folder1": "a file",
      "folder2": "secrets"
    },
    "bottom drawer": "soda"
  }
};
ourStorage.cabinet["top drawer"].folder2; // "secrets"
ourStorage.desk.drawer; // "stapler"
```

**Note:** If the object has a space in the name, use bracket notation.

#### Accessing nested arrays

Array bracket notation can be used to access objects in nested arrays:

```js
var myPlants = [
  {
    type: "flowers",
    list: [
      "rose",
      "tulip",
      "dandelion"
    ]
  },
  {
    type: "trees",
    list: [
      "fir",
      "pine",
      "birch"
    ]
  }  
];

var secondTree = myPlants[1].list[1]; // "pine"
```

## Loops

These are used to run the same code multiple times.

### While loops

This runs a loop `while` a specified condition is true. Here's an example:

```js
var myArray = [];

var i = 0;
while(i < 5) {
  myArray.push(i);
  i++;
}
```

So here, a `while` loop will keep `push`ing the incremental values `0` through `4` into `myArray`. It stops at `4` because the loop is set to run until `i < 5`.

While loops often contain two conditions. For example, to keep track of a result, and another as a counter:

```js
let result = 1;
let counter = 0;
while (counter < 10) {
  result = result * 2;
  counter = counter + 1;
}

console.log(result); // 1024
```

### For loops

These run the same code `for` a specified number of times, and consist of three semicolon-separated statements:
`for(initialization; condition; final-expression)`

Where:

- **initialization**: Defines and sets up the loop variable; the starting point.
- **condition**: This is evaluated at the beginning of each loop, and the loop will continue to execute so long as it results in `true` (and repeats until it results in `false`).
- **final-expression**: Defines what is executed for each loop.

So the same example we have in the `while` loop above can also be expressed with a `for` loop:

```js
var myArray = [];
for (var i = 0; i < 5; i++) {
  myArray.push(i);
}
```

You can combine this with *compound assignment* to have the loop create an array with, say, even numbers only using `i += 2` as the **final-expression**.

#### Iterating through values using for loops

This is a relatively common JavaScript task. Here's an example for an array called `myArr`:

```js
var myArr = [ 2, 3, 4, 5, 6];

var total = 0;
for (var i = 0; i < myArr.length; i++) {
  total += myArr[i]; // 20
}
```

Here, the `for` loop will start at position `0`, and will continue running as many times as there are elements in the array (**Note:** The reason this is `i < myArr.length` is because we start at position `0` of the array. So the element at the second position is actually `1`, or `<2`). Finally, the `i++` is another way of saying `i = i + 1`, or "move on to the next element".

#### Loops and nesting

For each level of nesting, you're creating another `for` loop inside the existing `for` loop. So here we're creating a `for` loop `j` inside of `for` loop `i`:

```js
var arr = [
  [1,2], [3,4,5], [6,7]
];
for (var i = 0; i < arr.length; i++) {
  for (var j = 0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}
```

**Note:** The **condition** for the nested array is `j < arr[i].length`.

### Do...while loops

Basically, a *do...while* loop will run (`do`) at least once, and continue to run until a condition (`while`) has been met.

So in the following example:

```js
var myArray = [];
var i = 10;

do {
  myArray.push(i);
  i++;
} while (i < 15);
```

This `for...while` loop will `push` the value `i` (`10`) onto the array, and then continue `push`ing values into the array until `14`. It will then stop as the condition has been met (i.e. `= 15`).

## Working with random numbers

There are several built-in JavaScript functions that you can use to work with random numbers:

- `Math.random()`: Generates a random decimal between `0` and (almost) `1`.
- `Math.floor()`: Rounds down to the nearest whole number.

### Generating a random number whole number (between 0 and x)

Here's how you could generate a random number between `0` and `19`:

```js
var randomNumberBetween0and19 = Math.floor(Math.random() * 20);
```

Breaking this down, we are:

1. Using `Math.random()` to generate a random number between `0` and (almost) `1`.
2. Multiplying this by `20`, which generates a random number between `0` and (almost) `20`.
3. Using `Math.floor()` to round the result down.
**Note**: Because `Math.random()` will never quite generate `1`, this means that `Math.random() * 20` will never quite generate `20`. Because `Math.floor()` always rounds down, the highest number you can generate is `19`.

### Generating a random whole number between x and y

Here's how you could generate a random number between `20` and `29`:

```js
function randomRange(myMin, myMax) {
  return Math.floor(Math.random() * (myMax - myMin +1) + myMin);
}

console.log(randomRange(20, 29));
```

## Converting to an integer

To convert a string to an integer, use the built-in `parseInt` function. By passing in a string (for example, `var a = parseInt("007");`) you'll convert this string (`"007"`) into an integer (`007`).

You can also pass a radix into `parseInt` (for example `parseInt(string, radix)`), so `var a = parseInt("11", 2);` returns the `"11"` in the binary system (base 2), which is an integer with the value `3`.

**Note:** If `parseInt` returns `NaN` (not a number) it means that the string contains values that couldn't be converted, for example `parseInt("hello");`.

## Ternary Operators

Also known as a *Conditional Operator*, the Ternary Operator is a single line `if`/`else` expression. It runs an operation on three values, using the following syntax:

```js
condition ? statement-if-true : statement-if-false
```

So instead of:

```js
function checkEqual(a, b) {
  if (a===b) {
    return true;
  } else {
    return false;
  }
}

checkEqual(1, 2);
```

You can use the Ternary Operator:

```js
function checkEqual(a, b) {
    return a===b ? true : false;
}

checkEqual(1, 2);
```

The same logic works if there are more conditions. So the following `if`/`else if`/`else` statement:

```js
function checkSign(num) {
  if (num > 0) {
    return "positive";
  } else if (num < 0) {
      return "negative";
  } else {
      return "zero";
  }
}

checkSign(3);
```

Can be expressed with the Ternary Operator:

```js
function checkSign(num) {
  return (num > 0) ? "positive" : (num < 0) ? "negative" : "zero";
}

checkSign(3);
```
