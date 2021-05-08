# HTML and CSS

HTML gives structure to a page's content, and CSS controls the layout and appearance.

## Basic HTML

### Defining the doc type and structure

For HTML, add `<!DOCTYPE html>` to the first line of the file. The rest of the page should be between `<html>` tags.
The `<head>` is where you include any metadata or markup, like `link`, `meta`, `title`, and `style`.
The `<body>` is where the actual page content goes.

### Comments

```html
<!-- Comments follow this format -->
```

### Anchors

Used to link to content outside the page. Most common is `<a href="*">`
Within a page, you can also use `id=name-of-anchor` within a header. Can also use `#top` and `#bottom` as anchors.

### Targets

Specify where to open the link. For example, `<a target="_blank" href="example.com">Example.com</a>` would open Example.com in a new tab.

### Lists

Bulleted lists start with `<ul>` (unordered list), followed by a `<li>` (line) for each bullet. Need to close each element too.

Numbered lists start with `<ol>` (ordered list), followed by a `<li>` (line) for each new number. Need to close each element too.

### Creating a form

Can use `<form>` to create.

#### Adding text input fields

Create with `<input type="text">`. It's self-closing. Can add some placeholder text with `<input type="text" placeholder="this is placeholder text">`. These don't have to be used in a `<form>`, per se.

#### Radio buttons

Create with `<input type="radio">`. Each radio button should be nested inside a `<label>` element. Should also have a `name` attribute, so that it knows which radio buttons belong together. Best practice is to also have a `for` attribute in there too, for assistive technologies, whatever they are... So, for example:
`<label for="option a"> <input id="option a" type="radio" name="bunch of options">Indoor </label>`
To make a button checked by default, use `<input type="radio" name="test-name" checked>`

#### Checkboxes

Similar as radio buttons in nearly every way. Create with `<input type="checkbox">`. Each checkbox should be nested inside a `<label>` element. For example:

```html
<label for="loving"
  ><input id="loving" type="checkbox" name="personality" /> Loving</label
>
```

To make a checkbox checked by default, use `<input type="checkbox" name="test-name" checked>`

#### Customizing with attributes

Can have an `action` attributed to it (e.g. `<form action="/url-where-you-want-to-submit-form-data"></form>`). To make an input field **required**, use `required` attribute (e.g. `<input type="text" required>`).

#### Submitting the form

Can add a submit button within the form element with `<button type="submit">this button submits the form</button>` (e.g. `<button type="submit">this button submits the form</button>`).

### DIVs

It's a general purpose container for other elements.

### Images

In the background you'd use a `background` property, with the `url()` function.

## Basic CSS

CSS tells the browser how to display the text written in the HTML. It's case-sensitive.
The CSS can be added:

- directly to HTML elements with `style` attribute.
- within `<style>` tags in the document
- in a separate CSS file, referenced in the HTML file
  Should end `style` declarations with a `;`.

Easy way to do this is to put a `style` block at the top of the code, if you want all elements of the same type to look the same. Need to have curly brackets around each element's rules, and add a `;` to each of them. For example:

```html
<style>
  h2 {
    color: red;
  }
</style>
```

### Color

```html
<h2 style="color: blue;">CatPhotoApp</h2>
```

Can also use hexadecimals or RGB values for more fine-tuned color, for example: `#000000` is the hexadecimal for `black`; `rgb(255, 255, 255)` is RGB for `white`.
Can add color to a background with `background-color`, then your choice of color picker. Recommended to use `rgba()` though, as the `a` is used to adjust the opacity.
Can also adjust the opacity with `opacity` property. For the opacity, `1` is opaque and `0` is transparent.
Can also use HSL values (hue, saturation, lightness), with `hsl()`. Example: `hsl(0, 100%, 50%)` is red. Using HSL values makes it easier to change shades.
Gradients are also possible, with the `background` element's `linear-gradient()` function. Need to specify where the gradient will start, in terms of degrees, and the color you want to start and end with. Example: `background: linear-gradient(35deg, #CCFFFF, #FFCCCC);`. Instead of hex values, can also use color names, `rgb()` values, or `hsl()` values.
If feeling like a 90s flashback, can also use `repeating-linear-gradient()`. I won't bother documenting it here as it is ugly AF.

### Fonts

```html
<h2 style="font-family: sans-serif;">CatPhotoApp</h2>
```

