# Regular expressions

Regular expressions (also known as *regex* or *regexp*) are widely used in programming. They help you match, search, and replace text by using a combination of symbols and text.

Here is how you can use them in JavaScript.

## Matching

The `test()` method is used to match part of a string. For example, if I wanted to find the word `"the"` in the string `"The dog chased the cat"` I could use the regex `/the/`.

In JavaScript, a common way to test this would use the `.test()` method:

```js
let testStr = "Sam likes to code";
let testRegex = /code/;
let result = testRegex.test(testStr);

console.log(result); // true
```

This returns either `true` or `false`.

**Note:** This is case sensitive.

### Matching possibilities

To search a string for multiple patterns you can use the `|` operator. So if you wanted to search a string for either `yes` or `no` you could use `/yes|no/`, or for `yes` or `no` or `maybe` with `/yes|no|maybe/`.

### Matching non-literal strings

When using `test()` to match part of a string, it will only work when there is a literal match (so `code` would not match for `Code` or `CODE`).

You can match these using a *flag*. There are several regex flags, but to ignore the case you would use the `i` flag. Here's an example:

```js
let testStr = "Sam likes to code";
let testRegex = /CODE/i;
let result = testRegex.test(testStr);

console.log(result); // true. As would "Code" or "coDE"
```

### Extracting matches

If you need more than a simple `true` or `false`, you can *extract* the match too. For example:

```js
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = extractStr.match(codingRegex);

console.log(result); // "coding"
```

#### Extracting multiple matches

For strings like `"Boom, boom, boom, boom!"`, using `match()` will only give you the first result. To find all instances of a match, use the `g` flag. For example:

```js
let vengaSong = "Boom, boom, boom, boom...";
let vengaRegex = /boom/g;
let result = vengaSong.match(vengaRegex);

console.log(result); // ["boom", "boom", "boom"]
```

But wait, what happened to the first `"Boom"`? Without the `i` flag, `match()` is case sensitive. But you can combine flags (for example, `gi` combines the *multiple* (`g`) and the *non-literal* (`i`) flags):

```js
let vengaSong = "Boom, boom, boom, boom...";
let vengaRegex = /boom/gi;
let result = vengaSong.match(vengaRegex);

console.log(result); // ["Boom", "boom", "boom", "boom"]
```

#### Using wildcards

When you don't know the exact match in a pattern, and writing regex to cover all possible options would be time consuming (as well as being inflexible), you can use a wildcard (`.`). This is also referred to as a *dot* or a *period*, and you use it like this:

```js
let exampleStr = "Let's have fun with regular expressions!";
let unRegex = /.un/;
let result = unRegex.test(exampleStr);

console.log(result); // true
```

#### Using character classes

When you want to search for a range of characters that match, you can use *character classes*. Any characters placed inside `[squarebrackets]` will match.

For example, if you wanted to search for "bag", "big", and "bug", but *not* "bog" you could use:

```js
let bagStr = "bag";
let bigStr = "big";
let bugStr = "bug";
let bogStr = "bog";
let regEx = /b[aiu]g/;
bagStr.match(regEx); // "bag"
bigStr.match(regEx); // "big"
bugStr.match(regEx); // "bug"
bogStr.match(regEx); // null
```

You can also match a range of characters, with a hyphen. Such as `[a-z]`, `[0-9]`, or `[a-r3-7]`. For example:

```js
let catStr = "cat";
let catStr = "bat";
let catStr = "mat";
let reGex = /[a-e]at/;
catStr.match(regEx); // "cat"
batStr.match(regEx); // "bat"
matStr.match(regEx); // null
```

##### Excluding characters

If you, instead, want to exclude characters, you can use *negated character sets*. Any characters placed inside `[^squarebrackets]` (with a caret, `^`, at the start) would be excluded. For example, if you wanted to find all characters except vowels you could use:

```js
/[^aeiou]/
```

##### Searching for patterns at the beginning of a string

