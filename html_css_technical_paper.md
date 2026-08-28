# Technical Paper on HTML/CSS


## Introduction

HTML and CSS are the two fundamental technologies used to build and style web pages.
HTML (HyperText Markup Language) defines the structure and semantic meaning of content.
CSS (Cascading Style Sheets) controls the presentation and layout of that content.



## 1. CSS Box Model

The CSS Box Model describes how the browser represents every HTML element as a rectangular box.

The box consists of four main areas:

<img src="https://miro.medium.com/v2/resize:fit:804/format:webp/1*ydgkPlP_bYrNp9FxxjYHFw.gif"
    alt="CSS Box Model" width="500">

The four parts are:

1. Content   (The content is the actual information inside the element like image, video, text etc).
2. Padding   (Padding creates space between the content and border).
3. Border    (The border surrounds the padding and content).
4. Margin    (Margin creates space outside the border).

Using these we can change BOX model of an element.

---


### box-sizing

Box-sizing is used to declare size of box-model of an element.

The default value is:

```css
box-sizing: content-box;
```

With `content-box`, the declared width represents only the content area.

For example:

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
}
```

The total width becomes:

300 + 20 + 20 + 5 + 5
= 350px

A common CSS reset is:

```css
* {
    box-sizing: border-box;
}
```

With `border-box`, the declared width includes the content, padding, and border.

Therefore:

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

The total width remains `300px`. It fits border, content and padding in 300px .

---

## 2. Inline vs Block Elements

HTML elements can participate in layout as block-level or inline-level elements.

### 2.1 Block Elements

Block elements generally:
* Start on a new line.
* Take whole horizontal space by default.
* Allow width and height to be controlled.
  
  Examples: div, p, h1, etc.

---

### 2.2 Inline Elements

Inline elements generally:

* Remain on the current line.
* Take only the width required by their content.
* Are commonly used within text.     

  Examples: span, a, strong, label etc.
---

### 2.3 `inline-block`

`inline-block` combines characteristics of inline and block layout to an element.

```css
.header_div {
    display: inline-block;
    width: 100px;
    padding: 10px;
}
```

The element can appear alongside other inline content while accepting dimensions.

---

### 2.4 CSS Display Property

The `display` property controls how an element participates in layout.

Common values include:

```css
display: block;  
display: inline;
display: inline-block;
display: flex;
display: grid;
display: none;
```
---

## 3. CSS Positioning

The `position` property controls how an element is positioned.

Common values are:

```css
static
relative
absolute
fixed
sticky
```

---

### 3.1 Static

Static positioning is the default.
```css
.box {
    position: static;
}
```
The element follows normal document flow.

---

### 3.2 Relative

```css
.box {
    position: relative;
    top: 20px;
    left: 10px;
}
```
The element remains in normal document flow but is visually offset from its original position.

`relative` is also commonly used to establish a containing block for absolute positioned descendants.

Example:

```css
.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 0;
    right: 0;
}
```

---

### 3.3 Absolute

```css
.child {
    position: absolute;
    top: 10px;
    right: 20px;
}
```

An absolutely positioned element is removed from normal document flow and positioned relative to an appropriate containing block.
It is positioned according to a parent or grand-parent who have position: relative.

Example:

```css
.card {
    position: relative;
}

.badge {
    position: absolute;
    top: 10px;
    right: 10px;
}
```

---

### 3.4 Fixed

```css
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}
```

A fixed-positioned element is positioned relative to the viewport and generally remains in place even after scrolling    
down.

---

### 3.5 Sticky

```css
.header {
    position: sticky;
    top: 0;
}
```

A sticky element behaves like a normally positioned element until it reaches the specified threshold   
It can stick to bottom or top and will not go out of screen-window.

---

## 4. Common CSS Structural Classes

CSS classes are often used to represent the structure of a page.

Common examples:

```text
.container
.wrapper
.header
.nav
.main
.content
```

Example:

```html
<div class="container">

    <header class="header">
        ...
    </header>

    <main class="main">
        ...
    </main>

    <footer class="footer">
        ...
    </footer>

</div>
```

Example CSS:

```css
.container {
    width: min(100% - 2rem, 1200px);
    margin-inline: auto;
}

.main {
    display: grid;
    grid-template-columns: 1fr 300px;
    gap: 2rem;
}
```

Structural classes should describe the role of a component rather than its visual appearance.

---

## 5. Common CSS Styling Classes

Reusable styling or utility-like classes can be created for common styles.

Examples:

```text
.text-center
.text-left
.text-right
.text-bold
.hidden
```

Example:

```css
.text-center {
    text-align: center;
}