Can make it **bold** with`<strong>`in-line, or to an element with`font-weight: bold;`. For more control, can also use`font-weight`(specifying a value for how thick you want it, like`100`). Can underline it with `<u>`, or to an element with`text-decoration: underline;`. Can make it italic with `<em>` tag, or to an element with`font-style: italic;`. Can make a strike-through with `<s>`, or to an element with`font-style: strike-through;`. Choose the size with`font-size`, and then choose a size in`px`. To give the font a nice 90s look, can add a drop shadow with`box-shadow`, specifying:

- `offset-x`, how far to push the shadow horizontally from the element.
- `offset-y`, how far to push the shadow vertically from the element.
- `blur-radius`, `spread-radius` and a color value, in that order.

  **Note:** The blur-radius and spread-radius values are optional.

### Text alignment

Use text-align, then:

- `text-align: justify;`
- `text-align: center;`
- `text-align: right;`
- `text-align: left;` (this is also the default)
  Can choose the line spacing with `line-height`.
  Can also add a line break with `<hr>` (horizontal rule).

### Text transform

Changes the appearance of text:

- `uppercase`: "TRANSFORM ME".
- `capitalize`: "Transform Me".
- `initial`: Use the default value.
- `inherit`: Use the text-transform value from the parent element.
- `none`: Use the original text.

### Transforming elements

Use the `transform` element with a `scale()` function, and in the brackets include an integer that corresponds to how much you want to scale the element. `2` would mean making it twice as big. Example, to double the size of paragraph text you'd use `p { transform:scale(2); }`

Can make this occur when the use hovers over it, with `:hover` pseudo-class:
`p:hover { transform: scale(2.1); }`

#### Skewing elements

Along the x-axis with `skewX()`, and specifying the degrees in the brackets:
`p { transform: skewX(-32deg); }`

Along the y-axis with, you guessed it, `skewY()`.

### Width

Specifies the `width` of an element in pixels (`px`). Ditto for the `height`.

### Borders

```html
<style>
  .thin-red-border {
    border-color: red;
    border-width: 5px;
    border-style: solid;
  }
</style>
```

### Animating properties

Set the name of the animation with `animation-name`. Set the length of time with `animation-duration`. Then, `@keyframes` is what is used to specify what happens during the animation using percentages (`0%` is the very start, and `100%` is the end). Example:

```css
#anim {
  animation-name: colorful;
  animation-duration: 3s;
}
@keyframes colorful {
  0% {
    background-color: blue;
  }
  100% {
    background-color: yellow;
  }
}
```

Can also add other values in-between, such as `50%`, too.

Can also use animations to do gnarly stuff with the buttons:

```css
button:hover {
  animation-name: background-color;
  animation-duration: 500ms;
  animation-fill-mode: forwards;
}
@keyframes background-color {
  100% {
    background-color: #4791d0;
  }
}
```

**Note:** The `animation-fill-mode: forwards;` stops the animation reverting back to its original state after 500ms.

#### Animating movement

When elements have a `position` you can create movement with `right`, `left`, `top`, `bottom`. Example, which would move the element down 50px, then up to it's starting point... as well as changing color:

```css
@keyframes rainbow {
  0% {
    background-color: blue;
    top: 0px;
  }
  50% {
    background-color: green;
    top: 50px;
  }
  100% {
    background-color: yellow;
    top: 0px;
  }
}
```

#### Animating opacity

You can probably guess how you use `opacity`... ?

#### Setting the number of animation loops

Use, for example, `animation-iteration-count: 3;` to loop through an animation three times before stopping. Can use `infinite` to keep it going forever.

#### Accelerating animation

Can use `animation-timing-function` to make an animation accelerate with `ease-in` or decelerate with `ease-out`. To make it stay the same speed, use `linear`.
Can also control this in a fine-tuned way using the `cubic-bezier` function. This creates four points which you can define the speed at each point. So, for example:
`animation-timing-function: cubic-bezier(0.1, 0.25, 0.75, 1);`
Would continue to accelerate through the animation.

### IDs

Often used for JavaScript stuff, but can be used to identify any specific part of the HTML page. In a `style` element, it starts with a `#` instead of a `.`. Should be unique. Example:

```html
<h2 id="cat-photo-app"></h2>
```

#### Importing custom fonts

For example, add the following from Google Fonts, to the top of the code:

```html
<link
  href="https://fonts.googleapis.com/css?family=Lobster"
  rel="stylesheet"
  type="text/css"
/>
```

