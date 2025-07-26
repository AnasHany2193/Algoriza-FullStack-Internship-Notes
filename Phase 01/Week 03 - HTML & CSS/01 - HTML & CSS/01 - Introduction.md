## 🧠 What is the Web?

- The web is a collection of **websites**, accessed via the **Internet**, made up of web pages.    
- These pages are written in **HTML**, styled with **CSS**, and often made interactive with **JavaScript**.
- Web browsers (like Chrome, Firefox, Edge) interpret this code and render the final page.

## 🧱 What is HTML?

**HTML** stands for **HyperText Markup Language**

🔹 It is used to **structure** content on the page  
🔹 Defines elements like:
- Paragraphs (`<p>`)
- Headings (`<h1>`–`<h6>`)
- Links (`<a>`)
- Images (`<img>`)
- Forms, buttons, lists, and more

### ✏️ Example

```html
<p>This is a paragraph</p>
<a href="https://example.com">Visit Site</a>
<img src="cat.jpg" alt="Cute Cat" />
```

### 🧩 Tags = Building Blocks

HTML uses **tags** to mark up content. Most tags come in **pairs**:

```html
<tagname> content goes here </tagname>
```

## 🎨 What is CSS?

**CSS** stands for **Cascading Style Sheets**

🔹 It is used to **style** and visually enhance HTML content  
🔹 Controls:
- Colors, fonts, sizes
- Layout and spacing
- Positioning
- Animations and effects

### ✏️ Example

```css
p {
  color: blue;
  font-size: 16px;
}
```

You can link CSS to HTML like this:

```html
<link rel="stylesheet" href="styles.css" />
```

## 🏗️ Structure of a Basic Webpage

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My First Web Page</title>
  </head>
  <body>
    <h1>Welcome to the Web</h1>
    <p>This is an awesome site.</p>
  </body>
</html>
```

### 💡 Breakdown:

|Part|Role|
|---|---|
|`<!DOCTYPE html>`|Declares this is an HTML5 document|
|`<html>`|Root of the document|
|`<head>`|Metadata: title, charset, links|
|`<body>`|Content visible to the user|

## 🛠️ Browser Dev Tools

Every browser has **developer tools**. You can open them with `F12` or right-click → “Inspect”.

🔧 You can:
- View/edit HTML & CSS live
- See console logs and errors
- Test responsiveness
- Debug JavaScript

## 🖼️ Visual: Web Development Flow

```plaintext
[ User ] ⇄ [ Browser ]
	            ⇓
	        [ HTML ] - Structure
	        [ CSS  ] - Style
	        [ JS   ] - Interactivity
```

## ✅ Summary

|Topic|Purpose|
|---|---|
|**HTML**|Structures the content|
|**CSS**|Styles and designs the page|
|**Browser**|Displays the web page|
|**Dev Tools**|Debug and inspect code|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**
