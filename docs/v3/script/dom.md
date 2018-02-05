# DOM 

Wee makes modifying and extracting data from your markup easy with a robust set of DOM functions. We’ve only included what you need without the cruft. You can also chain your methods.

## $addClass

Add classes to each matching selection

|Variable|Type                                                          |Default |Description                     |Required|
|--------|--------------------------------------------------------------|--------|--------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection                |✔	   |
|value   |[function](https://www.weepower.com/script/#functions), string|-       |Class name(s) to add or callback|✔	   |

### Single

```js
Wee.$addClass('ref:element', 'modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
Wee.$addClass('ref:element', 'modifier modifier2');
```

### Function

The current index and class value are injected into the callback. The scope of `this` is the element.

```js
Wee.$addClass('ref:element', function(i, className) {
    // Add an indexed classreturn className + i;
});
```

Callbacks can also be in the format of 'controllerName:method'. The index argument is always 0-based.

## $after

Insert selection or markup after each matching selection

|Variable|Type                                                   |Default |Description                  |Required|
|--------|-------------------------------------------------------|--------|-----------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection             |✔|
|source  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback, or HTML string|✔|
|remove  |boolean                                                |false   |Remove target after insertion|-        |

### Selection

```js
Wee.$after('ref:element', Wee.$('.js-element'));
```

### Markup

```js
Wee.$after('ref:element', '<span>Injected notice</span>');
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<div data-name="John Smith">
	<h1 data-ref="bioName">Name</h1>
</div>
```

```js
Wee.$after('ref:bioName', function(i, html) {
    // Add the parent data-name as a paragraph after the matched elementreturn'<p>' + Wee.$data(Wee.$parent(this), 'name') + '</p>';
});
```

```html
<div data-name="John Smith">
	<h1 data-ref="bioName">Name</h1>
	<p>John Smith</p>
</div>
```

## $append

Append selection or markup after each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔	    |
|source  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback, or HTML string|✔|

### Selection

```js
Wee.$append('ref:element', Wee.$('.js-element'));
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
Wee.$append('ref:listHeading', function(i, html) {
    // Modify the heading to include the number of listed namesreturn' (' + Wee.$children(Wee.$next()).length + ')';
});
```

```html
<h1 data-ref="listHeading">Names (2)</h1>
<ul>
	<li>John Doe</li>
	<li>Jane Doe</li>
</ul>
```

## $attr

Get attribute of first matching selection or set attribute of each matching selection

|Variable|Type                                                          |Default |Description                         |Required|
|--------|--------------------------------------------------------------|--------|------------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection                    |✔       |
|a       |string, object                                                |-       |Attribute to get or set or an object|✔       |
|b       |[function](https://www.weepower.com/script/#functions), string|-       |Value to assign to attribute        |-       |

### Get

```js
Wee.$attr('ref:element', 'href');
```

"[https://www.weepower.com](https://www.weepower.com)"

### Single

```js
Wee.$attr('ref:element', 'href', 'https://www.weepower.com/start');
```

### Multiple

```js
Wee.$attr('ref:element', {
    href: 'https://developer.mozilla.org',
    target: '_blank'
});
```

## $before

Insert selection or markup before each matching selection

|Variable|Type                                                   |Default |Description                 |Required|
|--------|-------------------------------------------------------|--------|----------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|source  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback or HTML string|✔|
|remove  |boolean                                                |false   |Remove target after insertion|-      |

### Selection

```js
Wee.$before('ref:element', Wee.$('.js-element'));
```

### Markup

```js
Wee.$before('ref:element', '<span>Injected notice</span>');
```

### Function

```js
Wee.$before('ref:element', function(i, html) {
    // Callback logic
});
```

## $children

Get unique direct children of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|---------|
|parent  |[selection](https://www.weepower.com/script/#selection)|-       |Parent selection|✔        |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|-        |

### All Children

Without a filter all direct children will be returned.

```js
Wee.$children('ref:element');
```

### Filtered

With a filter, only matching children will be returned.

```js
Wee.$children('ref:element', 'li');
```

The response excludes text and comment nodes.

## $clone

Clone each matching selection

|Variable|Type                                                   |Default|Description      |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔	    |

```js
Wee.$clone('ref:element');
```

## $closest

Get unique closest ancestors of each matching selection

|Variable|Type                                                   |Default |Description      |Required|
|--------|-------------------------------------------------------|--------|-----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection |✔       |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection |✔       |
|context |[selection](https://www.weepower.com/script/#selection)|-       |Context selection|-       |

```html
<div class="nav">
	<a class="link--account">Your Account</a>
</div>
<div class="nav">
	<a class="link--about">About Us</a>
</div>
```

```js
Wee.$closest('.link--about', '.nav');
```

```html
<div class="nav">
	<a class="link--about">About Us</a>
</div>
```

This method traverses up the DOM for the closest match. It doesn't match descendants.

## $contain

Determine if any matching parent selection contains descendant selection

|Variable  |Type                                                   |Default |Description         |Required|
|----------|-------------------------------------------------------|--------|--------------------|--------|
|parent    |[selection](https://www.weepower.com/script/#selection)|-       |Parent selection    |✔       |
|descendant|[selection](https://www.weepower.com/script/#selection)|-       |Descendant selection|✔       |

```js
Wee.$contains('ref:element', '.descendant');
```

```js
true
```

## $contents

Get unique content of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|parent  |[selection](https://www.weepower.com/script/#selection)|-       |Parent selection|✔       |

```js
Wee.$contents('ref:element');
```

The response includes text and comment nodes.

## $css

Get CSS value of first matching selection or set value of each matching selection

|Variable|Type                                                   |Default |Description                        |Required|
|--------|-------------------------------------------------------|--------|-----------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection                   |✔       |
|a       |string, object                                         |-       |Property to get or set or an object|✔       |
|b       |string                                                 |-       |Value to assign to property        |-       |

### Get Value

```js
Wee.$css('ref:element', 'marginTop');
```

```js
"0px"
```

### Set Single Value

```js
Wee.$css('ref:element', 'marginTop', '5px');
```

### Set Multiple Values

```js
Wee.$css('ref:element', {
    marginTop: '5px',
    color: 'red'
});
```

## $data

Get data of first matching selection or set data of each matching selection

|Variable|Type                                                   |Default |Description                              |Required|
|--------|-------------------------------------------------------|--------|-----------------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection                         |✔       |
|a       |string, object                                         |-       |Data attribute to get or set or an object|✔       |
|b       |string                                                 |-       |Value to assign to data attribute        |-       |

### Get All

```html
<div data-ref="element" data-id="150"></div>
```

```js
Wee.$data('ref:element');
```

```js
{
    ref: "element",
    id: 150
}
```

### Get Single

```html
<div data-ref="element" data-id="150"></div>
```

```js
Wee.$data('ref:element', 'id');
```

```js
150
```

### Set Single

```js
Wee.$data('ref:element', 'id', '250');;
```

### Set Multiple

```js
Wee.$data('ref:element', {
    id: '350',
    active: 'true'
});
```

## $empty

Remove child nodes from each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔	    |

```html
<div data-ref="bio">
	<h1>John Smith</h1>
	<p>Lorem ipsum dolor.</p>
</div>
```

```js
Wee.$empty('ref:bio');
```

```html
<div data-ref="bio"></div>
```

## $eq

Get indexed node of matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|index   |number                                                 |-       |Element index   |✔		|
|context |[selection](https://www.weepower.com/script/#selection)|-|Context selection||

```html
<ul class="js-element">
	<li>List item 1</li>
	<li>List item 2</li>
	<li>List item 3</li>
</ul>
```

```js
Wee.$eq('.js-element li', 1);
```

```html
<li>List item 2</li>
```

### Negative Index

```js
Wee.$eq('.js-element li', -1);
```

```html
<li>List item 3</li>
```

## $filter

Return a filtered subset of elements from a matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|filter  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection)|-|Filter selection or callback|✔	|
|options |object                                                 |-       |[Callback options](https://www.weepower.com/script/#functions)|-|

### Selection

```js
Wee.$filter('ref:element', '.filter');
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

```js
Wee.$filter('.people li', function(i, el) {
    // Return elements containing 'Doe'return Wee.$text(el).indexOf('Doe') !== -1;
});
```

```html
[<li>John Doe</li>, <li>Jane Doe</li>]
```

## $find

Get unique filtered descendants from each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|parent  |[selection](https://www.weepower.com/script/#selection)|-       |Parent selection|✔       |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|✔       |

```js
Wee.$find('table', 'tr');
```

## $first

Get the first element of a matching selection

|Variable|Type                                                   |Default |Description      |Required|
|--------|-------------------------------------------------------|--------|-----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection |✔       |
|context |[selection](https://www.weepower.com/script/#selection)|-       |Selection context|-       |

Works the same as [Wee.$()](https://www.weepower.com/script/dom#core) but only returns the first result from the result set.

```js
var $first = Wee.$first('ref:element');
```

## $hasClass

Determine if the matching selection has a class

|Variable |Type                                                   |Default |Description        |Required|
|---------|-------------------------------------------------------|--------|-------------------|--------|
|target   |[selection](https://www.weepower.com/script/#selection)|-       |Target selection   |✔       |
|className|string                                                 |-       |Specific class name|✔       |

### Single

```html
<div class="hello" data-ref="element"></div>
```

```js
$('ref:element').hasClass('hello');
$('ref:element').hasClass('donuts');
```

```js
truefalse
```

## $height

Get or set the height of each matching selection

|Variable|Type                                                                           |Default |Description     |Required|
|--------|-------------------------------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)                        |-       |Target selection|✔       |
|value   |[function](https://www.weepower.com/script/#functions), string, number, boolean|-       |Height to set, callback, or true to get outer height|✔|

### Get

```js
Wee.$height('ref:element');
```

```js
100
```

### Outer Height

```js
Wee.$height('ref:element', true);
```

```js
120
```

The value returned is a unitless pixel value.

### Set

```js
Wee.$height('ref:element', '10rem');
```

### Function

The current index and height are injected into the callback. The scope of `this` is the element.

```html
<div data-ref="example" style="height: 100px;"></div>
```

```js
Wee.$height('ref:example', function(i, height) {
    // Increase the height of the element by 50pxreturn (height += 50) + 'px';
});
```

If no unit is provided pixels will be set.

## $hide

Hide each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔		|

Hide works by adding the `js-hide` class which applies `display: none !important;`

```js
Wee.$hide('ref:element');
```

## $html

Get inner HTML of first selection or set each matching selection's HTML

|Variable|Type                                                          |Default |Description            |Required|
|--------|--------------------------------------------------------------|--------|-----------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection       |✔       |
|value   |[function](https://www.weepower.com/script/#functions), string|-       |HTML to set or callback|✔       |

```html
<div data-ref="element">
	<h1>Heading</h1>
</div>
```

### Get

```js
Wee.$html('ref:element');
```

```html
"<h1>Heading</h1>"
```

### Set

```js
Wee.$html('ref:element', '<h2>New Heading</h2>');
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```js
Wee.$html('.js-element', function(el, i, html) {
    // Return uppercase HTMLreturn html.toUpperCase();
});
```

## $index

Get the zero-based index of a matching selection relative to it's siblings

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔		|

```html
<ul>
	<li></li>
	<li></li>
	<li class="js-last"></li>
</ul>
```

```js
Wee.$index('.js-last');
```

```js
2
```

## $insertAfter

Insert each matching source selection element after each matching target selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|source  |[selection](https://www.weepower.com/script/#selection)|-       |Source selection|✔       |
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |

```js
Wee.$insertAfter('ref:element', '.js-element');
```

## $insertBefore

Insert each matching source selection element before each matching target selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|source  |[selection](https://www.weepower.com/script/#selection)|-       |Source selection|✔       |
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |

```js
Wee.$insertBefore('ref:element', '.js-element');
```

## $is

Determine if at least one matching selection matches a specified criteria

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|filter  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection)|-|Filter selection or callback|✔|
|options |object                                                 |-       |[Callback options](https://www.weepower.com/script/#functions)|-|

### Selection

```html
<div class="js-element"></div>
```

```js
Wee.$is('.js-element', 'div');
```

```js
true
```

### Function

```html
<ul class="names">
	<li>John Doe</li>
	<li data-hidden="true">Jane Doe</li>
	<li>John Smith</li>
	<li>Jane Smith</li>
</ul>
```

```js
Wee.$is('.names li', function(i, el) {
    // Check if data-hidden is set to truereturn Wee.$data(el, 'hidden') === 'true';
});
```

```js
true
```

## $last

Get the last element of a matching selection

|Variable|Type                                                   |Default |Description      |Required|
|--------|-------------------------------------------------------|--------|-----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection |✔       |
|context |[selection](https://www.weepower.com/script/#selection)|-       |Context selection|-       |

Works the same as [Wee.$()](https://www.weepower.com/script/dom#core) but only returns the last result from the result set.

```html
<ul class="names">
    <li>John Doe</li>
    <li>John Smith</li>
    <li>Jane Doe</li>
    <li>Jane Smith</li>
</ul>
```

```js
Wee.$last('.names li');
```

```html
<li>Jane Smith</li>
```

## $next

Get the unique next sibling of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔|
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|-|
|options |object                                                 |-       |[Callback option](https://www.weepower.com/script/#functions)|-|

### Simple

```js
Wee.$next();
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

```js
Wee.$next('ref:name');
```

```html
<li>Jane Smith</li>
```

## $not

Returns elements not matching the filtered selection

|Variable|Type                                                   |Default  |Description     |Required|
|--------|-------------------------------------------------------|---------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-        |Target selection|✔|
|filter  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection)|-|Filter selection or callback|✔|
|options |object                                                 |-        |[Callback options](https://www.weepower.com/script/#functions)|-|

### Selection

```js
Wee.$not('ref:element', 'div');
```

### Function

The current index and element are injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
    <li>John Doe</li>
    <li data-hidden="true">Jane Doe</li>
    <li>John Smith</li>
    <li>Jane Smith</li>
</ul>
```

```js
Wee.$not('.names li', function(i, el) {
    // Check if data-hidden is set to truereturn Wee.$data(el, 'hidden') === true;
});
```

```js
[<li>John Doe</li>, <li>John Smith</li>, <li>Jane Smith</li>]
```

## $offset

Get the offset position of a matching selection relative to the document

|Variable|Type                                                   |Default|Description     |Required|
|--------|-------------------------------------------------------|-------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-      |Target selection|✔       |
|value   |object                                                 |-      |Offset values   |-       |

### Set

```js
Wee.$offset('ref:element', {
    top: 100,
    left: 20
});
```

### Get

```js
Wee.$offset('ref:element');
```

```js
{
    top: 520,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $parent

Get unique parent from each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|child   |[selection](https://www.weepower.com/script/#selection)|-       |Child selection |✔       |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|-       |

### Selection Parent

```js
Wee.$parent('ref:element');
```

### Filtered

Return selection parent only if it matches the filter.

```js
Wee.$parent('ref:element', 'main');
```

## $parents

Get unique ancestors of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|child   |[selection](https://www.weepower.com/script/#selection)|-       |Child selection |✔       |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|-       |

```js
Wee.$parents('ref:element');
```

## $position

Get the position of the first matching selection relative to its offset parent

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔		|

```js
Wee.$position('ref:element');
```

```js
{
    top: 250,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $prepend

Prepend selection or markup before each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|source  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback, or HTML string|✔|
|options |object                                                 |-       |[Callback options](https://www.weepower.com/script/#functions)|-|

### Selection

```js
Wee.$prepend('ref:element', Wee.$('.js-element'));
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
Wee.$prepend('ref:listHeading', function() {
    return Wee.$children('ref:list').length + ' ';
});
```

```js
(<h1 data-ref="listHeading">2 Names</h1><ul data-ref="list"><li>John Doe</li><li>Jane Doe</li></ul>)
```

## $prev

Get the unique previous sibling of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|-       |
|options |object                                                 |-       |[Callback options](https://www.weepower.com/script/#functions)|-|

### Simple

```js
Wee.$prev();
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

```js
Wee.$prev('ref:name');
```

```html
<li>John Smith</li>
```

## $prop

Get property of first matching selection or set property of each matching selection

|Variable|Type                                                          |Default |Description                        |Required|
|--------|--------------------------------------------------------------|--------|-----------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection                   |✔       |
|a       |string, object                                                |-       |Property to get or set or an object|✔       |
|b       |[function](https://www.weepower.com/script/#functions), string|-       |Value to assign to property        |-       |

### Get

```js
Wee.$prop('ref:element', 'checked');
```

```js
true
```

### Single

```js
Wee.$prop('ref:element', 'checked', true);
```

### Multiple

```js
Wee.$prop('ref:element', {
    checked: true,
    required: false
});
```

## $remove

Remove each matching selection from the document

|Variable|Type                                                  |Default |Description      |Required|
|--------|------------------------------------------------------|--------|-----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-      |Target selection |✔       |
|context |[selection](https://www.weepower.com/script/#selection)|-      |Context selection|-       |

```js
Wee.$remove('ref:element');
```

## $removeAttr

Remove specified attribute of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔		|
|name    |string                                                 |-       |Attribute name  |✔		|

```js
Wee.$removeAttr('ref:element', 'title');
```

## $removeClass

Remove classes from each matching selection

|Variable|Type                                                           |Default |Description                        |Required|
|--------|---------------------------------------------------------------|--------|-----------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)        |-       |Target selection                   |✔       |
|value   |[function](https://www.weepower.com/script/#functions), string |-       |Class name(s) to remove or callback|✔       |

### Single

```js
Wee.$removeClass('ref:element', 'modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
Wee.$removeClass('ref:element', 'modifier modifier2');
```

### Function

The current index and class value are injected into the callback. The scope of `this` is the element.

```js
Wee.$removeClass('ref:element', function(i, className) {
    // Remove an indexed classreturn className + i;
});
```

## $replaceWith

Replace each matching selection with selection or markup

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|source  |[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback, or HTML string|✔|

### Selection

```js
Wee.$replaceWith('ref:element', Wee.$('.js-element'));
```

### Markup

```js
Wee.$replaceWith('ref:element', '<span>Replacement element</span>');
```

### Function

The current index and HTML are injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
    <li>John Doe</li>
    <li>Jane Doe</li>
</ul>
```

```js
Wee.$replaceWith('.names li', function(i, html) {
    return"<li>The " + html + "</li>";
});
```

```html
<ul class="names">
    <li>The Jane Doe</li>
    <li>The John Doe</li>
</ul>
```

## $scrollLeft

Get or set the X scroll position of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|window  |Target Selection|-       |
|value   |integer                                                |-       |Left position   |-       |

### Get Value

```js
Wee.$scrollLeft();
```

```js
0
```

The value returned is a unitless pixel value.

### Set Value

```js
Wee.$scrollLeft(15);
```

Scroll position should be provided as unitless pixel value.

## $scrollTop

Get or set the Y scroll position of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|window  |Target selection|-       |
|value   |integer                                                |-       |Top position    |-       |

```js
Wee.$scrollTop();
```

```js
1560
```

The value returned is a unitless pixel value.

### Set Value

```js
Wee.$scrollTop('body', 15);
```

Scroll position should be provided as unitless pixel value.

## $serializeForm

Serialize input values from first matching form selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|select  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|json    |boolean                                                |false   |Convert to JSON |-       |

### Standard

```js
Wee.$serializeForm('ref:element');
```

```js
"inputName=value&inputName2=value2"
```

### JSON


```js
Wee.$serializeForm('ref:element', true);
```

```js
{
    "inputName": "value",
    "inputName2": "value2"
}
```

## $show

Show each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |

Show works by removing the `js-hide` class either set manually or through [Wee.$hide()](https://www.weepower.com/script/dom#hide).

```js
Wee.$show('ref:element');
```

## $siblings

Get unique siblings of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       | 
|filter  |[selection](https://www.weepower.com/script/#selection)|-       |Filter selection|✔       |

```html
<p>Sibling paragraph</p>
<span>Sibling span</span>
<div data-ref="sibling">Target div.</div>
```

### All Siblings

Without a filter all siblings will be returned.

```js
Wee.$siblings('ref:sibling');
```

```js
[<p>Sibling paragraph</p>, <span>Sibling span</span>]
```

### Filtered

```js
Wee.$siblings('ref:sibling', 'p');
```

```js
[<p>Sibling paragraph</p>]
```

## $slice

Get subset of selection matches from specified range

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔       |
|start   |integer                                                |-       |Starting index  |✔       |
|end     |integer                                                |-       |Ending index    |✔       |

```js
Wee.$slice('li', 0, 3);
```

## $text

Get inner text of first selection or set each matching selection's text

|Variable|Type                                                          |Default |Description            |Required|
|--------|--------------------------------------------------------------|--------|-----------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection|      |✔       |
|value   |[function](https://www.weepower.com/script/#functions), string|-       |Text to set or callback|✔       |

```html
<div class="js-element">Inner text</div>
```

### Get

```js
Wee.$text('.js-element');
```

```js
"Inner text"
```

### Set

```js
Wee.$text('.js-element', 'New text');
```

### Function

The current index and text are injected into the callback. The scope of `this` is the element.

```js
Wee.$text('.js-element', function(el, i, text) {
    // Return uppercase textreturn text.toUpperCase();
});
```

## $toggle

Toggle the display of each matching selection

|Variable|Type                                                   |Default |Description     |Required|
|--------|-------------------------------------------------------|--------|----------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)|-       |Target selection|✔		|

Rotates calling the [hide](https://www.weepower.com/script/dom#hide) and [show](https://www.weepower.com/script/dom#show) methods.

```js
Wee.$toggle('ref:element');
```

## $toggleClass ##

Toggle adding and removing class(es) from the specified element

|Variable |Type                                                           |Default |Description              |Required|
|---------|---------------------------------------------------------------|--------|-------------------------|--------|
|target   |[selection](https://www.weepower.com/script/#selection)        |-       |Target selection         |✔       |
|className|[function](https://www.weepower.com/script/#functions),  string|-       |Class name(s) or callback|✔       |
|state    |boolean                                                        |-       |Force add or remove      |-       |

### Single

```js
Wee.$toggleClass('ref:element', 'modifier');
```

### Multiple

Separate multiple class names with spaces.

```js
Wee.$toggleClass('ref:element', 'modifier modifier2');
```

### Function

The current index, class value and state are injected into the callback. The scope of `this` is the element.

```js
Wee.$toggleClass('.element', function(i, className, state) {
    // Return the class intended for togglereturn className + (state === true ? '-on' : '-off');
});
```

## $val

Get value of first matching selection or set values of each matching selection

|Variable|Type                                                           |Default |Description                     |Required|
|--------|---------------------------------------------------------------|--------|--------------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)        |-       |Target selection                |✔       |
|value   |[function](https://www.weepower.com/script/#functions),  string|-       |Class name(s) to add or callback|✔       |

### Get

```js
Wee.$val('ref:element');
```

### Set

```js
Wee.$val('ref:element', '123');
```

### Function

```html
<input type="text" value="This is an ordinary sentence in an input field." data-ref="input">
```

```js
Wee.$val('ref:input', function(i, value) {
    // Check the length of the current value but don't change the valueif (value.length > 20) {
        alert('Getting long winded, aren\'t we?');
    }

    return value;
});
```

## $width

Get or set the width of each matching selection

|Variable|Type                                                          |Default |Description             |Required|
|--------|--------------------------------------------------------------|--------|------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection        |✔       |
|value   |[function](https://www.weepower.com/script/#functions), string|-       |Width to set or callback|✔       |

### Get

```js
Wee.$width('ref:element');
```

```js
100
```

The value returned is a unitless pixel value.

### Set

```js
Wee.$width('ref:element', '10rem');
```

### Function

The current index and width are injected into the callback. The scope of `this` is the element.

```html
<div data-ref="example"style="width: 100px;"></div>
```

```js
Wee.$width('ref:example', function(i, width) {
    // Increase the width of the element by 50pxreturn (width += 50) + 'px';
});
```

If no unit is provided pixels will be set.

## $wrap

Wrap markup around each matching selection

|Variable|Type                                                          |Default |Description             |Required|
|--------|--------------------------------------------------------------|--------|------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection        |✔       |
|html    |[function](https://www.weepower.com/script/#functions), string|-       |Wrapper HTML or callback|✔       |

### Markup

```js
Wee.$wrap('ref:element', '<div class="wrapper"></div>');
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
Wee.$wrap('.books', function(i) {
    if (Wee.$hasClass($(this), 'programming')) {
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

## $wrapInner

Wrap markup around the content of each matching selection

|Variable|Type                                                          |Default |Description             |Required|
|--------|--------------------------------------------------------------|--------|------------------------|--------|
|target  |[selection](https://www.weepower.com/script/#selection)       |-       |Target selection        |✔       |
|html    |[function](https://www.weepower.com/script/#functions), string|-       |Wrapper HTML or callback|✔       |

### Markup

```js
Wee.$wrapInner('ref:element', '<div class="wrapper"></div>');
```

### Function

The current index is injected into the callback. The scope of `this` is the element.

```html
<ul class="names">
    <li class="boss">Jane Doe</li>
    <li>John Doe</li><
/ul>
```

```js
Wee.$wrapInner('.names li', function(i) {
    // Wrap bosses in bold tagif (Wee.$hasClass($(this), 'boss')) {
        return'<b></b>';
    }
});
```

```html
<ul class="names">
    <li class="boss"><b>Jane Doe</b></li>
    <li>John Doe</li>
</ul>
```