The caret (`^`) can also be used to search for patterns at the beginning of strings. So for example:

```js
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString); // Returns true
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst); // Returns false
```

##### Searching for patterns at the end of a string

A `$` can be used to search for patterns at the end of a string. So for example:

```js
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding); // Returns true
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding); // Returns false
```

##### Matching characters that do not occur

The `*` character lets you match instances of zero or more occurrences. For example:

```js
let chewieQuote = "Aaaaaaaaaaaaaaaarrrgh!";
let chewieRegex = /Aa*/;
let result = chewieQuote.match(chewieRegex);
console.log(result); // "Aaaaaaaaaaaaaaaa"
```

##### Consecutive characters

To group characters that appear consecutively you can use the `+` character. For example:

```js
let difficultSpelling = "Mississippi";
let myRegex = /s+/ig; // Change this line
let result = difficultSpelling.match(myRegex);
console.log(result); // "ss", "ss", not "s", "s", "s", "s",
```

This can also be used to match across entire words, instead of individual characters. For example:

```js
let quoteSample = "The five boxing wizards jump quickly.";
let regexLetters = /[A-Za-z]/gi;
let result = quoteSample.match(regexLetters); // "T", "h", "e", "f", "i", "v", "e", "b", "o", "x", …

let regexWords = /[A-Za-z]+/gi;
let result = quoteSample.match(regexWords); // "The", "five", "boxing", "wizards", "jump", "quickly"
```

##### Lazy matching

This can be used when you want to find the shortest possible match. So let's say you were to use the regex `/t[a-z]*i/` on the string `"titanic`. By default, this regex would return `"titani"`. But if you wanted the shortest possible match (i.e. `"ti"`) instead, you'd use a `?` to indicate you want to use lazy matching: `/t[a-z]*?i/`.

### Shorthand character classes

Because some regex are used commonly, some nice people came up with *shorthand character classes* to save us all some time. An example of this is the regex `\w`, which is shorthand for all letters and numbers (much easier than writing out `[A-Za-z0-9_]`).

Here are some:

- `\w`: All letters and numbers.
- `\W`: No letters or numbers (but various other cahracters, like `@`, `%`, or `?`).
- `\d`: Digits (this is shorthand for `[0-9]`).
- `\D`: Non-digits (shorthand for `[^0-9]`).
- `\s`: Whitespace, carriage return, tab, and new line characters (this is shorthand for `[ \r\t\f\n\v]`).
- `\S`: Non-whitespace (this is shorthand for `[^ \r\t\f\n\v]`).

### Specifying the number of characters

To control the number of occurrences in regex, you can use *quantity specifiers* (with curly braces `{}`). There are several variations:

- `{3}`: Exactly 3 occurrences.
- `{3,}`: At least 3 occurrences.
- `{3,6}`: Between 3 and 6 occurrences.

For example, for the first 4 or more occurrences of alphabetical characters you would use:

```js
/^[A-Za-z]{4,}/
```

Or to match the strings `"Ohhh no"`, `"Ohhhh no"`, `"Ohhhhh no"`, and `"Ohhhhhh no"` (in other words, with between 3 and 6 `h`s):

```js
let ohStr = "Ohhhh no";
let ohRegex = /Oh{3,6} no/;
let result = ohRegex.test(ohStr); // true
```

### Checking for characters that may not exist

Sometimes you may want to check a string for a character that may or may not exist. In this case, you'd use a `?`. For example:

```js
let american = "color";
let british = "colour";
let englishRegex= /colou?r/;
rainbowRegex.test(american); // Returns true
rainbowRegex.test(british); // Returns true
```

### Lookaheads

*Lookaheads* are patterns that tell JavaScript to look ahead in a string to check for patterns later on, and are often used for checking for multiple patterns in the same string. There are two types of *lookaheads*:

