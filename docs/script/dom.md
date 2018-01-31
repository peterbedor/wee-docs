# DOM

Easily interface with the DOM for updates and retrieval

Wee makes modifying and extracting data from your markup easy with a robust set of DOM functions. We’ve only included what you need without the cruft. You can also chain your methods.

## $

Get matches to specified selector or return parsed HTML

| Variable | Type      | Default  | Description                     | Required |
|----------|-----------|----------|---------------------------------|----------|
| selector | selection | -        | Target selection or HTML string | ✔        |
| context  | selection | document | Context selection               | -        |

### Simple

```js|js
import $ from'wee-dom';

$('.js-element li');

---

[node, node, ...]
```

### Contextual

The context selection subsets the query to a more specific scope. This can result in a more limited and efficient traversal of the DOM.

```js|js
import $ from'wee-dom';

---

$('li', '.js-element');

[node, node, ...]
```

### Selection of DOM elements

Wee accepts any browser-supported selection queries. Internally Wee parses the selection string to invoke the most efficient native selection method and returns an array of matching nodes.

### Examples

```js
$('#id');
$('.class');
$('#id .class');
$('.class1, .class2');
$('.parent > .child');
```

### data-ref

References are a logical approach to selecting elements. They are cached when the page loads making them extremely quick to reference and are more visually distinct in markup than js- classes. Anywhere you can pass a standard selector you can also pass a ‘ref:name’ string.

```html|js
<div data-ref="element"></div>

---

$('ref:element');

// Shorthand
$(':element');
```

References can’t be used in subset selectors like `$('ref:element .child')`. To scope a selection within a reference pass the ref selector as the context argument like `$('.child', 'ref:element')`.

If multiple references are set with the same name they are pushed into an array and can be targeted with a single ref selection. You can also provide a comma-delimited list of multiple refs.

```html|js
<div data-ref="element"></div>
<div data-ref="element element2"></div>

---

$('ref:element');

$('ref:element, ref:element2');
```

## $el.addClass

Add classes to each matching selection

| Variable | Type             | Default | Description                      | Required |
|----------|------------------|---------|----------------------------------|----------|
| value    | function, string | -       | Class name(s) to add or callback | ✔        |

### Single

```js
import $ from'wee-dom';

$('ref:element').addClass('modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
import $ from'wee-dom';

$('ref:element').addClass('modifier modifier2');
```

### Function

The current index and class value are injected into the callback. The scope of `this` is the element.

```js
import $ from'wee-dom';

$('ref:element').addClass(function(i, className) {
    // Add an indexed classreturn className + i;
});
```

Note: The index argument is always 0-based.

## $el.after

Insert selection or markup after each matching selection

