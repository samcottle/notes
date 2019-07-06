# Eloquent JavaScript

Exercises from the book [Eloquent JavaScript](https://eloquentjavascript.net/), by Marijn Haverbeke.

## Program Structure

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

My answer:
```js
let number = 0;
let hash = "#";

while (number <= 7) {
  console.log(hash);
  number += 1;
  hash += "#";
}
```

Official answer:
```js

```
