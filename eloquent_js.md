# Eloquent JavaScript
Exercises from the book [Eloquent JavaScript](https://eloquentjavascript.net/), by Marijn Haverbeke.

## Program Structure
Exercises from the chapter on [Program Structure](https://eloquentjavascript.net/02_program_structure.html).

### Looping a triangle
Write a loop that makes seven calls to `console.log` to output the following triangle:
```
#
##
###
####
#####
######
#######
```

##### My solution
```js
let number = 0;
let hash = "#";

while (number <= 7) {
  console.log(hash);
  number += 1;
  hash += "#";
}
```

##### Official solution
```js

```

### FizzBuzz
Write a program that uses console.log to print all the numbers from 1 to 100, with two exceptions. For numbers divisible by 3, print "Fizz" instead of the number, and for numbers divisible by 5 (and not 3), print "Buzz" instead.

When you have that working, modify your program to print "FizzBuzz" for numbers that are divisible by both 3 and 5 (and still print "Fizz" or "Buzz" for numbers divisible by only one of those).

##### My solution
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

##### Official solution
```js

```

### Chessboard
Write a program that creates a string that represents an 8×8 grid, using newline characters to separate lines. At each position of the grid there is either a space or a "#" character. The characters should form a chessboard.

Passing this string to `console.log` should show something like this:
```
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

##### My solution
```js

```
