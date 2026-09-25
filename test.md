## AMA Questions

### 1. What are the types of HTTP methods? — (Aditya Sharma)

The most commonly used HTTP methods are:

- **GET** – Retrieve data from a server without modifying it.
- **POST** – Send new data to the server to create a resource.
- **PUT** – Update/replace an existing resource entirely.
- **PATCH** – Partially update an existing resource.
- **DELETE** – Remove a resource from the server.
---

### 2. Why do we use `stopPropagation()`? — (Alok Kumar)

In JavaScript, DOM events bubble up from the target element through its ancestors (or "capture down" during the capturing phase)       
stopPropagation() is used to prevent an event from bubbling up (or capturing down) further to parent/ancestor elements.        
**Use case:** If you have a button inside a div, and both have click listeners, clicking the button would normally trigger both    
handlers. Calling `event.stopPropagation()` inside the button's handler stops the div's handler from firing.

---

### 3. What are some input types in HTML? — (Amit Chandra Dey)

The `<input>` element supports many `type` attributes, including:

- `text` – single-line text
- `password` – masked text
- `email` – validated email format
- `number` – numeric input
- `checkbox` – multiple selectable options
- `radio` – single choice from a group
- `file` – file upload
- `range` – slider input
- `color` – color picker

---

### 4. Why do we use inheritance? — (Aniket Kumar)

Inheritance is an object-oriented programming concept where a class (child/subclass) acquires the properties and methods    
of another class (parent/superclass). We use it to:

- **Reuse code** – avoid rewriting common logic across classes.
- **Establish relationships** – model real-world "is-a" relationships (e.g., a `Dog` is a `Animal`).
- **Enable polymorphism** – child classes can override parent methods for specialized behavior.
- **Improve maintainability** – changes to shared logic only need to happen in one place (the parent class).

---

### 5. What is the difference between the DOM and HTML? — (Atul Kumar)

- **HTML** is the **static markup language** — plain text written in `.html` files that defines the structure and
   content of a webpage using tags.      
- **DOM (Document Object Model)** is the **live, in-memory tree representation** of that HTML, created by
   the browser after it parses the page. It's an object-oriented structure that JavaScript can read and modify dynamically.

**Key difference:** HTML is fixed source code; the DOM is dynamic and can change at runtime (e.g., via JavaScript)      
without altering the original HTML file. Every HTML page produces a DOM,     
but the DOM can end up different from the original HTML due to scripts modifying it.    

---

### 6. What is the `ls` command? — (Bokam Manikanta)

`ls` is a Unix/Linux command used to list the contents (files and directories) of a directory.

---

### 7. What is a higher-order function? — (Indra M)

A higher-order function (HOF) is a function that does at least one of the following:    

1. Takes one or more functions as arguments, or    
2. Returns a function as its result.


Common built-in HOFs: `map()`, `filter()`, `reduce()`, `forEach()`.

---

### 8. How does a browser render an HTML page? — (Krishnav Verma)

At a high level, the rendering process (the "Critical Rendering Path") is:

1. **Parse HTML** → builds the **DOM tree**.
2. **Parse CSS** → builds the **CSSOM tree**.
3. **Combine DOM + CSSOM** → forms the **Render Tree** (only visible elements).
4. **Layout (Reflow)** → calculates exact size/position of each element on the page.
5. **Paint** → fills in pixels (colors, text, images, borders) onto layers.
6. **Composite** → layers are combined and drawn to the screen by the GPU.

JavaScript execution can pause HTML parsing (unless `async`/`defer`),      
and changes to the DOM/CSSOM can trigger reflow and repaint again.    

---

### 9. What is the `sed` command in CLI? — (Pantham Adinarayana)

`sed` (Stream Editor) is a Unix/Linux command-line utility used for **parsing and transforming text**         
in a stream or file, most commonly for find-and-replace operations.

Common example:
```bash
sed 's/old/new/' file.txt        # Replace first "old" with "new" per line
sed 's/old/new/g' file.txt       # Replace all occurrences on each line
```

It's widely used for scripting, log processing, and batch text editing without opening a text editor.

---

### 10. What is encapsulation? — (Rahul Raj)

Encapsulation is an OOP principle of **bundling data (variables) and the methods that operate on that data into    
a single unit (class)**, while **restricting direct access** to some of the object's internal details.      

---

### 11. What are list tags in HTML? — (Sai Ganesh Lanka)

HTML provides three main types of lists:

1. Unordered List (`<ul>`) – bullet-point list, items marked with `<li>`.
   ```html
   <ul><li>Apple</li><li>Banana</li></ul>
   ```
2. Ordered List (`<ol>`) – numbered list.
   ```html
   <ol><li>Step 1</li><li>Step 2</li></ol>
   ```
3. Description List (`<dl>`) – list of terms and their descriptions, using `<dt>` (term) and `<dd>` (description).
   ```html
   <dl><dt>HTML</dt><dd>Markup language</dd></dl>
   ```

---

### 12. What are the types of inheritance? — (Santosh Anil Gurkhe)


1. **Single Inheritance** – one class inherits from one parent class.
2. **Multilevel Inheritance** – a class inherits from a class that itself inherits from another (a chain).
3. **Multiple Inheritance** – a class inherits from more than one parent class (supported directly in languages like C++, and via interfaces in Java).
4. **Hierarchical Inheritance** – multiple classes inherit from a single parent class.
5. **Hybrid Inheritance** – a combination of two or more types of inheritance above.

---

### 13. What is `insertBefore()`? — (Sibsankar Manna)

`insertBefore()` is a DOM method used to **insert a new node into the DOM tree before a specified existing child node**,     
under the same parent.     

**Syntax:**
```js
parentNode.insertBefore(newNode, refOfNodeBeforeWehaveToPlaceNewNode);
```