.text-bold {
    font-weight: bold;
}

.rounded {
    border-radius: 8px;
}

.full-width {
    width: 100%;
}
```

The exact naming convention depends on the project's CSS architecture.

---


## 6. CSS Specificity

Specificity determines which CSS declaration wins when multiple declarations apply to the same element.

A simplified priority order is:

```text

!important declaration > Inline style > ID selector > Class / Attribute / Pseudo-class > Element / Pseudo-element >Inherited styles

```

Example:

```css
p {
    color: blue;
}

.text {
    color: green;
}

#message {
    color: red;
}
```

HTML:

```html
<p id="message" class="text">
    Hello
</p>
```

The ID selector has higher specificity than the class and element selectors, so the text becomes red.

---

# 20. Responsive Web Design

Responsive Web Design means designing websites that adapt to different screen sizes and devices.

A responsive website should work well on:

```text
Mobile
Tablet
Laptop
Desktop
Large screens
```

Responsive design commonly uses:

* Flexible layouts
* Relative units
* Flexbox
* CSS Grid
* Media queries
* Responsive images
* Flexible typography

For example:

```css
.container {
    width: min(100% - 2rem, 1200px);
    margin-inline: auto;
}
```

This allows the container to shrink on smaller screens while remaining constrained on larger screens.

---

# 21. CSS Media Queries

Media queries allow CSS to apply conditionally based on the environment, such as viewport width or orientation.

Syntax:

```css
@media (condition) {
    /* CSS rules */
}
```

Example:

```css
.container {
    width: 100%;
}

@media (min-width: 768px) {
    .container {
        width: 750px;
    }
}
```

---

## 21.1 `max-width`

```css
@media (max-width: 600px) {
    .sidebar {
        display: none;
    }
}
```

---

## 21.2 `min-width`

```css
@media (min-width: 768px) {
    .container {
        max-width: 1200px;
    }
}
```

---

## 21.3 Orientation

```css
@media (orientation: landscape) {
    body {
        background: lightgray;
    }
}
```

---

## 21.4 Multiple Conditions

```css
@media (min-width: 768px) and (max-width: 1200px) {
    .container {
        padding: 20px;
    }
}
```

Modern media query syntax also supports range expressions:

```css
@media (width >= 768px) {
    .container {
        padding: 2rem;
    }
}
```
---


# 17. Flexbox

Flexbox is a one-dimensional CSS layout system.

It is useful for arranging elements along a row or column.

Basic example:

```css
.container {
    display: flex;
}
```

HTML:

```html
<div class="container">
    <div>One</div>
    <div>Two</div>
    <div>Three</div>
</div>
```

---

## 17.1 `flex-direction`

```css
.container {
    display: flex;
    flex-direction: row;
}
```

Possible values:

```text
row
row-reverse
column
column-reverse
```

---

## 17.2 `justify-content`

Controls distribution along the main axis.

```css
.container {
    display: flex;
    justify-content: center;
}
```

Common values:

```text
flex-start
center
flex-end
space-between
space-around
space-evenly
```

---

## 17.3 `align-items`

Controls alignment along the cross axis.

```css
.container {
    display: flex;
    align-items: center;
}
```

---

## 17.4 `gap`

Adds spacing between flex items.

```css
.container {
    display: flex;
    gap: 20px;
}
```

---

## 17.5 `flex-wrap`

Allows items to move onto multiple lines.

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

---

## 17.6 `flex`

The `flex` shorthand can represent:

```text
flex-grow
flex-shrink
flex-basis
```

Example:

```css
.item {
    flex: 1;
}
```

---

## 17.7 Common Flexbox Example

```css
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
}
```

This is particularly useful for navigation bars and headers.

---

# 18. CSS Grid

CSS Grid is primarily a two-dimensional layout system.

It allows developers to control rows and columns.

Basic example:

```css
.container {
    display: grid;
}
```

---

## 18.1 Grid Columns

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```

This creates three equal columns.

---

## 18.2 Grid Rows

```css
.container {
    display: grid;
    grid-template-rows: 100px 200px;
}
```

---

## 18.3 `gap`

```css
.container {
    display: grid;
    gap: 20px;
}
```

---

## 18.4 `repeat()`

Instead of:

```css
grid-template-columns: 1fr 1fr 1fr;
```

we can use:

```css
grid-template-columns: repeat(3, 1fr);
```

---

## 18.5 `minmax()`

```css
grid-template-columns:
    repeat(auto-fit, minmax(200px, 1fr));
```

This can create responsive card layouts.

---

## 18.6 Grid Example

