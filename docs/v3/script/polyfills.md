# Polyfills

Patching legacy IE JavaScript support

Polyfills are used to patch browser incompatibilities and inconsistencies. Wee ships with a couple basic components. If you don’t need them just remove them from the IE10 compile array.

## Placeholder

The Wee placeholder polyfill patches support for the placeholder attribute on inputs and textareas. It sets the value to the placeholder but clears it on focus and form post to mimic native placeholder functionality.

### Placeholder

```html
<input type="text" name="title" placeholder="Entry Title">
<textarea name="message" placeholder="Write your message..."></textarea>
```

## Slice

This polyfill adds support for slicing [NodeLists](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) and [HTMLCollections](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection) which is useful when working with the DOM in IE9 and below.

```js
var elements = Array.prototype.slice.call(nodeList);
```

Wee requires the slice polyfill for compatibility with IE9 and below.