- `(?=...)`: Positive lookahead - Looks to make sure a pattern is there (the `...` is the part that is not matched).
- `(?!...)`: Negative lookahead - Looks to make sure a pattern is **not** there (the `...` is the part that you do not want to be there).

For example:

```js
let quit = "qu";
let quRegex= /q(?=u)/; // First checks for the `q`, then looks ahead and also checks for the presence of the `u`. If `true` it returns the q.
quit.match(quRegex); // Returns ["q"]
```

Here's a more complex example, using two lookaheads to check password criteria:

```js
let sampleWord = "astronaut";
let pwRegex = /(?=\w{5,})(?=\D*\d{2})/;
let result = pwRegex.test(sampleWord); // false, because there aren't two consecutive characters
```

So to break this example down, `pwRegex` checks that `sampleWord` has both of the following conditions:

- `(?=\w{5,})`: At least 5 characters long.
- `(?=\D*\d{2})`: Two consecutive digits (`\D*` zero or more instances of non-digits, and `\d{2}` for two or more digits).

### Mixed character groupings (either/or)

Sometimes we might want to check for more than one group of characters. For example, if we want to check whether a string is either `Franklin Roosevelt` or `Eleanor Roosevelt`, we could use:

```js
let myString = "Eleanor Roosevelt";
let myRegex = /(Eleanor.*|Franklin.*) Roosevelt/;
let result = myRegex.test(myString);
```

**Note:** The `.*` used above picks up the presence of a middle name or initial/s (for example: `Franklin Roosevelt` or `Franklin D. Roosevelt`).

### Capture groups

Instead of manually repeating regex multiple times, you can reuse it with *capture groups*. The regex of any pattern you want repeated goes inside a `()`. Every time you want to repeat that pattern, use a `\1` (and if there is a second `(capture group)` you'd use `\2`, etc.).

For example, to test for any number that is repeated only three times:

```js
let repeatNum = "42 42 42";
let reRegex = /^(\d+)\s\1\s\1$/;
let result = reRegex.test(repeatNum); // true
```

To break `reRegex` down:

- `(\d+)`: This is the capture group (`()`), and it's a number that appears with any number of digits, i.e. consecutively (`\d+`).
- `\s`: Each of these represents whitespace.
- `\1`: Each of these represents another `(\d+)`.
- `^` and `$` specify the start and end.

### Search and replace

If we want to search through and replace some of the characters in a string, we can use `.replace()`.

Here's a simple example, replacing the word `"wrong"` with `"awesome"`:

```js
let wrongText = "This is just wrong!"
let wrongRegex = /wrong/;
console.log(wrongText.replace(wrongRegex, "awesome")); // Logs "This is just awesome!"
```

To use regex with `.replace()` and *capture groups*:

```js
console.log("Okey Dokey".replace(/(\w+)\s(\w+)/, "$2 $1")); // Logs Dokey Okey
```

To break this down, we're searching for characters that match the regex:

- `(\w+)\s(\w+)`: Capture group 1 (a word), whitespace, capture group 2 (a word).
Then the `$` can apparently also be used to specify where you want the capture groups to be placed. In this case, we're swapping the order, so:
- capture group 2, then capture group 1 (`"$2 $1"`).

### Removing whitespace from the start and the end

Sometimes you have whitespace at the start or end of a string, but don't want it. Here's how to get rid of it:

```js
let hello = "  Hello, World!  ";
let wsRegex = /^\s+|\s+$/g;
let result = hello.replace(wsRegex, "");
console.log(result); // "Hello, World!" (without whitespace at the start or end)
```

Breaking down `wsRegex`:

- `^\s+` and `\s+$` finds all of the whitespace at the start and end of the string.
- `|` operator separates them, because we are looking for multiple patterns (both whitespace at beginning or whitespace at the end).
- `g` flag, just because (honest answer, I don't understand this, and freeCodeCamp's explaination is "and I'm going to add a `g` here...").

**Note:** You could also use `.trim()` to achieve this.