| Variable | Type                                                 | Default | Description                                | Required |
|----------|------------------------------------------------------|---------|--------------------------------------------|----------|
| source   | function, [selection](/script/dom#selection), string | -       | Source selection, callback, or HTML string | ✔        |
| remove   | boolean                                              | false   | Remove target after insertion              | -        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').after($('.js-element'));
```

### Markup

```js
import $ from'wee-dom';

$('ref:element').after('<span>Injected notice</span>);
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<div data-name="John Smith">
	<h1 data-ref="bioName">Name</h1>
</div>
```

```js
import $ from'wee-dom';

$(ref.bioName').after(function(i, html) {
    // Add the parent data-name as a paragraph after the matched element
    return '<p>' + $data.(this).parent('name') + '</p>;
});
```

```html
<div data-name="John Smith">
	<h1 data-ref="bioName">Name</h1>
	<p>John Smith</p>
</div>
```

## $el.append

Append selection or markup after each matching selection

| Variable | Type                                      | Default | Description                                | Required |
|----------|-------------------------------------------|---------|--------------------------------------------|----------|
| source   | function, [selection](#selection), string |         | Source selection, callback, or HTML string | ✔        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').append($('.js-element'));
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<h1 data-ref="listHeading">Names</h1>
<ul>
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

```js
import $ from'wee-dom';

$('ref:listHeading').append(function(i, html){
    // Modify the heading to include the number of listed namesreturn' (' + $children($next()).length + ')';
});
```

```html
<h1 data-ref="listHeading">Names (2)</h1>
<ul>
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

## $el.attr

Get attribute of first matching selection or set attribute of each matching selection

| Variable  | Type             | Default | Description                          | Required |
|-----------|------------------|---------|--------------------------------------|----------|
| attribute | string, object   | -       | Attribute to get or set or an object | ✔        |
| value     | function, string | -       | Value to assign to attribute         | -        |

### Get

```js|js
import $ from'wee-dom';

$('ref:element').attr('href');

---

"https://www.weepower.com"
```

### Single

```js
import $ from'wee-dom';

$('ref:element').attr('href', 'https://www.weepower.com/start');
```

### Multiple

```js
import $ from'wee-dom';

$('ref:element').attr({
    href: 'https://developer.mozilla.org',
    target: '_blank'
});
```

## $el.before

Insert selection or markup before each matching selection

| Variable | Type                                      | Default | Description                               | Required |
|----------|-------------------------------------------|---------|-------------------------------------------|----------|
| source   | function, [selection](#selection), string | -       | Source selection, callback or HTML string | ✔        |
| remove   | boolean                                   | false   | Remove target after insertion             | -        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').before($('.js-element'));
```

### Markup

```js
import $ from'wee-dom';

$('ref:element').before('<span>Injected notice</span>');
```

### Function

```js
import $ from'wee-dom';

$('ref:element').before(function(i, html) {
    //Callback logic
});
```

## $el.children

Get unique direct children of each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection | -        |

### All Children

Without a filter all direct children will be returned.

```js
import $ from'wee-dom';

$('ref:element').children();
```

### Filtered

With a filter, only matching children will be returned.

```js
import $ from'wee-dom';

$('ref:element').children('li');
```

The response excludes text and comment nodes.

## $el.clone

Clone each matching selection

```js
import $ from'wee-dom';

$('ref.element').clone();
```

## $el.closest

Get unique closest ancestors of each matching selection

| Variable | Type                    | Default | Description       | Required |
|----------|-------------------------|---------|-------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection  | ✔        |
| context  | [selection](#selection) | -       | Context selection | -        |

```html
<div class="js-nav">
	<a class="js-link-account">Your Account</a>
</div>
<div class="nav">
	<a class="js-link-about">About Us</a>
</div>
```

```js|html
import $ from'wee-dom';

$('.js-link-about).closest('.js-nav');

 ---

<div class="js-nav">
	<a class="js-link-about">About Us</a>
</div>
```

This method traverses up the DOM for the closest match. It doesn't match descendants.

## $el.contains

Determine if any matching parent selection contains descendant selection

| Variable   | Type                    | Default | Description          | Required |
|------------|-------------------------|---------|----------------------|----------|
| descendant | [selection](#selection) | -       | Descendant selection | ✔        |

```js|js
import $ from'wee-dom';

$('ref:element').contains('.descendant');

---

true
```

## $el.contents

Get unique content of each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| parent   | [selection](#selection) | -       | Parent selection | ✔        |

```js
import $ from'wee-dom';

$('ref:element').contents();
```

The response includes text and comment nodes.

## $el.css

Get CSS value of first matching selection or set value of each matching selection

| Variable | Type           | Default | Description                                                          | Required |
|----------|----------------|---------|----------------------------------------------------------------------|----------|
| a        | string, object | -       | CSS property to get/set, or an object of properties and their values | ✔        |
| value    | string         | -       | Value to assign to property                                          | -        |

### Get Value

```js|js
import $ from'wee-dom';

$('ref:element').css('marginTop');

---

"0px"
```

### Set Single Value

```js
import $ from'wee-dom';

$('ref:element').css('marginTop', '5px');
```

### Set Multiple Values

```js
import $ from'wee-dom';

$('ref:element').css({
    marginTop: '5px',
    color: 'red'
});
```

## $el.data

Get data of first matching selection or set data of each matching selection

| Variable | Type           | Default | Description                               | Required |
|----------|----------------|---------|-------------------------------------------|----------|
| a        | string, object | -       | Data attribute to get or set or an object | ✔        |
| b        | string         | -       | Value to assign to data attribute         | -        |

### Get All

```html
<div data-ref="element" data-id="150"></div>
```

```js|js
import $ from'wee-dom';

$('ref:element').data();

---

{
    ref: "element",
    id: 150
}
```

### Get Single

```html
<div data-ref="element" data-id="150"></div>
```

```js|js
import $ from'wee-dom';

$('ref:element').data('id');

---

150
```

### Set Single

```js
import $ from'wee-dom';

$('ref:element').data('id', '250');
```

### Set Multiple

```js
import $ from'wee-dom';

$('ref:element').data({
    id: '350',
    active: 'true'
});
```

## $el.each

Execute function for each element in selection

| Variable | Type     | Default | Description                                | Required |
|----------|----------|---------|--------------------------------------------|----------|
| fn       | function | -       | Callback function                          | ✔        |
| options  | object   | -       | See options for [$each](/script/core#each) | -        |

```js
import $ from'wee-dom';

$('.js-element').each((el, i) => {
    // Callback logic
});
```

## $el.empty

Remove child nodes from each matching selection

```html
<div data-ref="bio">
	<h1>John Smith</h1>
	<p>Lorem ipsum dolor.</p>
</div>
```

```js
import $ from'wee-dom';

$('ref:bio').empty();
```

```html
<div data-ref="bio"></div>
```

## $el.eq

Get indexed node of matching selection

| Variable | Type                    | Default | Description       | Required |
|----------|-------------------------|---------|-------------------|----------|
| index    | number                  | -       | Element index     | ✔        |
| context  | [selection](#selection) | -       | Context selection | -        |

```html
<ul class="js-element">
	<li>List item 1</li>
	<li>List item 2</li>
	<li>List item 3</li>
|</ul>
```

```js|html
import $ from'wee-dom';

$('.js-element li').eq(1));

---

<li>List item 2</li>
```

### Negative Index

```js|html
import $ from'wee-dom';

$('.js-element li').eq(-1));

---

<li>List item 3</li>
```

## $el.filter

Return a filtered subset of elements from a matching selection

| Variable | Type                              | Default | Description                                | Required |
|----------|-----------------------------------|---------|--------------------------------------------|----------|
| filter   | function, [selection](#selection) | -       | Filter selection or callback               | ✔        |
| options  | object                            | -       | [Callback options](/script/core#callbacks) | -        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').filter('.filter');
```

### Function

The current index and element are injected into the callback. The scope of `this` is the element.

```html
<ul class="people">
	<li>John Doe</li>
	<li>John Smith</li>
	<li>Jane Doe</li>
	<li>Jane Smith</li>
</ul>
```

```js|js
import $ from'wee-dom';

$('.people li').filter((i, el) => {
    //Return elements containing 'Doe'return $text(el).indexOf('Doe') !== -1;
});

---

[<li>John Doe</li>, <li>Jane Doe</li>]
```

## $el.find

Get unique filtered descendants from each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection | ✔        |

```js
import $ from'wee-dom';

$('table').find('tr');
```

## $el.first

Get the first element of a matching selection

| Variable | Type                    | Default | Description       | Required |
|----------|-------------------------|---------|-------------------|----------|
| context  | [selection](#selection) | -       | Selection context | `        |

```js
import $ from'wee-dom';

const $first = $('ref:element').first();
```

## $el.hasClass

Determine if the matching selection has a class

| Variable  | Type   | Default | Description         | Required |
|-----------|--------|---------|---------------------|----------|
| className | string | -       | Specific class name | ✔        |

### Single

```html
<div class="hello" data-ref="element"></div>
```

```js|js
import $ from'wee-dom';

$('ref:element').hasClass('hello');
$('ref:element').hasClass('donuts');

---

true false
```

## $el.height ## (#height .doc__title)

Get or set the height of each matching selection

| Variable | Type                              | Default | Description                                          | Required |
|----------|-----------------------------------|---------|------------------------------------------------------|----------|
| value    | function, string, number, boolean | -       | Height to set, callback, or true to get outer height | ✔        |

### Get

```js|js
import $ from'wee-dom';

$('ref:element').height();

---

100
```

### Outer Height

```js|js
import $ from'wee-dom';

$('ref:element').height(true);

---

120
```

The value returned is a unitless pixel value.

### Set

```js
import $ from'wee-dom';

$('ref:element').height('10rem');
```

### Function

The current index and height are injected into the callback. The scope of `this` is the element.

```html
<div data-ref="example" style="height: 100px;"></div>
```

```js
import $ from'wee-dom';

$('ref:example').height((i, height) => {
    // Increase the height of the element by 50pxreturn (height += 50) + 'px';
});
```

If no unit is provided pixels will be set.

## $el.hide

Hide each matching selection

Hide works by adding the `js-hide` class which applies `display: none !important;`

```js
import $ from'wee-dom';

$('ref:element').hide();
```

## $el.html

Get inner HTML of first selection or set each matching selection's HTML

| Variable | Type             | Default | Description             | Required |
|----------|------------------|---------|-------------------------|----------|
| value    | function, string | -       | HTML to set or callback | ✔        |

```html
<div data-ref="element">
	<h1>Heading</h1>
</div>
```

### Get

```js|html
import $ from'wee-dom';

$('ref:element').html();

---

<h1>Heading</h1>
```

### Set

```js
import $ from'wee-dom';

$('ref:element').html('<h2>New Heading</h2>');
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```js
import $ from'wee-dom';

$('.js-element').html((el, i, html) => {
    // Return uppercase HTMLreturn html.toUpperCase();
});
```

## $el.index

Get the zero-based index of a matching selection relative to it's siblings

```html
<ul>
	<li></li>
	<li></li>
	<li class="js-last"></li>
</ul>
```

```js|js
import $ from'wee-dom';

$('.js-last).index();

---

2
```

## $el.insertAfter

Insert each matching source selection element after each matching target selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| target   | [selection](#selection) | -       | Target selection | ✔        |

```js
import $ from'wee-dom';

$('ref:element).insertAfter('.js-element');
```

## $el.insertBefore

Insert each matching source selection element before each matching target selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| target   | [selection](#selection) | -       | Target selection | ✔        |

```js
import $ from'wee-dom';

$('ref:element).insertBefore('.js-element');
```

## $el.is

Determine if at least one matching selection matches a specified criteria

| Variable | Type                              | Default | Description                                | Required |
|----------|-----------------------------------|---------|--------------------------------------------|----------|
| filter   | function, [selection](#selection) | -       | Filter selection or callback               | ✔        |
| options  | object                            | -       | [Callback options](/script/core#callbacks) | -        |

### Selection


```html
<div class="js-element"></div>
```

```js|js
import $ from'wee-dom';

$('.js-element').is('div');

---

true
```

### Function

```html
<ul class="names">
	<li>John Doe</li>
	<li data-hidden="true">Jane Doe</li>
	<li>John Smith</li><li>Jane Smith</li>
</ul>
```

```js|js
import $ from'wee-dom';

$('.names li').is((i, el) => {
    // Check if data-hidden is set to truereturn $(el).is('hidden') === 'true';
});

---

true
```

## $el.last

Get the last element of a matching selection

| Variable | Type                    | Default | Description       | Required |
|----------|-------------------------|---------|-------------------|----------|
| context  | [selection](#selection) | -       | Context selection | -        |

```html
<ul class="names">
	<li>John Doe</li>
	<li>John Smith</li>
	<li>Jane Doe</li>
	<li>Jane Smith</li>
</ul>
```

```js|html
import $ from'wee-dom';

$('.names li').last();

---

<li>Jane Smith</li>
```

## $el.map

Translate items in selection into new array

| Variable | Type     | Default | Description                              | Required |
|----------|----------|---------|------------------------------------------|----------|
| fn       | function | -       | Callback function                        | ✔        |
| options  | object   | -       | See options for [$map](/script/core#map) | -        |

```html
<div class='js-selection'>Hello</div>
<div class='js-selection'>World</div>
```

```js|js
import $ from'wee-dom';

$('.js-selection').map((el) => {
    return el.textContent;
});

---

['Hello', 'World']
```

## $el.next

Get the unique next sibling of each matching selection

| Variable | Type                    | Default | Description                                | Required |
|----------|-------------------------|---------|--------------------------------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection                           |          |
| options  | object                  | -       | [Callback options](/script/core#callbacks) | -        |

### Simple

```js
import $ from'wee-dom';

$('ref:element').next();
```

### Filtered

```html
<ul>
	<li>John Doe</li>
	<li>John Smith</li>
	<li data-ref="name">Jane Doe</li>
	<li>Jane Smith</li>
</ul>
```

```js|html
import $ from'wee-dom';

$('ref:name').next();

---

<li>Jane Smith</li>
```

## $el.not

Returns elements not matching the filtered selection

| Variable | Type                              | Default | Description                                | Required |
|----------|-----------------------------------|---------|--------------------------------------------|----------|
| filter   | function, [selection](#selection) | -       | Filter selection or callback               | ✔        |
| options  | object                            | -       | [Callback options](/script/core#callbacks) | -        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').not('div');
```

### Function

The current index and element are injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
	<li>John Doe</li>
	<li data-hidden="true">Jane Doe</li>
	<li>John Smith</li><li>Jane Smith</li>
</ul>
```

```js|js
import $ from'wee-dom';

$('.names li').not((i, el) => {
    // Check if data-hidden is set to truereturn $(el).data('hidden') === true;
});

---

[<li>John Doe</li>, <li>John Smith</li>, <li>Jane Smith</li>]
```

## $el.offset

Get the offset position of a matching selection relative to the document

| Variable | Type   | Default | Description   | Required |
|----------|--------|---------|---------------|----------|
| value    | object | -       | Offset values | -        |

### Set

```js
import $ from'wee-dom';

$('ref:element').offset({
    top: 100,
    left: 20
});
```

### Get

```js|js
import $ from'wee-dom';

$('ref:element').offset();

---

{
    top: 520,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $el.parent

Get unique parent from each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection | -        |

### Selection Parent

```js
import $ from'wee-dom';

$('ref:element').parent();
```

### Filtered

Return selection parent only if it matches the filter.

```js
import $ from'wee-dom';

$('ref:element').parent('main');
```

## $el.parents

Get unique ancestors of each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection | -        |

```js
import $ from'wee-dom';

$('ref:element').parents();
```

## $el.position

Get the position of the first matching selection relative to its offset parent

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| target   | [selection](#selection) | -       | Target selection | ✔        |

```js|js
import $ from'wee-dom';

$('ref:element').position();

---

{
    top: 250,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $el.prepend

Prepend selection or markup before each matching selection

| Variable | Type                                      | Default | Description                                                    | Required |
|----------|-------------------------------------------|---------|----------------------------------------------------------------|----------|
| source   | function, [selection](#selection), string | -       | Source selection, callback, or HTML string                     | ✔        |
| options  | object                                    | -       | [Callback options](https://www.weepower.com/script/#functions) | -        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').prepend($('.js-element'));
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<h1 data-ref="listHeading">Names</h1>
<ul data-ref="list">
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

```js
import $ from'wee-dom';

$('ref:listHeading').prepend(() => {
    return $('ref:list').children().d + ' ';
});
```

```html
<h1 data-ref="listHeading">2 Names</h1>
<ul data-ref="list">
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

## $el.prev

Get the unique previous sibling of each matching selection

| Variable | Type                    | Default | Description                                | Required |
|----------|-------------------------|---------|--------------------------------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection                           |          |
| options  | object                  | -       | [Callback options](/script/core#callbacks) | -        |

### Simple

```js
import $ from'wee-dom';

$('ref:element').prev();
```

### Filtered

```html
<ul>
	<li>John Doe</li>
	<li>John Smith</li>
	<li data-ref="name">Jane Doe</li>
	<li>Jane Smith</li>
</ul>
```

```js|html
import $ from'wee-dom';

$('ref:name').prev();

---

<li>John Smith</li>
```

## $el.prop

Get property of first matching selection or set property of each matching selection

| Variable | Type             | Default | Description                         | Required |
|----------|------------------|---------|-------------------------------------|----------|
| a        | string, object   | -       | Property to get or set or an object | ✔        |
| b        | function, string | -       | Value to assign to property         | -        |

### Get

```js|js
import $ from'wee-dom';

$('ref:element').prop('checked');

---

true
```

### Single

```js
import $ from'wee-dom';

$('ref:element').prop('checked', true);
```

### Multiple

```js
import $ from'wee-dom';

$('ref:element').prop({
    checked: true,
    required: false
});
```

## $el.remove

Remove each matching selection from the document

| Variable | Type                    | Default | Description       | Required |
|----------|-------------------------|---------|-------------------|----------|
| context  | [selection](#selection) | -       | Context selection | -        |

```js
import $ from'wee-dom';

$('ref:element').remove();
```

## $el.removeAttr

Remove specified attribute of each matching selection

| Variable | Type   | Default | Description    | Required |
|----------|--------|---------|----------------|----------|
| name     | string | -       | Attribute name | ✔        |

```js
import $ from'wee-dom';

$('ref:element').removeAttr('title');
```

## $el.removeClass

Remove classes from each matching selection

| Variable | Type             | Default | Description                         | Required |
|----------|------------------|---------|-------------------------------------|----------|
| value    | function, string | -       | Class name(s) to remove or callback | ✔        |

### Single

```js
import $ from'wee-dom';

$('ref:element').removeClass('modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
import $ from'wee-dom';

$('ref:element')removeClass('modifier modifier2');
```

### Function

The current index and class value are injected into the callback. The scope of `this` is the element.

```js
import $ from'wee-dom';

$('ref:element')removeClass((i, className) => {
    // Remove an indexed classreturn className + i;
});
```

## $el.replaceWith

Replace each matching selection with selection or markup

| Variable | Type                                      | Default | Description                                | Required |
|----------|-------------------------------------------|---------|--------------------------------------------|----------|
| source   | function, [selection](#selection), string | -       | Source selection, callback, or HTML string | ✔        |

### Selection

```js
import $ from'wee-dom';

$('ref:element').replaceWith($('.js-element'));
```

### Markup

```js
import $ from'wee-dom';

$('ref:element').replaceWith('<span>Replacement element</span>');
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

```js|html
import $ from'wee-dom';

$('.names li').replaceWith((i, html) => {
    return"<li>The " + html + "</li>";
});

---

<ul class="names">
	<li>The Jane Doe</li>
	<li>The John Doe</li>
</ul>
```

## $el.reverse

Reverse order of selection results

```js
import $ from'wee-dom';

$('.js-element').reverse();
```

## $el.scrollLeft

Get or set the X scroll position of each matching selection

| Variable | Type    | Default | Description   | Required |
|----------|---------|---------|---------------|----------|
| value    | integer | -       | Left position | -        |

### Get Value

```js|js
import $ from'wee-dom';

$('ref:element').scrollLeft();

---

0
```

The value returned is a unitless pixel value.

### Set Value

```js
import $ from'wee-dom';

$('ref:element').scrollLeft(15);
```

Scroll position should be provided as unitless pixel value.

## $el.scrollTop

Get or set the Y scroll position of each matching selection

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| value    | integer | -       | Top position | -        |

```js|js
import $ from'wee-dom';

$('ref:element').scrollTop();

---

1560
```

The value returned is a unitless pixel value.

### Set Value

```js
import $ from'wee-dom';

$('body').scrollTop(15);
```

Scroll position should be provided as unitless pixel value.

## $el.serializeForm

Serialize input values from first matching form selection

| Variable | Type    | Default | Description     | Required |
|----------|---------|---------|-----------------|----------|
| json     | boolean | false   | Convert to JSON | -        |

### Standard

```js|js
import $ from'wee-dom';

$('ref:element').serializeForm();

---

"inputName=value&inputName2=value2"
```

###
JSON
 ### (.doc__label .doc__code__label)

```js|js
import $ from'wee-dom';

$('ref:element').serializeForm(true);

---

{
    "inputName": "value",
    "inputName2": "value2"
}
```

## $el.show

Show each matching selection

Show works by removing the `js-hide` class either set manually or through [$el.hide()](#hide).

```js
import $ from'wee-dom';

$('ref:element').show();
```

## $el.siblings

Get unique siblings of each matching selection

| Variable | Type                    | Default | Description      | Required |
|----------|-------------------------|---------|------------------|----------|
| filter   | [selection](#selection) | -       | Filter selection | ✔        |

```html
<p>Sibling paragraph</p>
<span>Sibling span</span>
<div data-ref="sibling">Target div.</div>
```

### All Siblings

Without a filter all siblings will be returned.

```js|js
import $ from'wee-dom';

$('ref:sibling').siblings();

---

[<p>Sibling paragraph</p>, <span>Sibling span</span>]
```

### Filtered

```js|js
import $ from'wee-dom';

$(ref:sibling).siblings('p');

---

[<p>Sibling paragraph</p>]
```

## $el.slice

Get subset of selection matches from specified range

| Variable | Type    | Default | Description    | Required |
|----------|---------|---------|----------------|----------|
| start    | integer | -       | Starting index | ✔        |
| end      | integer | -       | Ending index   | ✔        |

```js
import $ from'wee-dom';

$('li').slice(0, 3);
```

## $el.text

Get inner text of first selection or set each matching selection's text

| Variable | Type             | Default | Description             | Required |
|----------|------------------|---------|-------------------------|----------|
| value    | function, string | -       | Text to set or callback | ✔        |

```html
<div class="js-element">Inner text</div>
```

### Get

```js|js
import $ from'wee-dom';

$('.js-element').text();

---

"Inner text"
```

### Set

```js
import $ from'wee-dom';

$('.js-element').text('New text');
```

### Function

The current index and text are injected into the callback. The scope of `this` is the element.

```js
import $ from'wee-dom';

$('.js-element').text((el, i , text) => {
    // Return uppercase textreturn text.toUpperCase();
});
```

## $el.toArray

Cast selection to array

```js
import $ from'wee-dom';

$('.js-elements').toArray();
```

## $el.toggle

Toggle the display of each matching selection

Rotates calling the [hide]() and [show]() methods.

```js
import $ from'wee-dom';

$(ref:element').toggle();
```

## $el.toggleClass

Toggle adding and removing class(es) from the specified element

| Variable  | Type             | Default | Description               | Required |
|-----------|------------------|---------|---------------------------|----------|
| className | function, string | -       | Class name(s) or callback | ✔        |
| state     | boolean          | -       | Force add or remove       | -        |

### Single

```js
import $ from'wee-dom';

$('ref:element').toggleClass('modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
import $ from'wee-dom';

$('ref:element').toggleClass('modifier modifier2');
```

### Function

The current index, class value and state are injected into the callback. The scope of `this` is the element.

```js
import $ from'wee-dom';

$('.element').toggleClass((i, className, state) => {
    // Return the class intended for togglereturn className + (state === true ? '-on' : '-off);
});
```

## $el.val

Get value of first matching selection or set values of each matching selection

| Variable | Type             | Default | Description                      | Required |
|----------|------------------|---------|----------------------------------|----------|
| value    | function, string | -       | Class name(s) to add or callback | ✔        |

### Get

```js
import $ from'wee-dom';

$('ref:element').val();
```

### Set

```js
import $ from'wee-dom';

$('ref:element').val('123');
```

### Function

The current index and value are injected into the callback. The scope of `this` is the element.

```html
<input type="text"value="This is an ordinary sentence in an input field." data-ref="input">
```

```js
import $ from'wee-dom';

$('ref:input').val((i, value) => {
    // Check the length of the current value but don't change the valueif (value.length > 20) {
        alert('Getting long winded, aren\'t we?');
    }
    return value;
});
```

## $el.width

Get or set the width of each matching selection

| Variable | Type             | Default | Description              | Required |
|----------|------------------|---------|--------------------------|----------|
| value    | function, string | -       | Width to set or callback | ✔        |

### Get

```js
import $ from'wee-dom';

$('ref:element').width();
```

```js
100
```

The value returned is a unitless pixel value.

### Set

```js
import $ from'wee-dom';

$('ref:element').width('10rem');
```

### Function

The current index and width are injected into the callback. The scope of `this` is the element.

```html
<div data-ref="example" style="width: 100px;"></div>
```

```js
import $ from'wee-dom';

$('ref:example').width((i, width) => {
    // Increase the width of the element by 50pxreturn (width += 50) + 'px';
});
```

If no unit is provided pixels will be set.

## $el.wrap

Wrap markup around each matching selection

| Variable | Type             | Default | Description              | Required |
|----------|------------------|---------|--------------------------|----------|
| html     | function, string | -       | Wrapper HTML or callback | ✔        |

### Markup

```js
import $ from'wee-dom';

$('ref:element').wrap('<div class="wrapper"></div>');
```

### Function

The current index is injected into the callback. The scope of `this` is the element.

```html
<div class="library">
	<ul class="books programming">
		<li>JavaScript: The Definitive Guide</li>
		<li>Mastering Regular Expressions</li>
	</ul>
	<ul class="books technique">
		<li>Code Complete</li>
		<li>The Pragmatic Programmer</li>
	</ul>
</div>
```

```js
import $ from'wee-dom';

$('.books').wrap(function(i) {
    if ($(this).hasClass('programming')) {
        return'<div class="reference"></div>'
    } else {
        return'<div class="readers"></div>'
    }
});
```

```html
<div class="library">
	<div class="reference">
		<ul class="books programming">
			<li>JavaScript: The Definitive Guide</li>
			<li>Mastering Regular Expressions</li>
		</ul>
	</div>
	<div class="readers">
		<ul class="books technique">
			<li>Code Complete</li>
			<li>The Pragmatic Programmer</li>
		</ul>
	</div>
</div>
```

## $el.wrapInner

Wrap markup around the content of each matching selection

| Variable | Type             | Default | Description              | Required |
|----------|------------------|---------|--------------------------|----------|
| html     | function, string | -       | Wrapper HTML or callback | ✔        |

### Markup

```js
import $ from'wee-dom';

$('ref:element').wrapInner('<div class="wrapper"></div>);
```

### Function

The current index is injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
	<li class="boss">Jane Doe</li>
	<li>John Doe</li>
</ul>
```

```js|html
import $ from'wee-dom';

$('.names li').wrapInner(function(i) {
    // Wrap bosses in bold tagif ($(this).hasClass('boss')) {
        return'<b></b>';
    }
});

---

<ul class="names">
	<li class="boss"><b>Jane Doe</b></li>
	<li>John Doe</li>
</ul>
```
