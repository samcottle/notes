# Basic data structures

Data can be stored and accessed in many different ways. Here we cover arrays and objects, and how to use bracket and dot notation to manipulate them, and copy and use information from them.

## Using arrays

### Getting the length

All arrays have a length, which can be accessed using `arrayName.length`:

```js
let oneDimensionalArray = [1, 2, 3, 4, 5];
console.log(oneDimensionalArray.length) // Logs 7
```

### Accessing contents using bracket notation

Bracket notation is a common way to access the content of an array (the other one being dot notation).

Each item in an array has an *index*. In JavaScript, arrays are *zero-indexed*, which means that the first item in the array is at position zero. We can use the index of an array to access or manipulate the data within it.

For example, to access the third item (which is at index `2`) in our `oneDimensionalArray`:

```js
let oneDimensionalArray = [1, 2, 3, 4, 5];
let oneVariable = oneDimensionalArray[2];
console.log(oneVariable); // Logs the third item in the array: 3
```

### Manipulating contents using bracket notation

You can also use bracket notation to manipulate the contents of an array.

For example, to change the third item (which is at index `2`) in our `oneDimensionalArray`:

```js
let oneDimensionalArray = [1, 2, 3, 4, 5];
oneDimensionalArray[2] = "three";
console.log(oneDimensionalArray); // Logs [1, 2, "three", 4, 5]
```

### Adding items to an array

The length of an array is not fixed, and the number of items within it can be added and removed. Two methods often used to do this are:

- `.push()`: Adds items to the end of the array.
- `.unshift()`: Adds items to the beginning of the array.

Here's an example of how you can use both to add items to an array, `romanNumerals`:

```js
let twentyThree = "XXIII";
let romanNumerals = ["XXI", "XXII"];

romanNumerals.unshift("XIX", "XX");
console.log(romanNumerals); // Logs ["XIX", "XX", "XXI", "XXII"]

romanNumerals.push(twentyThree);
console.log(romanNumerals); // Logs ["XIX", "XX", "XXI", "XXII", "XXIII"]
```

### Removing an item from an array

Two methods often used to remove items from an array are:

- `.pop()`: Removes items from the end of the array.
- `.shift()`: Removes items from the beginning of the array.

Here's an example of how you can use both to remove items from an array, `greetings`, and assign one of them to a variable, `dutchGreeting`:

```js
let greetings = ["What's up?", "Hello!", "Hoi!"];

let dutchGreeting = greetings.pop(); // Remove "Hoi" from end of array, and assign it to `dutchGreeting`

greetings.shift();
console.log(greetings); // Logs ["Hello!"]
```

### Removing multiple items from an array

Because removing multiple consecutive items from an array with `.pop()` and `.shift()` is inconvenient, JavaScript also has `.splice()`. This can be used to remove any number of consecutive items from an array, by specifying parameters that indicate the starting point, and the number of items to remove.

For example, to start at index `4` and remove `3` items:

```js
let array = ["Well,", "this", "is", "a", "really", "really", "really", "long", "array!"];
array.splice(4, 3);

console.log(array); // ["Well,", "this", "is", "a", "long", "array!"]
```

You can also use `.splice()` to replace (or swap out) the items you removed. This is done by specifying the items you want to swap them out with as additional parameters for `.splice()`. For example:

```js
function htmlColourNames(arr) {
  arr.splice(0, 2, 'DarkSalmon', 'BlanchedAlmond');
  return arr;
}

console.log(htmlColourNames(['DarkGoldenRod', 'WhiteSmoke', 'LavenderBlush', 'PaleTurqoise', 'FireBrick']));
// Logs [ "DarkSalmon", "BlanchedAlmond", "LavenderBlush", "PaleTurqoise", "FireBrick" ]
```

### Copying array items

If you want to access and use (in other words *extract*) multiple items from an array, use `.slice()`. This method leaves the original array unchanged.

You can use this to create a new array from an existing array. For example, to get the values between index `2` and `4` of the `forecast` array:

```js
function forecast(arr) {
  return arr.slice(2, 4);
}
console.log(forecast(['cold', 'rainy', 'warm', 'sunny', 'cool', 'thunderstorms'])); // Logs ['warm', 'sunny']
```

**Note:** Extraction occurs up to, but not including, the second parameter. This is why it's not `arr.slice(2, 3)`.

With ES6, there's an easy way to copy all the contents of an array: the *spread operator*. The syntax for this is identical to a spread operator used anywhere else (`...`). For example, to get all the contents of the array `arr`, you'd use `[...arr]`:

```js
function copyMachine(arr, num) {
  let newArr = [];
  while (num >= 1) {
    newArr.push([...arr]);
    num--;
  }
  return newArr;
}

console.log(copyMachine([true, false, true], 2));
```

You can use similar logic to concatenate and combine multiple arrays into one:

```js
function spreadOut() {
  let fragment = ['to', 'code'];
  let sentence = ['learning', ...fragment, 'is', 'fun']; // change this line
  return sentence;
}

console.log(spreadOut()); // Logs [ "learning", "to", "code", "is", "fun" ]
```

### Checking for the presence of a value in an array

If you want to check whether an array contains a certain value, use the `.indexOf()` method.

