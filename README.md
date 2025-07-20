# CHROME EXTENSION - LEAD TRACKER

Sales People spend countless hours tracking down leads or sourcing leads, that is, looking for people online who might be interested in our product.

## Add button and input tag

```html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <!-- Create an input element with type="text" and id="input-el" -->
        <!-- Create a SAVE INPUT button with id="input-btn" -->
        <input type="text" id="input-el">
        <button id="input-btn">SAVE INPUT</button>
        <script src="index.js"></script>
    </body>
</html>
```

## Style the button and input tag

![](C:\Users\DEll\AppData\Roaming\marktext\images\2025-07-16-00-37-27-image.png)

```css
body {
    margin: 0;
    padding: 10px;
    font-family: Arial, Helvetica, sans-serif;
}

/*

Style our app according to the provided design!

green color -> #5f9341

*/


input {
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
    border: 1px solid #5f9341;
    margin-bottom: 4px;
}

button {
    background: #5f9341;
    color: white;
    padding: 10px 20px;
    border: none;
    font-weight: bold;
}
```

--------

---

## Word on `box-sizing` property of CSS

Excellent—let’s break down the **`box-sizing`** property in CSS in a clear, practical way.

---

## 1️⃣ What does `box-sizing` do?

It controls **how the browser calculates the width and height** of an element.

Specifically, it decides **what’s included in the width/height** you set in CSS:

- Just the **content**

- Or **content + padding + border**

---

## 2️⃣ The two main values

### ✅ `content-box` (default)

- Width and height **only include the content**.

- Padding and border are **added outside** this size.

Example:

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  box-sizing: content-box; /* default */
}
```

**Rendered size:**

- Content: 200px

- Total width = 200 + (2×20) padding + (2×5) border = **250px**

---

### ✅ `border-box`

- Width and height **include** content, padding, and border.

- Padding and border **shrink the content area** if needed.

Example:

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  box-sizing: border-box;
}
```

**Rendered size:**

- Total width = **200px** (fixed)

- Content size adjusts to fit inside with padding and border.

---

## 3️⃣ Why use `border-box`?

✅ Makes layouts easier to manage.  
✅ Total size doesn’t unexpectedly grow when you add padding or border.  
✅ Popular in modern CSS:

```css
* {
  box-sizing: border-box;
}
```

This rule makes all elements use `border-box`, simplifying layout calculations.

---

## 4️⃣ Example comparison

| Property   | `content-box`                       | `border-box`                        |
| ---------- | ----------------------------------- | ----------------------------------- |
| Set width  | Content only (padding/border extra) | Includes content + padding + border |
| Total size | Grows if padding/border added       | Fixed as you defined it             |

---

## 5️⃣ Other values

- `inherit` – takes from parent

- `initial` – default (content-box)

- `unset` – removes applied value

---

## 6️⃣ Quick tip (recommended practice)

Many developers use:

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

✅ Ensures consistent sizing across all elements.

---

------------

## Make the input button work with `onclick`

```html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <input type="text" id="input-el">
        <button id="input-btn" onclick="saveLead()">SAVE INPUT</button>
        <script src="index.js"></script>
    </body>
</html>
```

```javascript
// Log out "Button clicked!" when the user clicks the "SAVE INPUT" button

function saveLead() {
    console.log("Button clicked!")
}
```

## Refactor to `addEventListener`

```js
let inputBtn = document.getElementById("input-btn")

inputBtn.addEventListener("click", function() {
    console.log("Button clicked from addEventListener")
})
```

---

---

Great! Let’s understand `addEventListener` in JavaScript — it’s one of the most important things for making web pages interactive.

---

## 🔧 What is `addEventListener`?

`addEventListener()` is a method used to **attach an event handler** to an HTML element — meaning, you can tell the browser to "do something" when a specific action happens (like a click, keypress, scroll, etc.).

---

## ✅ Basic Syntax

```javascript
element.addEventListener(event, function, useCapture);
```

### Parameters:

- **`event`** – the name of the event as a string (e.g., `"click"`, `"keydown"`)

- **`function`** – the code to run when the event happens (can be a named or anonymous function)