Then use it on the page by using `font-family: Lobster`.

#### Degrading fonts

This is when you specify more than one font, so that it will 'degrade' to the backup if the first isn't available. For example:

```css
p {
  font-family: Helvetica, sans-serif;
}
```

### Padding and margin

Can specify for an element: `margin: -25px`
Per side: `margin-bottom: -25px`
All sides in the same instructions: `margin: 20px 40px 20px 40px` (like a clock: top, right, bottom, left).
For padding, obviously you'd use `padding`.

### Relative, absolute, and fixed positions / offsets

Can move a particular element relative to where it should sit with `position: relative;`, followed by what you want to move it by: `top`, `bottom`, `left`, `right`, then the number of pixels:

```html
<style> h2 {
  position: relative;
  top: 20px;
}
```

This would move each h2 20px lower from where it would usually be.
Absolute is locked relative to parent container. Use `position: absolute`, and the top, right, bottom, left values.

Fixed position is basically the same as absolute, but it won't move when the user scrolls. Use `position: fixed;`, then specify the top, right, bottom, left values.

### Float values

These are removed from the normal flow of a document and pushed to either the `left` or `right` of their containing parent element. Can be used with the `width` property to specify how much horizontal space the floated element requires. Example:

```css
#right {
  float: right;
  width: 40%;
}
```

If they overlap, you can use `z-index` to choose which goes on top. Assign each element a`z-index` with an integer (`z-index: 1;`), and the highest integer will appear on top.

To center an element horizontally, use `margin: auto;`.

### Using classes

Classes are reusable styles. Class names start with a `.`, for example:

```html
<style>
  .blue-text {
    color: blue;
  }
</style>
```

When using classes, you don't need to add a `;` to the end of each style element.
To apply this to an element, you would use:

```html
<h2 class="blue-text">Example header</h2>
```

Can also use multiple classes for one element with:
`<img class="class1 class2">` (and if there are more than one that defines the same element, the last one will override the previous). Similarly, inline `style` declarations > `id` declarations > `class` declarations. The nuclear option is to use `!important` after a declaration, for example `color: red !important;`.

### Attributes

This is when you use `[att=value]` to style all attributes on the page.
For example, for radio boxes:

```css
[type="radio"] {
  margin: 20px 0px 20px 0px;
}
```

### Using absolute or relative values

Instead of `px` you can use `in` and `mm` (but this can go wrong if an unusual resolution is used). Can also use `em` and `rem`, which are relative to the size of the font.

### Variables

