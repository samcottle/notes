# Basic algorithm scripting

An algorithm is a series of steps that are followed to achieve an outcome.

This section of freeCodeCamp is a series of exercises, but uses concepts that haven't already been explained in the course. Therefore, I'm just dumping the exercises in here as examples of how to achieve certain outcomes.

## Reverse a string

Reverse the provided string.

You may need to turn the string into an array before you can reverse it.

Your result must be a string.

```js
function reverseString(str) {
  let arr = str.split(""); // Splits the string into an array. Each item in the array is one letter.
  arr.reverse(); // Reverses the order of the items in the array.
  return arr.join(""); // Joins the array into a string.
}

console.log(reverseString("hello")); // Logs "olleh"
```

## Factorialize a Number

Return the *factorial* of the provided integer. If the integer is represented with the letter `n`, a factorial is the product of all positive integers less than or equal to `n`.

Factorials are often represented with the shorthand notation `n!`

For example: `5! = 1 * 2 * 3 * 4 * 5 = 120`

Only integers greater than or equal to zero will be supplied to the function.

```js
function factorialize(num) {
  let listOfNums = [];
  if (num === 0) {
    return 1;
  }
  for (var i = 1; i <= num; i++) {
    listOfNums.push(i);
  }
  const reducer = (accumulator, currentValue) => accumulator * currentValue;
  let factor = listOfNums.reduce(reducer);
  return factor;
}

console.log(factorialize(5)); // Logs 120 (1 * 2 * 3 * 4 * 5)
console.log(factorialize(0)); // Logs 1, as per the if statement
```

**Note:** The reason that is to pass the test `factorialize(0) should return 1.`, which is apparently how factorializing works.

This can also be solved using recursion:

```js
function factorialize(num) {
  if (num === 0) { return 1; }
  return num * factorialize(num-1);
}

factorialize(5);
```

## Find the Longest Word in a String

Return the length of the longest word in the provided sentence.

Your response should be a number.

```js
function findLongestWordLength(str) {
  let wordsArr = str.split(" "); // Splits the string into an array of individual words.
  let longest = 0;

  // Loops through array, checking if a word in the array is longer than the value of `longest`
  // If it is, `longest` is overwritten with the length of that word.
  for (var i = 0; i < wordsArr.length; i++) {
    if (wordsArr[i].length > longest) {
      longest = wordsArr[i].length;
    }
  }
  return longest;
}

console.log(findLongestWordLength("The quick brown fox jumped over the lazy dog")); // 6 (number of characters in the longest word, "jumped")
```

## Repeat a String Repeat a String

Repeat a given string `str` (first argument) for `num` times (second argument). Return an empty string if `num` is not a positive number.

```js
function repeatStringNumTimes(str, num) {
  var n = 0
  var text = "";

  while(n < num) {
    text += str;
    n++;
  }
  return text;
}

console.log(repeatStringNumTimes("abc", 3)); // Logs "abcabcabc"
```

Another way to achieve this (which fails freeCodeCamp's test, due to the use of the `repeat` method) is:

```js
function repeatStringNumTimes(str, num) {
  if(num <= 0) {
    return "";
  } else {
  return str.repeat(num);
  }
}

console.log(repeatStringNumTimes("abc", 3)); // Logs "abcabcabc"
```