- **`useCapture`** *(optional)* – true or false (mostly used for advanced bubbling vs capturing behavior)

---

## 💡 Example: Button Click

```html
<button id="myBtn">Click Me</button>
<script>
  const btn = document.getElementById("myBtn");

  btn.addEventListener("click", function () {
    alert("Button was clicked!");
  });
</script>
```

✅ This shows an alert when the button is clicked.

---

## 🔁 Why use `addEventListener` instead of `onclick`?

- You can add **multiple listeners** to the same element.

- Keeps **HTML and JS separate** (cleaner code).

- Gives you more control (like removing listeners later).

Example with multiple handlers:

```javascript
btn.addEventListener("click", () => console.log("Click 1"));
btn.addEventListener("click", () => console.log("Click 2"));
```

---

## 🔄 Removing an Event Listener

To remove it, you must use a **named function**, like this:

```javascript
function greet() {
  alert("Hello!");
}

btn.addEventListener("click", greet);
btn.removeEventListener("click", greet);
```

> 🚫 You **can't** remove an anonymous function because it has no name to reference.

---

## 🎯 Common Events

| Event       | Trigger                  |
| ----------- | ------------------------ |
| `click`     | when user clicks         |
| `mouseover` | when mouse hovers        |
| `keydown`   | when a key is pressed    |
| `submit`    | when a form is submitted |
| `input`     | when input field changes |

---

## 🧠 Bonus: Arrow function vs regular function

Be careful when using arrow functions if you need access to `this` keyword (e.g. in classes), since `this` behaves differently in arrow functions.

---

---

## Create the `myLeads` array and `inputEl`

```js
// Create two variables:
// myLeads -> should be assigned to an empty array
// inputEl -> should be assigned to the text input field
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")

inputBtn.addEventListener("click", function() {
    console.log("Button clicked!")
})
```

---

---

Absolutely! Let's break down `let` vs `const` in **JavaScript** in a clean, clear way—covering their differences, use-cases, and **why/when** to choose one over the other.

---

## 🔑 1. What are `let` and `const`?

Both are used to declare **variables** in JavaScript (ES6 and later).

```js
let age = 25;
const name = "Priyansh";
```

They **replace `var`**, which had confusing scoping issues. `let` and `const` solve those.

---

## 🧠 2. Key Differences Between `let` and `const`

