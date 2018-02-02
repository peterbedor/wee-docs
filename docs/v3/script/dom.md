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

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|context|[selection](https://www.weepower.com/script/#selection)|-|Context selection||

Works the same as [Wee.$()](https://www.weepower.com/script/dom#core) but only returns the last result from the result set.

```
<ulclass="names"><li>John Doe</li><li>John Smith</li><li>Jane Doe</li><li>Jane Smith</li></ul>
```

```
Wee.$last('.names li');
```

```
<li>Jane Smith</li>
```

## $next ## (#next .doc__title)

Get the unique next sibling of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|filter|[selection](https://www.weepower.com/script/#selection)|-|Filter selection||
|options|object|-|[Callback options](https://www.weepower.com/script/#functions)||

### 
Simple
 ### (.doc__label .doc__code__label)

```
Wee.$next();
```

### 
Filtered
 ### (.doc__label .doc__code__label)

```
<ul><li>John Doe</li><li>John Smith</li><lidata-ref="name">Jane Doe</li><li>Jane Smith</li></ul>
```

```
Wee.$next('ref:name');
```

```
<li>Jane Smith</li>
```

## $not ## (#not .doc__title)

Returns elements not matching the filtered selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|filter|[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection)|-|Filter selection or callback|													✔											|
|options|object|-|[Callback options](https://www.weepower.com/script/#functions)||

### 
Selection
 ### (.doc__label .doc__code__label)

```
Wee.$not('ref:element', 'div');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and element are injected into the callback. The scope of `this` is the element.

```
<ulclass="names"><li>John Doe</li><lidata-hidden="true">Jane Doe</li><li>John Smith</li><li>Jane Smith</li></ul>
```

```
Wee.$not('.names li', function(i, el) {
    // Check if data-hidden is set to truereturn Wee.$data(el, 'hidden') === true;
});
```

```
[<li>John Doe</li>, <li>John Smith</li>, <li>Jane Smith</li>]
```

## $offset ## (#offset .doc__title)

Get the offset position of a matching selection relative to the document

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|value|object|-|Offset values||

### 
Set
 ### (.doc__label .doc__code__label)

```
Wee.$offset('ref:element', {
    top: 100,
    left: 20
});
```

### 
Get
 ### (.doc__label .doc__code__label)

```
Wee.$offset('ref:element');
```

```
{
    top: 520,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $parent ## (#parent .doc__title)

Get unique parent from each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|child|[selection](https://www.weepower.com/script/#selection)|-|Child selection|													✔											|
|filter|[selection](https://www.weepower.com/script/#selection)|-|Filter selection||

### 
Selection Parent
 ### (.doc__label .doc__code__label)

```
Wee.$parent('ref:element');
```

### 
Filtered
 ### (.doc__label .doc__code__label)

Return selection parent only if it matches the filter.

```
Wee.$parent('ref:element', 'main');
```

## $parents ## (#parents .doc__title)

Get unique ancestors of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|child|[selection](https://www.weepower.com/script/#selection)|-|Child selection|													✔											|
|filter|[selection](https://www.weepower.com/script/#selection)|-|Filter selection||

```
Wee.$parents('ref:element');
```

## $position ## (#position .doc__title)

Get the position of the first matching selection relative to its offset parent

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|

```
Wee.$position('ref:element');
```

```
{
    top: 250,
    left: 30
}
```

The object values are returned as unitless pixel values.

## $prepend ## (#prepend .doc__title)

Prepend selection or markup before each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|source|[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string|-|Source selection, callback, or HTML string|													✔											|
|options|object|-|[Callback options](https://www.weepower.com/script/#functions)||

### 
Selection
 ### (.doc__label .doc__code__label)

```
Wee.$prepend('ref:element', Wee.$('.js-element'));
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and HTML are injected into the callback. The scope of `this` is the element.

```
<h1data-ref="listHeading">Names</h1><uldata-ref="list"><li>John Doe</li><li>Jane Doe</li></ul>
```

```
Wee.$prepend('ref:listHeading', function() {
    return Wee.$children('ref:list').length + ' ';
});
```

```
(<h1data-ref="listHeading">2 Names</h1><uldata-ref="list"><li>John Doe</li><li>Jane Doe</li></ul>)
```

## $prev ## (#prev .doc__title)

Get the unique previous sibling of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|filter|[selection](https://www.weepower.com/script/#selection)|-|Filter selection||
|options|object|-|[Callback options](https://www.weepower.com/script/#functions)||

### 
Simple
 ### (.doc__label .doc__code__label)

```
Wee.$prev();
```

### 
Filtered
 ### (.doc__label .doc__code__label)

```
<ul><li>John Doe</li><li>John Smith</li><lidata-ref="name">Jane Doe</li><li>Jane Smith</li></ul>
```

```
Wee.$prev('ref:name');
```

```
<li>John Smith</li>
```

## $prop ## (#prop .doc__title)

Get property of first matching selection or set property of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|a|string, object|-|Property to get or set or an object|													✔											|
|b|[function](https://www.weepower.com/script/#functions), string|-|Value to assign to property||

### 
Get
 ### (.doc__label .doc__code__label)

```
Wee.$prop('ref:element', 'checked');
```

```
true
```

### 
Single
 ### (.doc__label .doc__code__label)

```
Wee.$prop('ref:element', 'checked', true);
```

### 
Multiple
 ### (.doc__label .doc__code__label)

```
Wee.$prop('ref:element', {
    checked: true,
    required: false
});
```

## $remove ## (#remove .doc__title)

Remove each matching selection from the document

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|context|[selection](https://www.weepower.com/script/#selection)|-|Context selection||

```
Wee.$remove('ref:element');
```

## $removeAttr ## (#removeattr .doc__title)

Remove specified attribute of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|name|string|-|Attribute name|													✔											|

```
Wee.$removeAttr('ref:element', 'title');
```

## $removeClass ## (#removeclass .doc__title)

Remove classes from each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|value|[function](https://www.weepower.com/script/#functions), string|-|Class name(s) to remove or callback|													✔											|

### 
Single
 ### (.doc__label .doc__code__label)

```
Wee.$removeClass('ref:element', 'modifier');
```

### 
Multiple
 ### (.doc__label .doc__code__label)

Separate multiple class names with spaces.

```
Wee.$removeClass('ref:element', 'modifier modifier2');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and class value are injected into the callback. The scope of `this` is the element.

```
Wee.$removeClass('ref:element', function(i, className) {
    // Remove an indexed classreturn className + i;
});
```

## $replaceWith ## (#replacewith .doc__title)

Replace each matching selection with selection or markup

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|source|[function](https://www.weepower.com/script/#functions), [selection](https://www.weepower.com/script/#selection), string||Source selection, callback, or HTML string|													✔											|

### 
Selection
 ### (.doc__label .doc__code__label)

```
Wee.$replaceWith('ref:element', Wee.$('.js-element'));
```

### 
Markup
 ### (.doc__label .doc__code__label)

```
Wee.$replaceWith('ref:element', '<span>Replacement element</span>');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and HTML are injected into the callback. The scope of `this` is the element.

```
<ulclass="names"><li>John Doe</li><li>Jane Doe</li></ul>
```

```
Wee.$replaceWith('.names li', function(i, html) {
    return"<li>The " + html + "</li>";
});
```

```
<ulclass="names"><li>The Jane Doe</li><li>The John Doe</li></ul>
```

## $scrollLeft ## (#scrollleft .doc__title)

Get or set the X scroll position of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|window|Target Selection||
|value|integer|-|Left position||

### 
Get Value
 ### (.doc__label .doc__code__label)

```
Wee.$scrollLeft();
```

```
0
```

The value returned is a unitless pixel value.

### 
Set Value
 ### (.doc__label .doc__code__label)

```
Wee.$scrollLeft(15);
```

Scroll position should be provided as unitless pixel value.

## $scrollTop ## (#scrolltop .doc__title)

Get or set the Y scroll position of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|window|Target selection||
|value|integer|-|Top position||

```
Wee.$scrollTop();
```

```
1560
```

The value returned is a unitless pixel value.

### 
Set Value
 ### (.doc__label .doc__code__label)

```
Wee.$scrollTop('body', 15);
```

Scroll position should be provided as unitless pixel value.

## $serializeForm ## (#serializeform .doc__title)

Serialize input values from first matching form selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|select|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|json|boolean|false|Convert to JSON||

### 
Standard
 ### (.doc__label .doc__code__label)

```
Wee.$serializeForm('ref:element');
```

```
"inputName=value&inputName2=value2"
```

### 
JSON
 ### (.doc__label .doc__code__label)

```
Wee.$serializeForm('ref:element', true);
```

```
{
    "inputName": "value",
    "inputName2": "value2"
}
```

## $show ## (#show .doc__title)

Show each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|

Show works by removing the `js-hide` class either set manually or through [Wee.$hide()](https://www.weepower.com/script/dom#hide).

```
Wee.$show('ref:element');
```

## $siblings ## (#siblings .doc__title)

Get unique siblings of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|filter|[selection](https://www.weepower.com/script/#selection)|-|Filter selection|													✔											|

```
<p>Sibling paragraph</p><span>Sibling span</span><divdata-ref="sibling">Target div.</div>
```

### 
All Siblings
 ### (.doc__label .doc__code__label)

Without a filter all siblings will be returned.

```
Wee.$siblings('ref:sibling');
```

```
[<p>Sibling paragraph</p>, <span>Sibling span</span>]
```

### 
Filtered
 ### (.doc__label .doc__code__label)

```
Wee.$siblings('ref:sibling', 'p');
```

```
[<p>Sibling paragraph</p>]
```

## $slice ## (#slice .doc__title)

Get subset of selection matches from specified range

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|start|integer|-|Starting index|													✔											|
|end|integer|-|Ending index|													✔											|

```
Wee.$slice('li', 0, 3);
```

## $text ## (#text .doc__title)

Get inner text of first selection or set each matching selection's text

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|value|[function](https://www.weepower.com/script/#functions), string|-|Text to set or callback|													✔											|

```
<divclass="js-element">Inner text</div>
```

### 
Get
 ### (.doc__label .doc__code__label)

```
Wee.$text('.js-element');
```

```
"Inner text"
```

### 
Set
 ### (.doc__label .doc__code__label)

```
Wee.$text('.js-element', 'New text');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and text are injected into the callback. The scope of `this` is the element.

```
Wee.$text('.js-element', function(el, i, text) {
    // Return uppercase textreturn text.toUpperCase();
});
```

## $toggle ## (#toggle .doc__title)

Toggle the display of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|

Rotates calling the [hide](https://www.weepower.com/script/dom#hide) and [show](https://www.weepower.com/script/dom#show) methods.

```
Wee.$toggle('ref:element');
```

## $toggleClass ## (#toggleclass .doc__title)

Toggle adding and removing class(es) from the specified element

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|className|[function](https://www.weepower.com/script/#functions),  string|-|Class name(s) or callback|													✔											|
|state|boolean|-|Force add or remove||

### 
Single
 ### (.doc__label .doc__code__label)

```
Wee.$toggleClass('ref:element', 'modifier');
```

### 
Multiple
 ### (.doc__label .doc__code__label)

Separate multiple class names with spaces.

```
Wee.$toggleClass('ref:element', 'modifier modifier2');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index, class value and state are injected into the callback. The scope of `this` is the element.

```
Wee.$toggleClass('.element', function(i, className, state) {
    // Return the class intended for togglereturn className + (state === true ? '-on' : '-off');
});
```

## $val ## (#val .doc__title)

Get value of first matching selection or set values of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|value|[function](https://www.weepower.com/script/#functions),  string|-|Class name(s) to add or callback|													✔											|

### 
Get
 ### (.doc__label .doc__code__label)

```
Wee.$val('ref:element');
```

### 
Set
 ### (.doc__label .doc__code__label)

```
Wee.$val('ref:element', '123');
```

### 
Function
 ### (.doc__label .doc__code__label)

```
<inputtype="text"value="This is an ordinary sentence in an input field."data-ref="input">
```

```
Wee.$val('ref:input', function(i, value) {
    // Check the length of the current value but don't change the valueif (value.length > 20) {
        alert('Getting long winded, aren\'t we?');
    }

    return value;
});
```

## $width ## (#width .doc__title)

Get or set the width of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|value|[function](https://www.weepower.com/script/#functions), string||Width to set or callback|													✔											|

### 
Get
 ### (.doc__label .doc__code__label)

```
Wee.$width('ref:element');
```

```
100
```

The value returned is a unitless pixel value.

### 
Set
 ### (.doc__label .doc__code__label)

```
Wee.$width('ref:element', '10rem');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index and width are injected into the callback. The scope of `this` is the element.

```
<divdata-ref="example"style="width: 100px;"></div>
```

```
Wee.$width('ref:example', function(i, width) {
    // Increase the width of the element by 50pxreturn (width += 50) + 'px';
});
```

If no unit is provided pixels will be set.

## $wrap ## (#wrap .doc__title)

Wrap markup around each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|html|[function](https://www.weepower.com/script/#functions), string|-|Wrapper HTML or callback|													✔											|

### 
Markup
 ### (.doc__label .doc__code__label)

```
Wee.$wrap('ref:element', '<div class="wrapper"></div>');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index is injected into the callback. The scope of `this` is the element.

```
<divclass="library"><ulclass="books programming"><li>JavaScript: The Definitive Guide</li><li>Mastering Regular Expressions</li></ul><ulclass="books technique"><li>Code Complete</li><li>The Pragmatic Programmer</li></ul></div>
```

```
Wee.$wrap('.books', function(i) {
    if (Wee.$hasClass($(this), 'programming')) {
        return'<div class="reference"></div>'
    } else {
        return'<div class="readers"></div>'
    }
});
```

```
<divclass="library"><divclass="reference"><ulclass="books programming"><li>JavaScript: The Definitive Guide</li><li>Mastering Regular Expressions</li></ul></div><divclass="readers"><ulclass="books technique"><li>Code Complete</li><li>The Pragmatic Programmer</li></ul></div></div>
```

## $wrapInner ## (#wrapinner .doc__title)

Wrap markup around the content of each matching selection

|Variable|Type|Default|Description|Required|
|--------|--------|--------|--------|--------|
|target|[selection](https://www.weepower.com/script/#selection)|-|Target selection|													✔											|
|html|[function](https://www.weepower.com/script/#functions), string|-|Wrapper HTML or callback|													✔											|

### 
Markup
 ### (.doc__label .doc__code__label)

```
Wee.$wrapInner('ref:element', '<div class="wrapper"></div>');
```

### 
Function
 ### (.doc__label .doc__code__label)

The current index is injected into the callback. The scope of `this` is the element.

```
<ulclass="names"><liclass="boss">Jane Doe</li><li>John Doe</li></ul>
```

```
Wee.$wrapInner('.names li', function(i) {
    // Wrap bosses in bold tagif (Wee.$hasClass($(this), 'boss')) {
        return'<b></b>';
    }
});
```

```
<ulclass="names"><liclass="boss"><b>Jane Doe</b></li><li>John Doe</li></ul>
```