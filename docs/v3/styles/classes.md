# Classes

Wee tries to stay out of your way and that means shipping with only the bare minimum of helper classes. As demonstrated, many of the helper classes can also be used as mixins.

## Container

Create a centered container based on @minWidth, @maxWidth, and @padContainer

```less
.container {
    .content-box();
    .max-width(@maxWidth);
    .min-width(@minWidth);
    .check () when (@padContainer = true) {
        .padded();
    }
    .check();
}
```

```less|css
.container();

---

display: block;
margin-left: auto;
margin-right: auto;
-moz-box-sizing: content-box;
-webkit-box-sizing: content-box;
box-sizing: content-box;
max-width: 1280px;
min-width: 260px;
padding-left: 6%;
padding-right: 6%;
```

## Image Align

Perfect for alignment of images in content blocks

### Left

```less
.img-left {
    float: left;
    .margin(.32em; @imageMarginSide; @imageMarginBottom; false);
}
```

```less|css
.img-left();

---

float: left;
margin-top: 0.32em;
margin-right: 2rem;
margin-bottom: 2rem;
```

### Right

```less
.img-right {
    float: right;
    .margin(.32em; false; @imageMarginBottom; @imageMarginSide);
}
```

```less|css
.img-right();

---

float: right;
margin-top: 0.32em;
margin-bottom: 2rem;
margin-left: 2rem;
```

The “img-left” and “img-right” class names can be overridden in variables.less.

## JS Hide

Used by the core Wee script to toggle visibility

```css
.js-hide {
    display: none !important;
}
```

## Not Printed

If print styling is enabled exclude elements from being printed

```html
<h1 class="not-printed">This won't be output when printing.</h1>
```