| Feature       | `let`                           | `const`                          |
| ------------- | ------------------------------- | -------------------------------- |
| Reassignable? | ✅ Yes                           | ❌ No (value can't be reassigned) |
| Redeclarable? | ❌ No (in the same scope)        | ❌ No                             |
| Block-scoped? | ✅ Yes                           | ✅ Yes                            |
| Hoisting      | ✅ Yes (but **not initialized**) | ✅ Yes (but **not initialized**)  |

---

## 🔁 3. Example: Reassignment

```js
let count = 5;
count = 10;   // ✅ Works

const PI = 3.14;
PI = 3.14159; // ❌ Error: Assignment to constant variable
```

> `const` means the variable **must stay the same reference** — it cannot be re-assigned.

---

## 📦 4. But Wait! `const` is *not* always constant inside!

When the value is an **object or array**, you *can* still modify the internal data:

```js
const user = { name: "Ava" };
user.name = "Zoe";  // ✅ Works

user = {}; // ❌ Error: can't reassign the variable
```

So: `const` protects the **variable**, not the **contents** of the object.

---

## 📐 5. Scope Comparison

Both `let` and `const` are **block-scoped**, meaning they exist **only inside `{}` where they're defined**.

```js
{
  let x = 10;
  const y = 20;
}
console.log(x); // ❌ ReferenceError
```

Unlike `var`, which is **function-scoped** and can leak outside blocks.

---

## ⚠️ 6. Temporal Dead Zone (TDZ)

If you access a `let` or `const` variable **before it's declared**, you get an error:

```js
console.log(a); // ❌ ReferenceError
let a = 5;
```

Even though they are hoisted, they are **not initialized** until the declaration line.

---

## 🧭 7. When to use what?

### ✅ Use `const`:

- By default, for all variables you don't plan to reassign.

- Safer: avoids accidental changes.

- Makes your code more predictable.

### ✅ Use `let`:

- When you **know** you'll reassign the value.

- Example: loops, counters, user input updates, etc.

```js
let score = 0;
score += 10;
```

---

## ✅ Best Practice:

> 🔒 Use `const` by default. Only use `let` when reassignment is required.

It makes your code easier to debug and maintain.

---

---

## Push to the `myLeads` array

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")

// Push the value "www.awesomelead.com" to myArray when the input button is clicked

inputBtn.addEventListener("click", function() {
    myLeads.push("www.awesomelead.com")
    console.log(myLeads)
})
```

## Push the value from the input field using `input.value`

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")

inputBtn.addEventListener("click", function() {
    // Push the value from the inputEl into the myLeads array 
    // instead of the hard-coded "www.awesomeleads.com" value
    // Google -> "get value from input field javascript"
    myLeads.push(inputEl.value)
    console.log(myLeads)
})
```

## Use a `for` loop to log out the leads

```js
for (let i = 0; i < myLeads.length; i++) {
    console.log(myLeads[i])
}
```

## Create the unordered list

```html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <input type="text" id="input-el">
        <button id="input-btn">SAVE INPUT</button>
        <!-- 1. Create an unordered list element (<ul>) with id="ul-el" -->
        <ul id="ul-el"></ul>
        <script src="index.js"></script>
    </body>
</html>
```

```js
let myLeads = ["www.awesomelead.com", "www.epiclead.com", "www.greatlead.com"]
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
// 2. Grab the unordered list and store it in a const variable called ulEl
const ulEl = document.getElementById("ul-el")

console.log(ulEl)

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    console.log(myLeads)
})


for (let i = 0; i < myLeads.length; i++) {
    console.log(myLeads[i])
}
```

## Render the leads in the unordered list using `innerHTML`

```js
let myLeads = ["www.awesomelead.com", "www.epiclead.com", "www.greatlead.com"]
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    console.log(myLeads)
})


for (let i = 0; i < myLeads.length; i++) {
    ulEl.innerHTML += "<li>" + myLeads[i] + "</li>"
}
```

<img src="file:///C:/Users/DEll/AppData/Roaming/marktext/images/2025-07-16-13-33-22-image.png" title="" alt="" width="196">

---

---

Excellent—let’s talk about **how to add content to a container** in HTML using JavaScript.

"Container" here just means any HTML element that holds other elements (like a `<div>`, `<section>`, etc.).

Below I'll show you **step by step** how to do it, with **clear examples**.

---

## ✅ 1️⃣ The HTML Container Example

Here’s a basic container in HTML:

```html
<div id="container"></div>
```

---

## ✅ 2️⃣ Adding Content with `.innerHTML`

You can *replace* or *add* HTML inside it.

**Replace existing content**:

```javascript
document.getElementById('container').innerHTML = '<p>Hello!</p>';
```

✅ Now the container has:

```html
<p>Hello!</p>
```

---

**Append (add without deleting old content)**:

```javascript
document.getElementById('container').innerHTML += '<p>Another line</p>';
```

✅ Now it has both:

```html
<p>Hello!</p>
<p>Another line</p>
```

⚠️ **Note**: innerHTML += can be inefficient for big/complex DOM structures.

---

## ✅ 3️⃣ Adding Elements with `appendChild()`

A safer, cleaner way:

```javascript
const container = document.getElementById('container');

const newElement = document.createElement('p');
newElement.textContent = 'I am new here!';

container.appendChild(newElement);
```

✅ This *adds* a new `<p>` inside the container without touching existing children.

---

## ✅ 4️⃣ Using `append()`

`append()` is even more flexible:

```javascript
container.append('Plain text too!', newElement);
```

✅ You can add multiple nodes or strings at once.

---

## ✅ 5️⃣ Using `insertAdjacentHTML()`

If you want to insert HTML at a *specific position*:

```javascript
container.insertAdjacentHTML('beforeend', '<p>Appended at end!</p>');
```

Positions can be:

- `"beforebegin"` – before the container itself

- `"afterbegin"` – inside, at the start

- `"beforeend"` – inside, at the end

- `"afterend"` – after the container itself

---

## ✅ 6️⃣ Full Example

```html
<div id="container"></div>
<button id="addButton">Add Item</button>

<script>
  const container = document.getElementById('container');
  const button = document.getElementById('addButton');

  button.addEventListener('click', () => {
    const item = document.createElement('p');
    item.textContent = 'New item added!';
    container.appendChild(item);
  });
</script>
```

✅ Every time you click the button, a new `<p>` is added to the container.

---

## 🧭 TL;DR

✅ **Replace** content:

```javascript
container.innerHTML = 'New content';
```

✅ **Append** HTML (less recommended for complex updates):

```javascript
container.innerHTML += 'More content';
```

✅ **Safer: Add element node**:

```javascript
container.appendChild(newElement);
```

✅ **Flexible insert**:

```javascript
container.insertAdjacentHTML('beforeend', '<p>New!</p>');
```

---

---

## Use `createElement()` and `append()` instead of `innerHTML`

```js
let myLeads = ["www.awesomelead.com", "www.epiclead.com", "www.greatlead.com"]
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    console.log(myLeads)
})

// Let's try a different method!
for (let i = 0; i < myLeads.length; i++) {
    ulEl.innerHTML += "<li>" + myLeads[i] + "</li>"
    // create element
    // set text content
    // append to ul
    const li = document.createElement("li")
    li.textContent = myLeads[i]
    ulEl.append(li)
}
```

## Improving the performance of our app

```js
let myLeads = ["www.awesomelead.com", "www.epiclead.com", "www.greatlead.com"]
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    console.log(myLeads)
})

// 1. Create a variable, listItems, to hold all the HTML for the list items
// Assign it to an empty string to begin with
let listItems = ""
for (let i = 0; i < myLeads.length; i++) {
    // 2. Add the item to the listItems variable instead of the ulEl.innerHTML
    listItems += "<li>" + myLeads[i] + "</li>"
}
// 3. Render the listItems inside the unordered list using ulEl.innerHTML
ulEl.innerHTML = listItems
```

> DOM Manipulation comes with a cost.

## Create the render function

Important Code -

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    // 2. Call the renderLeads() function
    renderLeads()
})