When the value is successfully found, `.indexOf()` will return the index of that value (and if the value is not found, it will return an index of `-1`).

Here's an example of a function that checks an array (`arr`) for the presence of an element (`elem`):

```js
function quickCheck (arr, elem) {
  if (arr.indexOf(elem) >= 0) {
    return true;
  }
  return false;
}

console.log(quickCheck(['squash', 'onions', 'shallots'], 'onions')); // Logs true
```

### Iterating through an array with a for loop

The most versatile way to iterate over an array is the humble `for` loop. This lets you loop through an array and test each item in the array and against a condition.

For example, to loop through an array (`arr`) so that any nested arrays containing the element (`elem`) are filtered and removed (in other words, nested arrays that do not have the element are added to a new array `newArr`):

```js
function filteredArray(arr, elem) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
      if (arr[i].indexOf(elem) == -1) {
      newArr.push(arr[i]);
      }
  }
  return newArr;
}

console.log(filteredArray([[3, 2, 3], [1, 6, 3], [3, 13, 26], [19, 3, 9]], 3)); // Logs []
console.log(filteredArray([[10, 8, 3], [14, 6, 23], [3, 18, 6]], 18)); // Logs [[ 10, 8, 3 ], [ 14, 6, 23 ]]
```

### Working with multi-dimensional arrays

Arrays can be nested inside arrays, creating a *multi-dimensional* array.

For example, this array that goes 5 levels deep:

```js
let nestedArray = [
  ['deep'],
  [
    ['deeper'], ['deeper']
  ],
  [
    [
      ['deepest'], ['deepest']
    ],
    [
      [
        ['deepest-est?']
      ]
    ]
  ]
];

console.log(nestedArray[2][1][0][0][0]); // Logs the contents of the array nested five levels deep: 'deepest-est?'
nestedArray[2][1][0][0][0]) = 'deeper still'; // Changes the value of the datum from 'deepest-est?' to 'deeper still'
console.log(nestedArray[2][1][0][0][0]); // Now logs 'deeper still'
```

## Using objects

JavaScript object are similar to arrays, but contain *key-value pairs*. These are pieces of data (*values*) that are mapped to specific identifiers (*keys*, or *properties*). Here's a very simple example of an object containing types of `foods` and their quantity:

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28
};
```

Like an array, an object's data can be accessed using bracket notation:

```js
let numberOfApples = foods["apples"];
console.log(numberOfApples);
```

But they can also be accessed using dot notation:

```js
let numberOfApples = foods.apples;
```

### Adding key-value pairs to an object

Both dot and bracket notation can also be used to add data to an object.

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28
};

foods.bananas = 13; // dot notation
foods.grapes = 35; // dot notation
console.log(foods); // { apples: 25, oranges: 32, plums: 28, bananas: 13, grapes: 35 }
foods["strawberries"] = 27;
console.log(foods); // { apples: 25, oranges: 32, plums: 28, bananas: 13, grapes: 35, strawberries: 27 }
```

### Accessing property names with bracket notation

Bracket notation can be useful when you need to know the value associated with a key that exists within an object.

For example, if we wanted to know how many apples were in the `foods` object, we could use:

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28,
  bananas: 13,
  grapes: 35,
  strawberries: 27
};

function checkInventory(scannedItem) {
  return foods[scannedItem];
}

console.log(checkInventory("apples")); // Logs 25, the number of apples
```

### Deleting a property in an object

You can use the `delete` keyword to remove a property from an object. Here's an example:

```js
let foods = {
  apples: 25,
  oranges: 32,
  plums: 28,
  bananas: 13,
  grapes: 35,
  strawberries: 27
};

delete foods.oranges;
delete foods.plums;
delete foods.strawberries;

console.log(foods); // Logs { apples: 25, bananas: 13, grapes: 35 }
```

### Checking an object for a property

You can use the `.hasOwnProperty()` to check for the presence of a particular property. You can also use the `in` keyword.

Here's how you'd use both to test for the presence of the `users` Alan, and Jeff, and Sarah, and Ryan:

```js
let users = {
  Alan: {
    age: 27,
    online: true
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: true
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function isEveryoneHere(obj) {
  return obj.hasOwnProperty("Alan" && "Jeff" && "Sarah" && "Ryan");
}
console.log(isEveryoneHere(users)); // true

function areTheyReally(obj) {
  return "Alan" && "Jeff" && "Sarah" && "Ryan" in users;
}
console.log(areTheyReally(users)); // true
```

### Iterating through an object

To iterate through an object to check for certain values you can use a `for...in` statement.

Here's an example of how you would loop through the object `users`, to check the number that are online:

```js
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function countOnline(obj) {
  let result = 0;
  for (let user in obj) {
    if (obj[user].online === true) {
      result++;
    }
  }
  return result;
}

console.log(countOnline(users)); // 2
```

### Generating an array of object keys

To get a an array of keys from an object you can use the `Object.keys()` method.

For example:

```js
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function getArrayOfUsers(obj) {
  return Object.keys(obj);
}

console.log(getArrayOfUsers(users)); // [ "Alan", "Jeff", "Sarah", "Ryan" ]
```
