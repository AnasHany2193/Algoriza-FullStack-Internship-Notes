## 📏 Units & Sizes

CSS supports both **absolute** and **relative** units for sizing elements.

### 🔸 Absolute Units

- Don't scale with screen size. Fixed regardless of the device.

```css
cm, mm, in, pt, pc, px
```

- `px`: **Pixels** – most commonly used absolute unit in web design.

### 🔸 Relative Units

- Scale based on another reference (usually parent or root element).

```css
em     /* Relative to the parent element's font size */
rem    /* Relative to the root element's (html) font size */
ex     /* x-height of the font (height of lowercase x) */
ch     /* Width of the character '0' of the current font */
lh     /* Line height of the element */
%      /* Percentage of parent element's size */
vw     /* 1% of the viewport width */
vh     /* 1% of the viewport height */
vmin   /* 1% of the smaller dimension (width or height) */
vmax   /* 1% of the larger dimension (width or height) */
```

✅ **Tip:** Use `rem` for scalable font sizes and spacing. Avoid `px` for responsive layouts.

## 📦 CSS Box Model

Everything on a web page is treated as a **box** in CSS. The box model includes:

```
 ┌─────────────────────────────┐
 │         Margin              │
 │  ┌───────────────────────┐  │
 │  │       Border          │  │
 │  │  ┌─────────────────┐  │  │
 │  │  │    Padding      │  │  │
 │  │  │  ┌───────────┐  │  │  │
 │  │  │  │  Content  │  │  │  │
 │  │  │  └───────────┘  │  │  │
 │  │  └─────────────────┘  │  │
 │  └───────────────────────┘  │
 └─────────────────────────────┘
```

- `content`: Actual text/image inside the element
- `padding`: Space **inside** the border (between content and border)
- `border`: The outer edge around padding
- `margin`: Space **outside** the element (between other elements)

### ✅ Best Practice:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

- `box-sizing: border-box`: Includes padding and border **within** the element's total width/height (more intuitive).

### Example:

```css
.container {
  font-size: 1.5rem;
  margin: 1rem 1.5rem;
  padding: 1.5rem 3rem;
  border: 2px dashed red;
  border-radius: 5px;
  outline: 5px solid purple;
  outline-offset: 5px;
}
```


## 🔠 Typography

Typography controls **how text appears** on the screen.

### Font Setup

```css
body {
  padding: 10%;
  font-size: 1.3rem;
  font-family: "Josefin Sans", sans-serif, "Times New Roman";
}
```

- Use a **font stack** with fallback fonts.
- Set base `font-size` on `body` using `rem` for scalable design.


✅ Use `font: inherit;` on inputs and buttons to match parent font styles.

### Text Styling

```css
p {
  text-decoration: underline;   /* underline, line-through, none */
  text-transform: uppercase;    /* capitalize, lowercase, uppercase */
  text-align: justify;          /* left, right, center, justify */
  text-indent: 2em;             /* indent first line */
  line-height: 1.5em;           /* vertical spacing between lines */
  letter-spacing: 0.1em;        /* space between characters */
  word-spacing: 0.2em;          /* space between words */
  font-weight: bold;            /* normal, bold, 100–900 */
  font-style: italic;           /* normal, italic, oblique */
}
```

## 🔗 Styling Links

```css
a {
  text-decoration: none;
  cursor: pointer;
  color: blue;
}

a:visited {
  color: indigo;
}

a:hover,
a:focus {
  color: dodgerblue;
}

a:active {
  color: red;
}
```

- Use `:hover`, `:focus`, and `:active` pseudo-classes for interactive styling.
- `:visited`: Changes link color after it's clicked
- `cursor: pointer`: Indicates a clickable element

## 📋 Styling Lists

```css
ol {
  list-style-type: none;  /* Removes numbering */
  padding: 0;
}

ul {
  color: #00f;
  line-height: 1.6;
  text-align: center;
  /* list-style-type: square; */
  /* list-style-position: outside; */
  /* list-style-image: url("../images/checkmark.png"); */
  /* list-style: square outside url("../images/checkmark.png"); */
}
```

- Customize list markers using `list-style-type`, `list-style-image`, etc.
- `list-style: type position image;` (shorthand)

### Advanced Marker Styling:

```css
li:nth-child(odd) {
  color: red;
}

::marker {
  color: black;
  font-family: sans-serif;
  content: ":) ";
}
```

- `::marker`: Targets the bullet or number in a list
- `nth-child(odd)`: Applies styles to every odd `<li>`

## 🧠 Summary

|Concept|Description|
|---|---|
|Box Model|Foundation of all layout and spacing in CSS|
|Units|Use `rem`, `%`, `vw/vh` for responsive designs|
|Typography|Controls text appearance: fonts, spacing, alignment|
|Link Styles|Use pseudo-classes for interactive behavior|
|Lists|Style bullets or numbers, change spacing, and use custom markers|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**