// 1. Wrap the code below in a renderLeads() function
function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += "<li>" + myLeads[i] + "</li>"
    }
    ulEl.innerHTML = listItems
}
```

## Clear out the input field

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    // Clear out the input field
    inputEl.value = ""
    renderLeads()
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += "<li>" + myLeads[i] + "</li>"
    }
    ulEl.innerHTML = listItems  
}
```

## Aside : Another way to render the leads

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    renderLead()
    inputEl.value = ""
})

function renderLead() {
    let listItem = "<li>" + inputEl.value + "</li>"
    ulEl.innerHTML += listItem
}
```

## Add the `<a>` tag

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    renderLeads()
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        // Wrap the lead in an anchor tag (<a>) inside the <li>
        // Can you make the link open in a new tab?
        listItems += "<li><a target='_blank' href='" + myLeads[i] + "'>" + myLeads[i] + "</a></li>"
    }
    ulEl.innerHTML = listItems  
}
```

> Note that here we have to add the **javascript variable** inside the **HTML element**, hence we used the `' " + myLeads[i] + " '`.

## Using Template Strings/literals

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    renderLeads()
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
     // listItems += "<li><a target='_blank' href='" + myLeads[i] + "'>" + myLeads[i] + "</a></li>"
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

**Benefits of using Template Strings/literals**

- Break the HTML syntax into multiple lines so that it looks how it should look like.

- Clear Syntax for writing JavaScript variables inside the strings to be added to our DOM.

- Concatenation becomes a piece of cake.

- Strings appear as they are inside the template strings.

- Example 

- ```js
  // template strings/literals
  
  const recipient = "James"
  
  // Refactor the email string to use template strings
  const email = "Hey " + recipient + "! How is it going? Cheers Per"
  
  console.log
  ```

- ```js
  // template strings/literals
  
  const recipient = "James"
  
  // Refactor the email string to use template strings
  const email = `Hey ${recipient}! How is it going? Cheers Per`
  
  console.log
  ```