Use the syntax `--variable-name:`, followed by the `value;`. For example, `--penguin-skin: gray;`. You would then assign it to something with `background: var(--penguin-skin);`.
If you wanted to assign a backup for the variable (an older browser doesn't support it, for example), you would use the syntax `background: var(--penguin-skin, black);`.
Variables are available to use within the element that you create it. It also cascades to any variables within that one, hence **Cascading** Style Sheets. To apply a style to an entire HTML page, apply it to `:root`, for example `<style> :root { --penguin-belly: pink; }`
Root values can be overwritten if you set a different one in a specific element.

### Psuedo-classes

Added to give a class when an element is in a specific state. For example, to make anchor/link text red when you hover over it you'd use:

```css
a:hover {
  color: red;
}
```

### Pseudo-elements

Not sure about these either, but `::before` and `::after` pseudo-elements are used to add somethng before and after a specific element. For these to work, they must have a `content` property:

```css
.heart::before {
  content: "";
  background-color: yellow;
  border-radius: 25%;
  position: absolute;
  height: 50px;
  width: 70px;
  top: -50px;
  left: 5px;
}
```

## Accessibility

It's a good idea to keep the following in mind when building a website:

1. have well-organized code that uses appropriate markup.
2. ensure text alternatives exist for non-text and visual content.
3. create an easily-navigated page that's keyboard-friendly.

### Alt tags

The `alt` tags are added to images to render text in their place. Example: `<img src="importantLogo.jpeg" alt="Company logo">`. Good alt text is short but descriptive, and meant to briefly convey the meaning of the image. Also good for SEO.

If there's no need for an `alt` tag, you can leave it empty:

```html
<img src="visualDecoration.jpeg" alt="" />
```

### Element tags

HTML5 introduced a number of new elements that give developers more options while also incorporating accessibility features. These are:

- `main` - Wraps main content; only one per page. Shouldn't be used around the navigation, or anything other than the main text/content on the page.
- `header` - Different than the `<head>`. Often the `<h1>` of the page.
- `footer` - Indicates the content at the bottom of the page.
- `nav` - Used to indicate the main navigation on your page.
- `article` - Used around self-contained content (The tag works well with blog entries, forum posts, or news articles). Basically, think "if I removed all surrounding context, would the content still make sense?"
- `section` - Section on a page.

Can think of it hierarchically as:

`<div>` - groups content
`<section>` - groups related content
`<article>` - groups independent, self-contained content

#### Audio

Use `<audio>` to add an audio player to the page. The browser automatically renders the play/pause/seek controls when you add a `controls` attribute. Also specify the `type`.For example:

```html
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

#### Figures

If you use a `figure` in your page, also include a `figcaption`, which should be a text alternative explaining what it is. Basically, a brief summary:

```html
<figure>
  <img
    src="roundhouseDestruction.jpeg"
    alt="Photo of Camper Cat executing a roundhouse kick"
  />
  <br />
  <figcaption>
    Master Camper Cat demonstrates proper form of a roundhouse kick.
  </figcaption>
</figure>
```

#### Labels

When building a form, make the `labels` more accessible with `for` attribute:

```html
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" />
</form>
```

**Note:** This should usually match the `id` tag.

For radio buttons, where there are a set of choices, can additionally use a `fieldset` (indicates where the section is) and a `legend` (indicates where the question/statement is):

```html
<form>
  <fieldset>
    <legend>Choose one of these three items:</legend>
    <input id="one" type="radio" name="items" value="one" />
    <label for="one">Choice One</label><br />
    <input id="two" type="radio" name="items" value="two" />
    <label for="two">Choice Two</label><br />
    <input id="three" type="radio" name="items" value="three" />
    <label for="three">Choice Three</label>
  </fieldset>
</form>
```

#### The date

For newer browsers, you can add a `date` field to add a date picker. For older browsers, this will default to a text input field. So makes sense to show what format you want for the text input:

```html
<label for="input1">Enter a date:</label>
<input type="date" id="input1" name="input1" />
```

#### The time

A standardized accessible format will be used when `time` and `datetime` are added to a page:

```html
The best day to host the vaunted Mortal Kombat tournament is
<time datetime="2016-09-15">Thursday, September 15<sup>th</sup></time
>.
```

### Using CSS to make pages more accessible

Basically, when you want to hide accessible (screen reader) content from the 'default' user, use `sr-only` class:

```css
.sr-only {
  position: absolute;
  left: -10000px;
  width: 1px;
  height: 1px;
  top: auto;
  overflow: hidden;
}
```

**Note:** The `left` position fires this **way** off to the side, out of view of the average user.

### Contrast

Text to background contrast ratio (relative luminance) should be 4.5:1. This also applies to the grey scale versions of colors, so that colour-blind people (particularly with shades of green) can see them too. Easier to do these if using `hsl()` color values. If in doubt, use an online tool to check these.

### Using accesskeys to make links more accessible

Better for keyboard only users. Example:

```html
<button accesskey="b">Important Button</button>
```

The, when people hit the b key on their keyboard they get directed to this button.

There's also the `tabindex`, which you assign to page elements, allowing the user to tab through them in a specific order (and then moves on to the other, non-assigned elements - or `tabindex` elements with the integer `0`). Each is assigned an integer, indicating the order 'within' the index:

```html
<div tabindex="1">I get keyboard focus, and I get it first!</div>
<div tabindex="2">I get keyboard focus, and I get it second!</div>
```

## Responsive web design

Basically, adapting your site for devices of different sizes, power, and mobile.

### Media queries

Displays specific content when a devices screen size is less or more than a certain size.
Less (or equal to) a width of `100px`: `@media (max-width: 100px) { /* CSS Rules */ }`.
More (or equal to) a height of `350px`: `@media (min-height: 350px) { /* CSS Rules */ }`.
So if you want to use a `font-size` of `20px`, except for devices less than `800px` high, you'd use:

```html
<style>
  p {
    font-size: 20px;
  }

  /_ Add media query below _/ @media (max-height: 800px) {
    p {
      font-size: 10px;
    }
  }
</style>
```

### Responsive images

Can scale images to fit a certain percentage of the screen (although the image won't go wider than its original width). By specifying the `display` the image will appear as it's own line, and the `height` keeps the size ratio from going weird:

```css
img {
  max-width: 100%;
  display: block;
  height: auto;
}
```

#### Optimizing for high res (i.e. retina)

Basically set the image to half it's original res so it doesn't look blurry:

```html
<style>
  img {
    height: 250px;
    width: 250px;
  }
</style>
<img src="coolPic500x500" alt="A most excellent picture" />
```

### Responsive typography

Can use viewport units to scale text size.

- vw: 10vw would be 10% of the viewport's width.
- vh: 3vh would be 3% of the viewport's height.
- vmin: 70vmin would be 70% of the viewport's smaller dimension (height vs. width).
- vmax: 100vmax would be 100% of the viewport's bigger dimension (height vs. width).
  So `width: 80vw;` would be 80% the width of the viewport.

### Flex boxes

Make content behave in predictable way across different browsers, screens, etc. Done by placing the CSS property `display: flex;` on an element.
Adding `display: flex` to an element turns it into a flex container. This makes it possible to align children of that element into rows or columns. You do this by adding the `flex-direction` property to the parent item and setting it to `row` (this is the default) or `column`.
Other options for `flex-direction` are `row-reverse` and `column-reverse`.

#### Justifying flex boxes

Several options for how to space the flex items along the main axis. Most common is `justify-content: center;`. Others are:

- `flex-start`: aligns items to the start of the flex container.
- `flex-end`: aligns items to the end of the flex container.
- `space-between`: aligns items to the center of the main axis, with extra space placed between the items.
- `space-around`: similar to `space-between` but the first and last items are not locked to the edges of the container, the space is distributed around all the items.

#### Aligning items

This is similar to `justify-content`, but for the opposite axis.
`align-items` include:

- `flex-start`: aligns items to the start of the flex container.
- `flex-end`: aligns items to the end of the flex container.
- `center`: align items to the center.
- `stretch`: stretch the items to fill the flex container. For example, rows items are stretched to fill the flex container top-to-bottom.
- `baseline`: align items to their baselines. Baseline is a text concept, think of it as the line that the letters sit on.

#### align-self

Can use `align-self` to adjust each item's alignment individually, instead of setting them all at once. Useful since other common adjustment techniques using the CSS properties `float`, `clear`, and `vertical-align` do not work on `flex` items:

```html
#box-1 { background-color: dodgerblue; align-self: center; height: 200px; width:
200px; } #box-2 { background-color: orangered; align-self: flex-end; height:
200px; width: 200px; }
```

#### Flex wrapping

However, using the flex-wrap property, it tells CSS to wrap items. This means extra items move into a new row or column. The break point of where the wrapping happens depends on the size of the items and the size of the container (in terms of %s, for example).
CSS also has options for the direction of the wrap:

- `nowrap`: this is the default setting, and does not wrap items.
- `wrap`: wraps items from left-to-right if they are in a row, or top-to-bottom if they are in a column.
- `wrap-reverse`: wraps items from bottom-to-top if they are in a row, or left-to-right if they are in a column.

#### Flex shrinking

The `flex-shrink` property allows an item to shrink if the flex container is too small. Items shrink when the width of the parent container is smaller than the combined widths of all the flex items within it. Then allocate an integer to each, to determine size. So in this case, `box-2` would be twice the size of `box-1`:

```css
#box-1 {
  background-color: dodgerblue;
  width: 100%;
  height: 200px;
  flex-shrink: 1;
}

