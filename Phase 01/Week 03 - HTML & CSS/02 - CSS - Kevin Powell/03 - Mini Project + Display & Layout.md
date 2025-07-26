## 🧱 Reset and Base Styling

```css
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin: 0.5rem;
  font-family: "Roboto", sans-serif;
  text-align: center;
}
```

### ✅ Best Practices:

- Use `box-sizing: border-box` for predictable layouts.
- Always apply a CSS reset (`* {}`) to remove browser inconsistencies.
- Use a clean base font (`Roboto` here) for consistent typography

## 🧭 Navigation Layout (Mini Project)

```css
nav {
  border: 2px solid #333;
  border-radius: 2rem;
  margin: 0 auto 1rem;
  max-width: 600px;
  font-size: 3rem;
  line-height: 7rem;
}

nav h2 {
  padding: 1rem;
  background-color: gold;
  border-radius: 2rem 2rem 0 0;
}

nav ul {
  list-style-type: none;
}

nav li {
  border-top: 1px solid #333;
}

nav a {
  display: block;
  text-decoration: none;
  color: #333;
}

nav a:visited {
  color: #333;
}

nav a:hover,
nav a:focus {
  background-color: #333;
  color: whitesmoke;
  cursor: pointer;
}

nav li:last-child a {
  border-radius: 0 0 2rem 2rem;
}
```

## 📐 CSS Display Property

### ✅ Key Display Values:

|Value|Description|
|---|---|
|`block`|Takes full width, starts on a new line (e.g., `<div>`, `<p>`)|
|`inline`|Flows with text, cannot set width/height (e.g., `<span>`, `<a>`)|
|`inline-block`|Like `inline`, but respects width & height|
|`none`|Completely hides the element (not even in layout flow)|
|`flex`, `grid`|For modern layouts (explained in later sections)|

### Example:

```css
.opposite {
  display: inline-block;
  background-color: #333;
  color: whitesmoke;
  height: 50px;
  padding: 10px;
  margin: 10px;
}
```

## 🧾 Horizontal Navigation Example

```css
ul {
  list-style-type: none;
  padding: 0.5rem;
  margin: 0;
  background-color: #000;
  text-align: right;
}

li {
  display: inline-block;
  margin-inline: 0.5rem;
}

li a {
  color: white;
  text-decoration: none;
}

li a:hover,
li a:focus {
  text-decoration: underline;
}
```

✅ `display: inline-block` allows the `<li>` elements to sit side-by-side, unlike the default `block` behavior.

## 🏄 Float Layout

```css
.block {
  width: 30vw;
  height: 30vw;
  background-color: #000;
  color: #fff;
  padding: 1rem;
}

.left {
  float: left;
  margin-right: 1rem;
}

.right {
  float: right;
  margin-left: 1rem;
}

.clear {
  clear: both;
}
```

### Important Notes:

- Floats take elements **out of normal document flow**.
- Use `clear: both;` to stop content from wrapping around floated elements.

✅ Modern alternative: use `flexbox` or `grid` instead of floats for layout!

## 🚿 Clearing Floats

```css
section {
  background-color: bisque;
  border: 1px solid #333;
  padding: 1rem;

  overflow: auto;      /* Safe clearfix method */
  display: flow-root;  /* Newer method for self-contained layout block */
}
```

✅ `display: flow-root` creates a new block formatting context (BFC), preventing float-related collapse.

## 📰 CSS Columns (Multicol Layouts)

You had a heading for columns but no code — here’s a standard example:

```css
.columns {
  column-count: 3;
  column-gap: 2rem;
  column-rule: 1px solid #ccc;
}
```

```html
<section class="columns">
  <p>Lorem ipsum dolor sit amet...</p>
  <p>Aliquam tincidunt mauris eu risus...</p>
  <p>Ut velit mauris, egestas sed...</p>
</section>
```

### Column Properties:

- `column-count`: Number of columns
- `column-gap`: Spacing between columns
- `column-rule`: Line between columns

## 🧠 Summary of Layout Practices

|Topic|Best Practices / Tips|
|---|---|
|Box Model|Always set `box-sizing: border-box` for easier sizing|
|Display|Use `block`, `inline-block`, `none`, and explore `flex`/`grid` for advanced UI|
|Float|Outdated for layout; useful only in special cases (like image wrapping)|
|Clearfix|Use `overflow: auto;` or `display: flow-root;` to clear floats safely|
|Columns|Use for newspaper-style layouts or lightweight multicolumn text|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**