## Aside : Converting Strings to Numbers with `Number()`

By default, `input.value` is always returned as a string. To convert it into a number, we write - `Number(input.value)`. If the `input.value` contains characters other than string, then the `Number` function won't be able to convert it into a number and then it returns `NaN` which stands for **Not a Number**

## Style the list

```html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <a href="#">Home</a>
        <input type="text" id="input-el">
        <button id="input-btn">SAVE INPUT</button>
        <ul id="ul-el">
        </ul>
        <script src="index.js"></script>
    </body>
</html>
```

```css
body {
    margin: 0;
    padding: 10px;
    font-family: Arial, Helvetica, sans-serif;
}

input {
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
    border: 1px solid #5f9341;
    margin-bottom: 4px;
}

button {
    background: #5f9341;
    color: white;
    padding: 10px 20px;
    border: none;
    font-weight: bold;
}


/* STYLE THE LIST ACCORDING TO THE DESIGN */
ul {
    margin-top: 20px;
    list-style: none;
    padding-left: 0;
}

li {
    margin-top: 5px;
}

li a { /*This is how we target the a tags which are only inside the li tags*/
    color: #5f9341;
}
```

Our Output looks something like this -

<img src="file:///C:/Users/DEll/AppData/Roaming/marktext/images/2025-07-16-15-15-31-image.png" title="" alt="" width="359">

**Let's prepare our app for deployment**

## Little changes to the body selector in CSS - setting `min-width` for our chrome extension.

```css
body {
    margin: 0;
    padding: 10px;
    font-family: Arial, Helvetica, sans-serif;
    min-width: 400px;
}
```

### Creating a `manifest.json` file like this -

```json
{
    "manifest_version": 3,
    "version": "1.1",
    "name": "Leads tracker",
    "action": {
        "default_popup": "index.html",
        "default_icon": "icon.png"
    }
}
```

Now, we need to do something so that we can keep our sales leads saved (across page refreshes) even after refreshing the page or opening the chrome again later.

## What is localStorage ?

It's like a local database we can use. When we open the dev tools in chrome and go to the `Application` tab, there we will something called as `localStorage`.

It stores `key: value` pairs.

`localStorage.clear()` would clear out the localStorage key:value pairs completely.

`localStorage.setItem("key", "value")` is what we are looking for since it persists the data across page refreshes.

To get the value of the item we saved in the localStorage, we write `localStorage.getItem("keyName")`

`localStorage` object is always available to us whenever we are working with the `JavaScript`. Both key and value need to be strings as they are very primitive database.

## Storing Arrays in loalStorage

The keys and values stored with `localStorage` are always in the UTF-16 DOMString format, which uses two bytes per character. As with objects, integer keys are automatically converted to strings.

**localStorage** only supports **STRINGS**. Hence we need to convert our array into a string before being able to store it.

Example to convert strings to arrays using `JSON.parse()`.

```js
let myLeads = `["www.awesomelead.com"]` // myLeads is a string clearly

myLeads = JSON.parse(myLeads) // JSON.parse parses the string into an array

myLeads.push("www.epiclead.com") // push() method exists only on the strings

console.log(myLeads) // console logs out the myLeads array
```

Example to convert arrays into strings using `JSON.stringify`

```js
let myLeads = ["www.awesomelead.com"]

myLeads = JSON.stringify(myLeads)

console.log(typeof myLeads) // prints string
```

Hence, by using `JSON` methods, we can flip back and forth between **strings** and **arrays**. Infact, a more common use case is converting a **JSON** object into a **JS**  object and vice versa.

Complete Example -

```js
let myLeads = `["www.awesomelead.com"]`

// 1. Turn the myLeads string into an array
myLeads = JSON.parse(myLeads)
// 2. Push a new value to the array
myLeads.push("www.lead2.com")
// 3. Turn the array into a string again
myLeads = JSON.stringify(myLeads)
// 4. Console.log the string using typeof to verify that it's a string
console.log(typeof myLeads)
```