#box-2 {
  background-color: orangered;
  width: 100%;
  height: 200px;
  flex-shrink: 2;
}
```

#### Flex grow

The opposite of `flex-shrink` is the `flex-grow` property, except the `flex-grow` property controls the size of items when the parent container expands.

#### Flex basis

Specifies the initial size of the item before CSS makes adjustments with `flex-shrink` or `flex-grow`.
The units used by the `flex-basis` property are the same as other size properties (`px`, `em`, `%`, etc.). The value `auto` will size items based on the content.

#### Flex shortcut

There is a shortcut available to set several `flex` properties at once. The `flex-grow`, `flex-shrink`, and `flex-basis` properties can all be set together by using the `flex` property.
For example, `flex: 1 0 10px;` will set the item to `flex-grow: 1;`, `flex-shrink: 0;`, and `flex-basis: 10px;`.
The default property settings are `flex: 0 1 auto;`.

#### Flex ordering

The `order` property is used to tell CSS the order of how `flex` items appear in the `flex` container. By default, items will appear in the same order they come in the source HTML. The property takes numbers as values, and negative numbers can be used. So an element with `order: 2;` will come before `order: 1;`.

#### Tying flex together

The following will cause `#box-1` to grow to fill the extra space at twice the rate of `#box-2` when the container is greater than `300px` and shrink at twice the rate of `#box-2` when the container is less than `300px`. `300px` is the combined size of the flex-basis values of the two boxes:

```html
<style>
  #box-container {
    display: flex;
    height: 500px;
  }
  #box-1 {
    background-color: dodgerblue;
    flex: 2 2 150px;
    height: 200px;
  }

  #box-2 {
    background-color: orangered;
    flex: 1 1 150px;
    height: 200px;
  }
</style>
```

## CSS grids

Used to organize an HTML page. Set any HTML element to a grid container by setting the `display` property to `grid`.

Need to define a structure before you can do anything with it.

### Columns

To use columns, add `grid-template-columns`. So on a style element called `container`, this would be:
`.container { display: grid; grid-template-columns: 50px 50px; }`

Which would achieve a two column grid, with each column being 50px wide.
Can also define sizes with `px` and `em`. Can also use:

- `fr`: sets to a fraction of the available space,
- `auto`: sets to the width or height of its content automatically,
- `%`: adjusts to the percent width of its container.
  Example: `grid-template-columns: auto 50px 10% 2fr 1fr;`, which equates to five columns. The first column is as wide as its content, the second column is 50px, the third column is 10% of its container, and for the last two columns; the remaining space is divided into three sections, two are allocated for the fourth column, and one for the fifth.

#### Adding gaps

To add a gap between the columns, use the grid-column-gap property like this: `grid-column-gap: 10px;`. This would give a gap of 10px between each column in the grid.
There's also `grid-gap`, which can be used to give the rows and columns the same gap. Or as shorthand, where if you put two values it takes the first to mean the row gap and the second to be the column gap.

### Rows

Similar to columns, but with `grid-template-rows` instead. To add a gap you'd use `grid-row-gap`.

### Grid-columns and -rows

Similar to above, but you control where the column starts and finishes. So `grid-column: 1 / 3;` would mean an item starts at column 1 and finishes at column 3.
Same deal with rows using `grid-row`.
Note: position 1 is the margin (either left or top). I'm tired... just Google `grid-column`s, etc...

### Aligning columns and rows around content

For horizontal alignment, use `justify-self` property to set this. Default value is `stretch`, which makes the content fit the cell. Can also use `start`, `center`, and `end`.
To apply this to everything in the grid, use `justify-items`, followed by one of the above values. For example: `justify-items: center;`.

Ditto applies to vertical alignment, which is instead `align-self`, and `align-items`.

### Creating grids on the fly

If you want a grid-area, but don't have a grid already assigned, you can create one on the fly with something like `item1 { grid-area: 1/1/2/4; }`, where it translates to `grid-area: horizontal line to start at / vertical line to start at / horizontal line to end at / vertical line to end at;`... so the item in the example will consume the rows between lines 1 and 2, and the columns between lines 1 and 4.

### Repeating columns and rows

Instead of typing the same stuff again and again, can use the `repeat` function. So for example:
`grid-template-rows: repeat(100, 50px);` would give you 100 rows of `50px` in height. Can also repeat them with `grid-template-columns: repeat(2, 1fr 50px) 20px;`, which will give you `grid-template-columns: 1fr 50px 1fr 50px 20px;` (the same as 1fr 50px repeated, twice followed by 20px).

#### Limiting the size of columns and rows when they resize

Use `minmax` function. Example: `grid-template-columns: 100px minmax(50px, 200px);` would generate two columns, one of 100px, and another that is no smaller than 50px and bigger than 200px.

#### Using auto-fill and auto-fit

Fills as many rows or columns as possible until it's full. Can be used in combination with `minmax`. For example: when `grid-template-columns` is set to `repeat(auto-fill, minmax(60px, 1fr));` it will keep adding columns until it can't add any more (based on the size of the screen when it's resized).
`auto-fit` is similar, but will basically fit the contents across the page (so they perfectly fit).

### Grids within grids (with grids...)

This is also an option. Basically create `grid-template-columns` with `grid-template-columns`.
