## 🚀 HTML Basics

### 🔤 What is HTML?

- **HTML (HyperText Markup Language)** is the standard markup language for creating web pages.
- It defines the **structure and meaning** of content using **elements** (tags).

### 📄 Basic Page Structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My Web Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

### 🔍 Key Elements

|Tag|Purpose|
|---|---|
|`<!DOCTYPE html>`|Declares HTML5 document|
|`<html>`|Root element|
|`<head>`|Metadata, title, links|
|`<body>`|Content shown to users|

## 📝 Text & Headings

### 🔡 Headings

- HTML supports 6 heading levels: `<h1>` to `<h6>`
- `<h1>` is most important, usually used once per page (e.g. page title)

```html
<h1>Main Title</h1>
<h2>Subheading</h2>
<h3>Section Title</h3>
```

> ✅ **Best Practice:** Use headings in hierarchical order for accessibility and SEO.

### 📌 Paragraphs & Inline Text

```html
<p>This is a paragraph of text.</p>
<em>Emphasized text</em>
<strong>Important text</strong>
<br /> <!-- Line break -->
<span>This is inline text</span>
```

|Tag|Role|
|---|---|
|`<p>`|Paragraph|
|`<br>`|Line break|
|`<em>`|Emphasized (italic)|
|`<strong>`|Important (bold)|
|`<span>`|Inline wrapper (useful for styling)|

## 🔗 Links, Images, and Lists

### 🔗 Links (`<a>`)

```html
<a href="https://github.com" target="_blank">Visit GitHub</a>
<a href="/about.html">About Us</a>
```

> ✅ `target="_blank"` opens the link in a new tab.  
> ⚠️ Always include `alt` for accessibility with images.

### 🖼️ Images (`<img>`)

```html
<img src="img/pic.jpg" alt="Description of image" width="400" />
```

|Attribute|Purpose|
|---|---|
|`src`|Image path|
|`alt`|Text shown if image fails to load|
|`width` / `height`|Resize image|

### 📋 Lists

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<ol>
  <li>Step 1</li>
  <li>Step 2</li>
</ol>
```

|Tag|Type|
|---|---|
|`<ul>`|Unordered list (bullets)|
|`<ol>`|Ordered list (numbers)|
|`<li>`|List item|

## 🧾 HTML Forms

### 🔐 Inputs & Fields

```html
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required />

  <label for="email">Email:</label>
  <input type="email" id="email" required />

  <input type="submit" value="Submit" />
</form>
```

|Input Type|Description|
|---|---|
|`text`|Single-line input|
|`email`|Validates email|
|`password`|Hides characters|
|`radio` / `checkbox`|Select options|
|`select` / `option`|Dropdown list|
|`textarea`|Multi-line input|

> ✅ Always link `label` to input using `for="id"`  
> ✅ Use `placeholder`, `required`, and `name` attributes for good form UX.

## 🧠 HTML5 Semantic Tags

Semantic elements clearly describe their meaning in a human- and machine-readable way.

|Tag|Meaning|
|---|---|
|`<header>`|Top of the page or section|
|`<nav>`|Navigation links|
|`<main>`|Main content of the page|
|`<section>`|Thematic group of content|
|`<article>`|Standalone content (e.g. blog post)|
|`<footer>`|Bottom of the page|

### 🧪 Example

```html
<main>
  <article>
    <h2>News Article</h2>
    <p>Some news content...</p>
  </article>

  <section>
    <h3>More Info</h3>
    <p>Extra details here.</p>
  </section>
</main>
```

> ✅ **Use semantic tags** for better SEO and accessibility.  
> ❌ **Don’t use `<div>` or `<span>` everywhere** — they have no semantic meaning.

## 🧩 HTML Mini Challenges

Try these on your own:

1. **Build a profile card**  
    Includes name, image, short bio, and link.
2. **Create a simple contact form**  
    Include name, email, message, and submit button.
3. **Create a blog layout**  
    Use semantic tags to structure: header, nav, main, article, footer.
4. **List your favorite movies**  
    Use an unordered list with images and descriptions.
## 🔚 Wrap-up

|Concept|Summary|
|---|---|
|HTML|Structures content using tags|
|Elements|Can be block (e.g. `<div>`, `<h1>`) or inline (`<span>`, `<a>`)|
|Semantic Tags|Make content easier to understand|
|Forms|Used for collecting user input|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**