## Save the leads to localStorage

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    // Save the myLeads array to localStorage 
    // PS: remember JSON.stringify()
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    renderLeads()

    // To verify that it works:
    console.log( localStorage.getItem("myLeads") )
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

But, here we are not actually displaying the already saved leads. Hence,

## Get the leads from the local storage

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

// Get the leads from the localStorage - PS: JSON.parse()
// Store it in a variable, leadsFromLocalStorage
// Log out the variable
localStorage.
let leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )

console.log(leadsFromLocalStorage)

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    renderLeads()

    // To verify that it works:
    console.log( localStorage.getItem("myLeads") )
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

> `Null` is a falsy value that we developers use to signalize emptiness. Whereas, the returned `array` from the localStorage would be seen as a truthy value. 

## Important - Truthy and falsy values

```js
// Anything which is read by JS as true is a truthy value.
// And anything which is read by JS as false is a falsy value.
// Any number other than 0 is a truthy value
// Number 0 is a falsy value
// Empty string is a falsy value
// Filled string is a truthy value
// Filled array is a truthy value
// Empty array is a truthy value as well
```

```js
List of falsy values :
// false (mostly used)
// 0  (mostly used)
// ""
// null  (mostly used)
// undefined  (mostly used)
// NaN
```

> `Null` and `undefined` both are primitive data-types which signal emptiness. The core difference is - `Null` is how you as a developer signalize emptiness whereas `undefined` is how JavaScript signalizes emptiness.

Example of `null`

```js
let currentViewers = null

currentViewers = ["jane", "nick"]

currentViewers = null

if (false) {
    // do something , e.g. notify the live streamers
    console.log("we have viewers")
}
```

Here, `null` we used to signalize emptiness as developers.

Example of `undefined`

```js
let currentViewers
console.log(currentViewers)  // prints undefined


let currentViewers = {}
console.log(currentViewers.randomKey)  // prints undefined
```

> To check if some value is truthy or falsy, we can write - `console.log(Boolean(value))`.

## Checking the localStorage before rendering

If the key `"myLeads"` does not exist in localStorage, if we do `localStorage.getItem("myLeads")`, we will get `null`.

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")

// ["lead1", "lead2"] or null
let leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )

// 1. Check if leadsFromLocalStorage is truthy
// 2. If so, set myLeads to its value and call renderLeads()

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    renderLeads()
}

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    renderLeads()
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

## Style the delete button like this

<img src="file:///C:/Users/DEll/AppData/Roaming/marktext/images/2025-07-17-16-38-23-image.png" title="" alt="" width="402">

```css
button {
    background: #5f9341;
    color: white;
    padding: 10px 20px;
    border: 1px solid #5f9341;
    font-weight: bold;
}

#delete-btn {
    background: white;
    color: #5f9341;
}
```

## Make the delete button work

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
// 1. Store the delete button in a deleteBtn variable
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    renderLeads()
}

// 2. Listen for double clicks on the delete button (google it!)
// 3. When clicked, clear localStorage, myLeads, and the DOM

deleteBtn.addEventListener("dblclick", function() {
    console.log("double clicked!")
    localStorage.clear()
    myLeads = []
    renderLeads()
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    renderLeads()
})

function renderLeads() {
    let listItems = ""
    for (let i = 0; i < myLeads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${myLeads[i]}'>
                    ${myLeads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems  
}
```

## How function parameters can improve our code

**Reusablity** of the code is a very important topic in itself. We will understand it by making our `renderLeads()` function re-usable.

Let's say we have an array for the Old-leads as well or maybe it will be a future feature to be included, but our `renderLeads()` function always targets the `myLeads` array 

```js
let myLeads = []
let oldLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    render(myLeads)
}

function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}