```css
.cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

HTML:

```html
<div class="cards">

    <div class="card">Card 1</div>
    <div class="card">Card 2</div>
    <div class="card">Card 3</div>

</div>
```

---

# 23. Common HTML Meta Tags

Meta tags provide information about an HTML document.

They are placed inside:

```html
<head>
```

---

## 23.1 Character Encoding

```html
<meta charset="UTF-8">
```

Specifies the character encoding of the document.

---

## 23.2 Viewport

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
>
```

This is important for responsive webpages.

---

## 23.3 Description

```html
<meta
    name="description"
    content="Learn HTML and CSS fundamentals."
>
```

Provides a description of the page.

---

## 23.4 Robots

```html
<meta name="robots" content="index, follow">
```

Provides instructions to search-engine crawlers.

---

## 23.5 Theme Color

```html
<meta name="theme-color" content="#ffffff">
```

Can influence browser UI theming on supported platforms.
---

# 24. CSS Variables

CSS custom properties allow reusable values to be defined.

Example:

```css
:root {
    --primary-color: #2563eb;
    --text-color: #222;
    --spacing: 16px;
}
```

Use them with:

```css
.button {
    background-color: var(--primary-color);
    color: white;
    padding: var(--spacing);
}
```

---

## Fallback Values

```css
color: var(--text-color, black);
```

If `--text-color` does not exist, `black` is used.

---

# 25. Pseudo-classes

Pseudo-classes select elements based on their state or position.

Common pseudo-classes:

```text
:hover
:focus
:active
:visited
:first-child
:last-child
:nth-child()
:checked
:disabled
```

Example:

```css
button:hover {
    background-color: darkblue;
}
```

Focus:

```css
input:focus {
    outline: 2px solid blue;
}
```

Nth child:

```css
li:nth-child(2) {
    color: red;
}
```

---

# 26. Pseudo-elements

Pseudo-elements style a specific part of an element or create generated content.

Common pseudo-elements:

```text
::before
::after
::first-letter
::first-line
::selection
```

Example:

```css
.title::before {
    content: "★ ";
}
```

Another example:

```css
p::first-letter {
    font-size: 2rem;
}
```

---

# 27. Transitions

CSS transitions create smooth changes between states.

Example:

```css
.button {
    background-color: blue;
    transition: background-color 0.3s ease;
}

.button:hover {
    background-color: darkblue;
}
```

Common transition properties:

```text
transition-property
transition-duration
transition-timing-function
transition-delay
```

Shorthand:

```css
transition: all 0.3s ease;
```

It is generally better to transition only the properties that need animation rather than using `all` indiscriminately.

---

# 28. Transforms

Transforms visually modify an element.

## Translate

```css
.box {
    transform: translateX(20px);
}
```

## Scale

```css
.box {
    transform: scale(1.2);
}
```

## Rotate

```css
.box {
    transform: rotate(45deg);
}
```

Multiple transformations can be combined:

```css
.box {
    transform: translateX(20px) rotate(10deg);
}
```

---


# 36. References

## HTML

1. MDN Web Docs — HTML
   https://developer.mozilla.org/en-US/docs/Web/HTML

2. WHATWG — HTML Living Standard
   https://html.spec.whatwg.org/

3. web.dev — Learn HTML
   https://web.dev/learn/html/

## CSS

4. MDN Web Docs — CSS
   https://developer.mozilla.org/en-US/docs/Web/CSS

5. MDN — CSS Box Model
   https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model

6. MDN — CSS Selectors
   https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Selectors

7. MDN — CSS Specificity
   https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Specificity

## Layout

8. web.dev — CSS Layout
   https://web.dev/learn/css/layout

9. web.dev — Flexbox
   https://web.dev/learn/css/flexbox

10. web.dev — CSS Grid
    https://web.dev/learn/css/grid

11. MDN — CSS Positioning
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Positioning

## Responsive Design

12. MDN — Responsive Web Design
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design

13. MDN — CSS Media Queries
    https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries

14. MDN — Media Queries
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Media_queries

15. web.dev — Learn Responsive Design
    https://web.dev/learn/design

## Accessibility

16. MDN — Accessibility
    https://developer.mozilla.org/en-US/docs/Web/Accessibility

17. W3C Web Accessibility Initiative
    https://www.w3.org/WAI/

18. WAI-ARIA Authoring Practices Guide
    https://www.w3.org/WAI/ARIA/apg/

## Web Standards

19. W3C — CSS
    https://www.w3.org/Style/CSS/

20. WHATWG — HTML Standard
    https://html.spec.whatwg.org/

21. MDN Web Docs
    https://developer.mozilla.org/
