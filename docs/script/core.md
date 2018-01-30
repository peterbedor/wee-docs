# Core

Foundation of utilities and helpers

## Callbacks

Options for callback functions

Functions passed in as parameters to any Wee API method are evaluated in the same fashion. Usually, an options object will be provided for these Wee API methods that take a callback function that can have the following properties:

| Variable | Type   | Default | Description                                            | Required |
|----------|--------|---------|--------------------------------------------------------|----------|
| args     | array  | -       | Arguments to be passed into value if value is function |    -      |
| scope    | object | -       | Scope assigned to value if value is a function         |     -     |

## $chain

Register a new chainable method for [Wee selections](/script/dom#selection)

```js
import { $chain } from'core/chain';
import $ from'wee-dom';

$chain('setId', function(id) {
    this.attr('id', id);

    returnthis;
});

$('.selection').setId('selection');
```

## $each ##

Execute function for each matching selection

| Variable | Type                               | Default | Description                                                | Required |
|----------|------------------------------------|---------|------------------------------------------------------------|----------|
| target   | [selection](/script/dom#selection) | -       | Target selection                                           | ✔        |
| fn       | function                           | -       | Callback function                                          | ✔        |
| options  | object                             | -       | Object properties below and [Callback](#callbacks) options | -         |

### Options Object

| Variable | Type                               | Default  | Description                    | Required |
|----------|------------------------------------|----------|--------------------------------|----------|
| context  | [selection](/script/dom#selection) | document | Callback context               |    -      |
| reverse  | boolean                            | false    | Reverse the order of execution |     -     |

### Simple

```js
import { $each } from'core/dom';

$each('ref:element', (el, i) => {
    // Callback logic
});
```

### Advanced

```js
import { $each } from'core/dom';

$each('ref:element', (el, i) => {
    // Callback logic
}, {
    reverse: true,
    scope: this
});
```

The element and index are injected as the first two callback parameters.

## $env

Get current environment or set current environment against specified object

| Variable | Type   | Default | Description         | Required |
|----------|--------|---------|---------------------|----------|
| rules    | object | -       | Environmental rules |   -       |
| fallback | string | "local" | Default environment |    -      |

### Set

The key values can either be strings for a direct match or a functions for more complex evaluation. If a function is provided the response should be a boolean. If no match is found the default environment value is used.

```js|js
import { $env } from'core/core';

$env({
    prod: 'www.weepower.com',
    stage: 'stage.weepower.com'
});

---

'prod'
```


### Get

```js|js
import { $env } from'core/core';

$env();

---

'prod'
```

## $envSecure

Determine if the current environment is SSL encrypted

```js|js
import { $envSecure } from'core/core';

$envSecure();

---

true
```

## $equals

Compare two values for strict equality

| Variable | Type   | Default | Description    | Required |
|----------|--------|---------|----------------|----------|
| a        | object | -       | original value | ✔        |
| b        | object | -       | compared value | ✔        |

```js|js
import { $equals } from'core/types';

$equals(1, 2);
$equals({
    key: true
}, {
    key: false
});
$equals([1, 2, 3], [1, 2, 3]);

---

false
false
true
```

## $exec

Execute specified function

| Variable | Type            | Default | Description                    | Required |
|----------|-----------------|---------|--------------------------------|----------|
| fn       | function, array | -       | Functions to execute           | ✔        |
| options  | object          | -       | [Callback options](#callbacks) |  -        |

```js
import { $exec } from'core/core';

$exec(() => {});
```

```js|js
import { $exec } from'core/core';

$exec((greeting, subject) => {
    console.log(`${greeting}${subject}`);
}, {
    scope: this,
    args: ['Hello', 'world']
});

---

'Hello world'
```


```
import { $exec } from'core/core';

$exec([
    function() {},
    function() {}
]);
```

## $isArray

Determine if value is an array

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| value    | any  | -       | Value to evaluate | ✔        |

```js|js
import { $isArray } from'core/types';

$isArray([
    'string',
    'string2'
]);

$isArray('string');

---

true
false
```

## $isFunction

Determine if value is a function

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| value    | any  | -       | Value to evaluate | ✔        |

```js|js
import { $isFunction } from'core/types';

$isFunction({});
$isFunction('string');
$isFunction(() => {});

---

false
false
true
true
```

## $isObject

Determine if value is an object

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| value    | any  | -       | Value to evaluate | ✔        |

```js|js
import { $isObject } from'core/types';

$isObject({});
$isObject('string');

---

true
false
```

## $isString

Determine if value is a string

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| value    | any  | -       | Value to evaluate | ✔        |

```js|js
import { $isString } from'core/types';

$isString({});
$isString('string');

---

false
true
```

## $map

Translate items in an array or selection to new array

The callback receives the current element as well as the index.

| Variable | Type                                      | Default | Description                    | Required |
|----------|-------------------------------------------|---------|--------------------------------|----------|
| target   | array, [selection](/script/dom#selection) | -       | Array or selection             | ✔        |
| fn       | function                                  | -       | Callback function              | ✔        |
| options  | object                                    | -       | [Callback](#callbacks) options |-          |

###Array

```js|js
$map([1, 2, 3], function(val) {
    return val + 1;
});

---

[2, 3, 4]
```

### Selection

```js|js
$map('ref:element', (el, i) => $(el).text());

---

["text", "text", ...]
```

## $parseHTML

Create document fragment from an HTML string

| Variable | Type   | Default | Description     | Required |
|----------|--------|---------|-----------------|----------|
| html     | string | -       | HTML to convert | ✔        |

```js
import { $parseHTML } from'core/dom';

const docFragment = $parseHTML('<span class="testing">Testing</span>');
$hasClass(docFragment.childNodes, 'testing');
```

## $serialize

Serialize

| Variable | Type   | Default | Description         | Required |
|----------|--------|---------|---------------------|----------|
| obj      | object | -       | Object to serialize | ✔        |

```js|html
import { $serialize } from'core/types';

$serialize({
    key1: 123,
    key2: [
        'value 1',
        'value 2'
    ]
});

---

key1=123&key2[]=value+1&key2[]=value+2
```

Only the first level of the object is serialized.

## $setRef

Add ref elements to datastore

Available data-ref values are pushed into the global storage for later retrieval. This method can be called after dynamic content is injected to ensure new refs are available for selection.

| Variable | Type                       | Default  | Description       | Required |
|----------|----------------------------|----------|-------------------|----------|
| context  | [selection](/script/dom#$) | document | Context selection |  -        |

```html
<div data-ref="element"></div>
```

```js
import { $setRef } from'core/dom';

$setRef();
```

```js|js
import $ from'wee-dom';

$('ref:element').toArray();

---

[<div data-ref="element"></div>]
```

This function is called by default on page load and after relevant DOM manipulation. Subsequent calls clear the cache for the provided context and reset the references.

## $toArray

Cast value to array if it isn't one

| Variable | Type | Default | Description               | Required |
|----------|------|---------|---------------------------|----------|
| val      | any  | -       | Value to convert to array | ✔        |

```js|js
import { $toArray } from'core/types';

$toArray(['test']);
$toArray('test');

---

['test']
['test']
```

## $type

Determine the JavaScript type of an object

| Variable | Type | Default | Description        | Required |
|----------|------|---------|--------------------|----------|
| obj      | any  | -       | Object to evaluate | ✔        |

```js|js
import { $type } from'core/types';

$type([
    'string',
    'string2'
]);
$type({});
$type('string');

---

array
object
string
```

## $unique

Create new array with only unique values from source array

| Variable | Type  | Default | Description | Required |
|----------|-------|---------|-------------|----------|
| array    | array | -       | Value array | ✔        |

```js|js
import { $unique } from'core/dom';

$unique([1, 1, 2, 3, 3, 3, 4]);

---

[1, 2, 3, 4]
```

## $unserialize

Convert serialized string back into an object

| Variable | Type   | Default | Description       | Required |
|----------|--------|---------|-------------------|----------|
| value    | string | -       | Serialized string | ✔        |

```js|js
import { $unserialize } from'core/types';

$unserialize('key1=123&key2[]=value+1&key2[]=value+2');

---

{
    "key1": "123",
    "key2[]": [
        "value 1",
        "value 2"
    ]
}
```

## $isNumber

Determine if value is a number

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| value    | any  | -       | Value to evaluate | ✔        |
|strict|boolean|true|Match values that are actual numbers, not strings with numeric characters||

```js|js
import { $isNumber } from'core/types';

$isNumber('1');
$isNumber(1);
$isNumber('1', false);

---

false
true
true
```

## $extend

Extend target object with source object(s)

| Variable | Type            | Default | Description                                 | Required |
|----------|-----------------|---------|---------------------------------------------|----------|
| deep     | boolean, object | false   | Extend nested properties else target object | ✔        |
| target   | object          | -       | Target/source object                        | ✔        |
| source   | object          | -       | Source object                               |  -        |
| source   | object          | -       | Additional objects...                       |   -       |

### Clone Object

If the second argument is an empty object literal, the third object will be cloned.

```js|js
import { $extend } from'core/types';

$extend(true, {}, {
    key1: 'val1',
    key2: 'val2'
});

---

{
    key1: "val1",
    key2: "val2"
}
```

### Merge Objects

```js|js
import { $extend } from'core/types';

$extend({
    key1: 'val1',
    key2: 'val2'
}, {
    key2: 'val3',
    key3: 'val4'
});

---

{
    key1: "val1",
    key2: "val3",
    key3: "val4"
}
```

## $copy

Clone provided object

| Variable | Type   | Default | Description          | Required |
|----------|--------|---------|----------------------|----------|
| target   | object | -       | Target/source object | ✔        |

```js|js
import { $copy } from'core/types';

$copy({
    key1: 'val1',
    key2: 'val2'
});

---

{
    key1: "val1",
    key2: "val2"
}
```
