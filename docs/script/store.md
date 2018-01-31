# Store

## $setVar

Refresh all store instances from data in DOM

| Variable | Type                               | Default  | Description              | Required |
|----------|------------------------------------|----------|--------------------------|----------|
| context  | [selection](/script/dom#selection) | document | Context to search within | -        |

**Document**

```html
<body>
    <meta data-set="key" data-value="true">
    ...
<body>
```

**Set Variables from Document**

```js
import { $setVar } from'wee-store';

$setVar();
```

**Retrieval**

```js|js
import $store from'wee-store';

$store.get('key');

---
true
```

## $store.concat

Merge arrays together

### Parameters

| Variable | Type    | Default | Description                                        | Required |
|----------|---------|---------|----------------------------------------------------|----------|
| key      | string  | -       | Property name                                      | ✔        |
| value    | array   | -       | Value to be merged into existing value             | ✔        |
| prepend  | boolean | false   | Add value to beginning of array instead of the end | -        |

```js|js
import $store from'wee-store';

$store.concat('key', 1); // Will create array if property does not yet exist
$store.concat('key', [2, 3]);
$store.concat('key', [4, 5], true); // Prepend value

$store.get('key');

---

[4, 5, 1, 2, 3]
```

## $store.configure

Sometimes, you may need to update settings on an existing store instance. This is most applicable to the default store module that is automatically generated. If you wanted to enable browser storage on the default module, for example, you could do this:

```js
$store.configure({ browserStorage: 'session' });
```

| Variable | Type   | Default | Description          | Required |
|----------|--------|---------|----------------------|----------|
| options  | object | { }     | Options object below | ✔        |

### Options Object

| Variable       | Type    | Default | Description                                                                               | Required |
|----------------|---------|---------|-------------------------------------------------------------------------------------------|----------|
| browserStorage | string  | -       | Enable browser storage to persist data from store instance - `local` or `session`         | -        |
| keepInMemory   | boolean | true    | Keep data set on store instance in memory (must be true unless browserStorage is enabled) | -        |

## $store.create

Create new store instance

### Parameters

| Variable | Type   | Default | Description            | Required |
|----------|--------|---------|------------------------|----------|
| name     | string | -       | Name of store instance | ✔        |
| options  | object | { }     | Store options below    | -        |

### Options Object

| Variable       | Type    | Default | Description                                                                               | Required |
|----------------|---------|---------|-------------------------------------------------------------------------------------------|----------|
| browserStorage | string  | -       | Enable browser storage to persist data from store instance - `local` or `session`         | -        |
| keepInMemory   | boolean | true    | Keep data set on store instance in memory (must be true unless browserStorage is enabled) | -        |
| prefix         | string  | 'wee'   | Prefix for storage key used to set browser storage if enabled                             |          |

```js|js
import $store from'wee-store';

const cartStore = $store.create('cart', {
    browserStorage: 'local',
    prefix: 'mysite'
});

cartStore.set('quantity', 2); // Data stored in localStorage under 'mysite_cart'

---

cartStore.get('quantity'); // 2
```

## $store.destroy

Destroy store instance

```js
import $store from'wee-store';

const $storeInstance = $store.create('test');

$storeInstance.destroy();
```

## $store.drop

Delete property

### Parameters

| Variable | Type   | Default | Description   | Required |
|----------|--------|---------|---------------|----------|
| key      | string | -       | Property name | ✔        |

### Remove by Key


```js|js
import $store from'wee-store';

// Will create array if property does not yet exist
$store.set('key', {
    key1: 1,
    key2: 2
});
$store.drop('key.key1');

$store.get('key');

---

{ key2: 2 }
```

### Remove by Value


```js|js
import $store from'wee-store';

// Will create array if property does not yet exist
$store.set('key', [1, 2, 3]);
$store.drop('key', 2);

$store.get('key');

---

[1, 3]
```

## $store.get

Retrieve property

### Parameters

| Variable | Type    | Default | Description                                    | Required |
|----------|---------|---------|------------------------------------------------|----------|
| key      | string  | -       | Property name                                  | -        |
| fallback | *       | -       | Fallback value if property does not exist      | -        |
| set      | boolean | false   | Set value if property doesn't exist            | -        |
| options  | object  | { }     | [See callback options](/script/core#callbacks) | -        |

### Simple


```js
import $store from'wee-store';

$store.set('key', true);
$store.set('otherKey', false);
```

```js|js
$store.get('key');

---

true
```

```js|js
$store.get('notSet');

---

null
```

### Retrieve all data


```js|js
// Continuation of Simple example above
$store.get();

---

{ key: true, otherKey: false }
```

### Fallback


```js|js
$store.get('key', 'Fallback');
$store.get('key');

---

Fallback
null
```

### Set Value


```js|js
$store.get('key', 'Fallback', true);
$store.get('key');

---

Fallback
Fallback
```

## $store.has

Check if property or value exists

### Parameters

| Variable | Type   | Default | Description      | Required |
|----------|--------|---------|------------------|----------|
| key      | string | -       | Storage property | ✔        |
| value    | *      | -       | Storage value    | -        |

### Check Key


```js|js
import $store from'wee-store';

$store.set('key', {
    key1: 'Don'
});
$store.has('key.key1');

---

true
```

### Check Value


```js|js
import $store from'wee-store';

$store.set('key', [1, 2, 3]);
$store.has('key', 2);
$store.has('key', 4);

---
<!--  -->
true
false
```

## $store.merge

Extend object

### Parameters

| Variable | Type   | Default | Description                               | Required |
|----------|--------|---------|-------------------------------------------|----------|
| key      | string | -       | Property name                             | ✔        |
| value    | object | -       | Object to be extended into existing value | ✔        |

```js|js
import $store from'wee-store';

// Will create array if property does not yet exist
$store.merge('key', {
    key1: 1,
});

$store.merge('key', {
    key2: 2,
});

$store.get('key');

---

{ key1: 1, key2: 2 }
```

## $store.push

Add a value to an array

### Parameters

| Variable | Type    | Default | Description                                        | Required |
|----------|---------|---------|----------------------------------------------------|----------|
| key      | string  | -       | Property name                                      | ✔        |
| value    | *       | -       | Value to be added to array                         | ✔        |
| prepend  | boolean | false   | Add value to beginning of array instead of the end | -        |

```js|js
import $store from'wee-store';

$store.push('key', 1); // Will create array if property does not yet exist
$store.push('key', 2);
$store.push('key', 3, true); // Prepend value

$store.get('key');
$store.get('key.0');

---

[3, 1, 2]
3
```

## $store.set

Set property

### Parameters

| Variable | Type   | Default | Description                                    | Required |
|----------|--------|---------|------------------------------------------------|----------|
| key      | string | -       | Property name                                  | ✔        |
| value    | *      | -       | Property value                                 | ✔        |
| options  | object | { }     | [See callback options](/script/core#callbacks) | -        |

### Simple


```js
import $store from'wee-store';

$store.set('key', true);
```

###
Function


```js|js
import $store from'wee-store';

$store.set('key', function(greeting, subject) {
    if (this.inclusive) {
        subject = 'world';
    }

    return`${greeting}${subject}!`;
}, {
    scope: { inclusive: true },
    args: ['Hello', 'Jim']
});

---

'Hello world!'
```

## $store.setVar

Refresh specific store instance from data in DOM

| Variable | Type                               | Default  | Description              | Required |
|----------|------------------------------------|----------|--------------------------|----------|
| context  | [selection](/script/dom#selection) | document | Context to search within | -        |

**Document**

```html
<body>
    <meta data-store="test" data-set="key" data-value="true">
    ...
<body>
```

**Set Variables from Document**

```js
import $store, { $setVar } from'wee-store';

const testStore = $store.create('test');

testStore.setVar();
```

**Retrieval**

```js|js
testStore.get('key');

---

true
```
