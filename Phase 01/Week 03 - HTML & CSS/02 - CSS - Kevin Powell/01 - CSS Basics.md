# 🟦 CSS: Cascading Style Sheets – Basics

**Definition:**  
CSS is a language used to describe the presentation (style and layout) of HTML documents. It controls how elements look on the page — including colors, spacing, fonts, layouts, and responsiveness.

## ✅ CSS Syntax

```css
selector {
  property: value; /* This is a declaration */
}
```

- **Selector**: Targets the HTML element(s) (e.g. `p`, `.btn`, `#header`)
- **Property**: The style you want to change (e.g. `color`, `font-size`)
- **Value**: The value assigned to the property (e.g. `red`, `24px`)
- A collection of declarations is called a **rule set**

## 🔍 CSS Selectors

### 🔸 Universal Selector

```css
* {
  background-color: #eeeeee;
}
```

- Selects **all elements** on the page

### 🔸 Class Selector

```css
.gray {
  color: gray;
}
```

- Targets elements with class `gray` (e.g. `<p class="gray">`)

### 🔸 ID Selector

```css
#second {
  font-style: italic;
}
```

- Targets a single element with ID `second` (IDs must be unique)

### 🔸 Group Selector

```css
h1, h2 {
  color: blue;
}
```

- Applies the same styles to both `h1` and `h2`

### 🔸 Descendant Selector

```css
p span {
  background-color: gold;
  text-transform: uppercase;
}
```

- Targets `<span>` inside `<p>`, and styles only those

## 🎨 Colors in CSS

You can define colors in multiple ways:

```css
p {
  color: papayawhip;              /* Named color */
  color: rgb(70, 70, 70);         /* Red, Green, Blue */
  color: rgba(70, 70, 70, 0.8);   /* RGB with opacity */
  color: #444444;                 /* Hexadecimal */
  color: #444;                    /* Shorthand HEX */
  color: hsl(0, 2%, 32%);         /* Hue, Saturation, Lightness */
}
```

💡 **Tip:** Use tools like [Coolors](https://coolors.co/) or [ColorZilla](https://www.colorzilla.com/) for picking color palettes.

## 🛠️ Types of CSS: Inline, Internal, External

|Type|How it's written|Use case|
|---|---|---|
|**Inline**|`style="color: red;"` inside an HTML tag|Quick fixes or dynamic styles|
|**Internal**|Inside a `<style>` tag in the `<head>` of HTML|For single-page projects or testing|
|**External**|Linked via `<link rel="stylesheet">`|Best practice for larger projects|

```html
<!-- Internal -->
<head>
  <style>
    p {
      color: red;
    }
  </style>
</head>

<!-- External -->
<link rel="stylesheet" href="styles.css">
```

✅ **Best Practice:** Always prefer **external CSS** for scalability and reusability.

## 🧪 Debugging CSS

- Use **Chrome DevTools (F12)** → "Elements" and "Styles" tabs to inspect, modify, and test CSS live.
- Enable **"Toggle device toolbar"** to preview responsive designs.
- Use the **computed tab** to understand which styles are taking effect (especially when overriding styles).

## 🧠 Summary

|Concept|Summary|
|---|---|
|Syntax|CSS uses selectors + property-value declarations|
|Selectors|Target elements via tag, class, ID, or relationships (like `p span`)|
|Color Modes|CSS supports named, RGB, RGBA, HEX, HSL|
|Types of CSS|Inline, Internal, External — External is the best for real projects|
|Dev Tools|Browser dev tools help inspect and debug styles visually|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**