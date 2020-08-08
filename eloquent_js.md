# Eloquent JavaScript

Exercises from the book [Eloquent JavaScript](https://eloquentjavascript.net/), by Marijn Haverbeke.

## Program Structure

Exercises from the chapter on [Program Structure](https://eloquentjavascript.net/02_program_structure.html).

### Looping a triangle

Write a loop that makes seven calls to `console.log` to output the following triangle:

```text
#
##
###
####
#####
######
#######
```

#### Solution

```js
let number = 0;
let hash = "#";

while (number <= 7) {
  console.log(hash);
  number += 1;
  hash += "#";
}
```

#### More eloquent solution

```js
for (let line = "#"; line.length < 8; line++) {
  console.log(line);
}
```

### FizzBuzz

Write a program that uses console.log to print all the numbers from 1 to 100, with two exceptions. For numbers divisible by 3, print "Fizz" instead of the number, and for numbers divisible by 5 (and not 3), print "Buzz" instead.

#### Solution

```js
let number = 0;

while (number <= 100) {
  if (number % 3 === 0) {
    console.log("Fizz");
  } else if (number % 5 === 0) {
    console.log("Buzz");
  } else {
    console.log(number);
  }
  number += 1;
}
```

### Chessboard

Write a program that creates a string that represents an 8×8 grid, using newline characters to separate lines. At each position of the grid there is either a space or a "#" character. The characters should form a chessboard.

Passing this string to `console.log` should show something like this:

```text
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
```

When you have a program that generates this pattern, define a binding `size = 8` and change the program so that it works for any `size`, outputting a grid of the given width and height.

#### Solution

```js
size = 8;
string = "";

for (let outer = 0; outer < size; outer++) {
  for (let inner = 0; inner < size; inner++) {
    if ((inner + outer) % 2 === 0) {
      string = string + " ";
    } else {
      string = string + "#";
    }
  }
  string = string + "\n";
}

console.log(string);
```
