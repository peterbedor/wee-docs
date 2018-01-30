# Classes

Wee tries to stay out of your way and that means shipping with only the bare minimum of helper classes. As demonstrated, many of the helper classes can also be used as mixins.

## Container
Create a centered container based on `$minWidth`, `$maxWidth`, and `$bumperPadding`

```scss
.container {
	@if ($padContainer == true) {
		padding-left: $bumperPadding;
		padding-right: $bumperPadding;
	}

	display: block;
	margin-left: auto;
	margin-right: auto;
	box-sizing: content-box;
	@if ($maxWidth != false) {
		max-width: $maxWidth;
	}

	@if ($minWidth != false) {
		min-width: $minWidth;
	}
}
```

## Image Align
Perfect for alignment of images in content blocks

### Left

```css
.img-left {
    float: left;
    margin-top: .32em;
    margin-right: $imageMarginSide;
    margin-bottom: $imageMarginBottom;
}
```

### Right

```css
.img-left {
    float: right;
    margin-top: .32em;
    margin-bottom: $imageMarginBottom;
    margin-left: $imageMarginSide;
}
```

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