deleteBtn.addEventListener("dblclick", function() {
    localStorage.clear()
    myLeads = []
    render(myLeads)
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```

## Aside : Function Parameters

```js
const welcomeEl = document.getElementById("welcome-el")

// Add the ability to choose the emoji as well!

function greetUser(greeting, name) {
    welcomeEl.textContent = `${greeting}, ${name} ${emoji}`
}

greetUser("Howdy", "James", ":heart:")
```

## Aside : Argumenets vs Parameters

Parameters are inside of the function, whereas, Arguments are outside of the function.

While declaration of the function, we call them **parameters** and while invoking a function, we call them **arguments**

## Passing arrays as parameters

```js
// Create a function, getFirst(arr), that returns the first item in the array
const getFirst = (arr) => {
    return arr[0]
}


// Call it with an array as an argument to verify that it works
getFirst(["Priyansh"])
```

## New feature - Save Tab Button

### Create the **tabBtn**

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )
// 1. Grab the SAVE TAB button and store it in a tabBtn variable
const tabBtn = document.getElementById("tab-btn")

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    render(myLeads)
}

const tabs = [
    {url: "https://www.linkedin.com/in/per-harald-borgen/"}
]

// 2. Listen for clicks on tabBtn. Log Per's LinkedIn URL to the console
tabBtn.addEventListener("click", function(){
    console.log(tabs[0].url)
})

function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}

deleteBtn.addEventListener("dblclick", function() {
    localStorage.clear()
    myLeads = []
    render(myLeads)
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```

### Save the tab url

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )
const tabBtn = document.getElementById("tab-btn")

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    render(myLeads)
}

const tabs = [
    {url: "https://www.linkedin.com/in/per-harald-borgen/"}
]

tabBtn.addEventListener("click", function(){
    // Save the url instead of logging it out
    myLeads.push(tabs[0].url)
    localStorage.setItem("myLeads", JSON.stringify(myLeads))
    render(myLeads)
})

function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}

deleteBtn.addEventListener("dblclick", function() {
    localStorage.clear()
    myLeads = []
    render(myLeads)
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```

### How to get the current tab ?

`chrome.tab` 

**Description** - Use the chrome.tabs API to ineract with the browser's tab system. You can use this API to create, modify and rearrange tabs in the browser

**Use the Chrome API to get the tab**

```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )
const tabBtn = document.getElementById("tab-btn")

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    render(myLeads)
}

const tabs = [
    {url: "https://www.linkedin.com/in/per-harald-borgen/"}
]


tabBtn.addEventListener("click", function(){
    // chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
    // })
    
    chrome.tabs.query({active: true, currentWindow: true}, function(tabs){
        console.log(tabs)
        
        
    })
    
    myLeads.push(tabs[0].url)
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
    
})

function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}

deleteBtn.addEventListener("dblclick", function() {
    localStorage.clear()
    myLeads = []
    render(myLeads)
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```

**Important Code to save tabs**
```js
chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
    myLeads.push(tabs[0].url)
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```

Thus, the whole code looks like this -
```js
let myLeads = []
const inputEl = document.getElementById("input-el")
const inputBtn = document.getElementById("input-btn")
const ulEl = document.getElementById("ul-el")
const deleteBtn = document.getElementById("delete-btn")
const leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )
const tabBtn = document.getElementById("tab-btn")

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    render(myLeads)
}

tabBtn.addEventListener("click", function(){    
    chrome.tabs.query({active: true, currentWindow: true}, function(tabs){
        myLeads.push(tabs[0].url)
        localStorage.setItem("myLeads", JSON.stringify(myLeads) )
        render(myLeads)
    })
})

function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}

deleteBtn.addEventListener("dblclick", function() {
    localStorage.clear()
    myLeads = []
    render(myLeads)
})

inputBtn.addEventListener("click", function() {
    myLeads.push(inputEl.value)
    inputEl.value = ""
    localStorage.setItem("myLeads", JSON.stringify(myLeads) )
    render(myLeads)
})
```
Also, updating the manifest.json file to -
```json
{
    "manifest_version": 3,
    "version": "1.0",
    "name": "Leads tracker",
    "action": {
        "default_popup": "index.html",
        "default_icon": "icon.png"
    },
    "permissions": [
        "tabs"
    ]
}
```

## Recap 
- `const`
- `addEventListener()`
- `innerHTML`
- `input.value`
- function paramters / arguments
- template strings - write multiple line strings preserving spaces, ENTER, and much cleaner way of intgrating JS variables in the HTML code and other strings.
- localStorage 
- JSON - JSON.strigify() and JSON.parse() methods
- Objects in arrays
---
