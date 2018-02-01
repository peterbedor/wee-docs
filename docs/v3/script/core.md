# Core

## $

Get matches to specified selector or return parsed HTML

VariableTypeDefaultDescriptionRequired
selector

[selection](https://www.weepower.com/script#selection)

-

Target selection or HTML string

													✔
											
context

[selection](https://www.weepower.com/script#selection)

document

Context selection

```js
    Wee.$('.js-element li');
```

```js
    [node, node, ...]
```

### Contextual

The context selection subsets the query to a more specific scope. This can result in a more limited and efficient traversal of the DOM.

```js
    Wee.$('li', '.js-element');
```

```js
    [node, node, ...]
```

### References

Pre-fetched elements can be selected by using the ‘ref:name’ format.

```js
    Wee.$('ref:element');
```

```js
    [node, node, ...]
```

References can’t be chained like `$('ref:element .child')`. To scope a selection within a reference pass the ref selector as the context argument like `$('.child', 'ref:element')`.

### Multiple

Multiple selectors can be concatenated with commas. You can even mix refs with standard selectors.

```js
    Wee.$('ref:element, .js-element li');

    [node, node, ...]
```

### Parsing HTML

If HTML is provided it will be parsed and returned.

```js
    Wee.$('<div class="element" />');
```

```js
    [node]
```

### External selector engine

To use another query engine set the global `WeeSelector` variable. This variable can be set anywhere at any time but before Wee instantiation is ideal.

```js
    var WeeSelector = Sizzle;
```

## fn.extend

Extend existing controller with additional methods and properties

VariableTypeDefaultDescriptionRequired
a

string, object

-

Controller name or core methods

													✔
											
b

object

-

Public methods and properties

c

object

-

Private methods and properties

### Extend Controller
```js
    Wee.fn.extend('controllerName', {
        extendedPublicFunction: function() {
            this.finalPublicFunction('output');
        }
    });
```

```js
    Wee.controllerName.extendedPublicFunction();
```

```js
    "Success"
```

### Extend Core

To extend the core pass a method object as the first argument. This can be done to add additional core methods or override default functionality.

```js
    Wee.fn.extend({
        addNumbers: function(num1, num2) {
            return num1 + num2;
        }
    });
```

```js
    Wee.addNumbers(2, 4);
```

```js
    6
```

Note: When extending a controller that doesn’t exist a new controller is created.

## fn.make

Create namespaced controller

Controllers serve as the wrapper for custom script. They can be created per page, section, or for specific reusable components. If placed in your build directory you easily create a well-organized, extensible structure.

VariableTypeDefaultDescriptionRequired
name

string

-

Controllername

													✔
											
pub

object

-

Public methods and properties

													✔
											
priv

object

-

Private methods and properties

options

object

-

Object properties below

### Options Object

VariableTypeDefaultDescriptionRequired
args

object

-

Passed to _construct method (both public and private) if defined

instance

boolean

true

Instructs make method to instantiate controller

### Public
```js
    Wee.fn.make('controllerName', {
        init: function() {
            return 'Initialized';
        }
    });
```
```js
    Wee.controllerName.init();
```
```js
    "Initialized"
```

Note: To create a new instance of a controller use the following syntax:
`var instance = Wee.fn.controllerName();`

### Private/Public

Private functions can be accessed from public methods by using `this.$private.functionName(arguments)` syntax. To call back into a public method from a private one use this.$public.functionName(arguments).

Also note that you have access to `this.$get()`, `this.$set()`, and `this.$push(`) across both public and private methods. By default stored values are namespaced to the current controller scope. If you need to control global variables use `Wee.$get()`, `Wee.$set()`, and `Wee.$push()`.

```js
    Wee.fn.make('controllerName', {
        init: function() {
            this.anotherPublicFunction('varName'); // Call public method
    
            return this.$private.privateFunction('varName'); // Call private method
        },
        anotherPublicFunction: function(key) {
            this.$set(key, 'Success');
        },
        finalPublicFunction: function(output) {
            console.log(output);
        }
    }, {
        privateFunction: function(key) {
            return this.anotherPrivateFunction(key); // Call private method
        },
        anotherPrivateFunction: function(key) {
            var output = this.$get(key);
    
            this.$public.finalPublicFunction(output); // Call public method
        }
    });
```

```js
    Wee.controllerName.init();
```

```js
    "Success"
```

### Constructor

The construct method is immediately executed on controller creation and is useful for setting variables or invoking additional methods.
```js
    Wee.fn.make('controllerName', {
        _construct: function() {
            this.publicVariable = 'Public Variable';
    
            this.init();
        }
    });
```

Note: You can pass a config object to controller constructors.

```js
    Wee.fn.make('controllerName', {
        _construct: function(options) {
            this.publicVar = options.publicVar;
        }
    }, {
        _construct: function(options) {
            this.privateVar = options.privateVar;
        }
    }, {
        args: {
            publicVar: 'public',
            privateVar: 'private'
        }
    });
    
    console.log(Wee.controllerName.publicVar);
    console.log(Wee.controllerName.privateVar);
```

```js
    'public'
    'private'
```

```js
    var instance = Wee.fn.controllerName({
        publicVar: 'another public'
    });
    
    console.log(instance.publicVar);
```

```js
    'another public'
```

### Destructor

The destruct method is executed to perform additional clean up or other actions when the controller is destroyed using `this.$destroy()` or `Wee.controllerName.$destroy()` outside the controller.

    Wee.fn.make('controllerName', {
        _destruct: function() {
            this.save();
        }
    });

The construct and destruct methods can be placed in the public object and/or the private object.

### Inheritance

You can easily leverage existing controllers to extend into new controllers by using ‘childController:parentController’ controller name syntax.

    Wee.fn.make('parentName', {
        base: function() {
            // Base logic
        }
    });
    
    Wee.fn.make('childName:parentName', {
        init: function() {
            this.base();
        }
    });

## $concat

Concatenate values into global storage

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference or value

													✔
											
value

any

-

Storage value or prepend value

prepend

boolean

false

Prepend value to storage

    Wee.$concat('key', 1);
    Wee.$concat('key', [2, 3], true);

    [2, 3, 1]

## $diff

Generate a delta from two objects

VariableTypeDefaultDescriptionRequired
a

object

-

Original object

													✔
											
b

object

-

Compared object

													✔
											

    Wee.$diff({
        key1: 'Don',
        key2: true,
        key3: {
            nested: true
        }
    }, {
        key1: 'Don',
        key3: {
            nested: false
        },
        key4: 'new'
    });

    {
        key1: {
            after: "Don",
            before: "Don",
            type: "-"
        },
        key2: {
            after: undefined,
            before: true,
            type: "d"
        },
        key3: {
            nested: {
                after: false,
                before: true,
                type: "u"
            }
        },
        key4: {
            after: "new",
            before: undefined,
            type: "c"
        }
    }

## $drop

Remove key or value from global array

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference or value

													✔
											
value

any

-

Storage key, value, or prepend value

prepend

boolean

false

Prepend value to storage

### Key

    Wee.$set('key', {
        key1: 'Don',
        key2: 'Draper'
    });
    Wee.$drop('key.key2');

    {
        key1: 'Don'
    }

### Value

    Wee.$set('key', [1, 2, 3]);
    Wee.$drop('key', 2);

    [1, 3]

## $each

Execute function for each matching selection

VariableTypeDefaultDescriptionRequired
target

[selection](/script#selection)

-

Target selection

													✔
											
fn

[function](/script#functions)

-

Callback function

													✔
											
options

object

-

Object properties below

### Options Object

VariableTypeDefaultDescriptionRequired
args

array

-

Callback arguments

context

[selection](/script#selection)

document

Callback context

scope

object

-

Callback scope

reverse

boolean

false

Reverse the order of execution

### Simple

    Wee.$each('ref:element', function(el, i) {
        // Callback logic
    });

### Advanced

    Wee.$each('ref:element', function(el, i) {
        // Callback logic
    }, {
        reverse: true,
        scope: this
    });

The element and index are injected as the first two callback parameters.

## $env

Get current environment or set current environment against specified object

VariableTypeDefaultDescriptionRequired
rules

object

-

Environmental rules

fallback

string

"local"

Default environment

### Set

The key values can either be strings for a direct match or a [functions](/script#functions) for more complex evaluation. If a function is provided the response should be a boolean. If no match is found the default environment value is used.

    Wee.$env({
        prod: 'www.weepower.com',
        stage: 'stage.weepower.com'
    });

    "prod"

### Get

    Wee.$env();

    "prod"

## $envSecure

Determine if the current environment is SSL encrypted

    Wee.$envSecure();

    true

## $equals

Compare two values for strict equality

VariableTypeDefaultDescriptionRequired
a

object

-

original value

													✔
											
b

object

-

Compared value

													✔
											

    Wee.$equals(1, 2);
    Wee.$equals({
        key: true
    }, {
        key: false
    });
    Wee.$equals([1, 2, 3], [1, 2, 3]);

    false
    false
    true

## $exec

Execute specified function or controller method

VariableTypeDefaultDescriptionRequired
fn

[function](/script#functions), array

-

Functions to execute

													✔
											
options

object

-

Function options below

VariableTypeDefaultDescriptionRequired
args

array

-

Function arguments

scope

object

-

Function scope

    Wee.$exec('controllerName:methodName');

    Wee.$exec('controllerName:methodName', {
        scope: this,
        args: [
            'Hello',
            123
        ]
    });

    Wee.$exec(function() {
        //
    });

    Wee.$exec([
        'controllerName:methodName',
        'controllerName2:methodName2'
    ]);

This method is mostly intended for external use although it can be used anywhere. Controller methods are best executed in the form of `Wee.controllerName.methodName()`.

## $get

Get global variable

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

fallback

any

null

Default value if not set

set

boolean

false

Set default permanently

options

object

-

[Callback options](/script#functions)

    Wee.$get('key');
    Wee.$get('key', 'Fallback');
    Wee.$get('key');
    Wee.$get('key', 'Fallback', true);
    Wee.$get('key');

    null
    Fallback
    null
    Fallback
    Fallback

### Get All

    Wee.$get();

    {object}

## $has

Check if storage criteria is set

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

													✔
											
value

any

-

Storage key or value

### Key

    Wee.$set('key', {
        key1: 'Don'
    });
    Wee.$has('key.key1');

    true

### Value

    Wee.$set('key', [1, 2, 3]);
    Wee.$has('key', 4);

    false

## $isArray

Determine if value is an array

VariableTypeDefaultDescriptionRequired
value

any

-

Value to evaluate

													✔
											

    Wee.$isArray([
        'string',
        'string2'
    ]);
    Wee.$isArray('string');

    true
    false

## $isFunction

Determine if value is a function

VariableTypeDefaultDescriptionRequired
value

any

-

Value to evaluate

													✔
											

    Wee.$isFunction({});
    Wee.$isFunction('string');
    Wee.$isFunction('controller:fn');
    Wee.$isFunction(function() {});

    false
    false
    true
    true

## $isObject

Determine if value is an object

VariableTypeDefaultDescriptionRequired
value

any

-

Value to evaluate

													✔
											

    Wee.$isObject({});
    Wee.$isObject('string');

    true
    false

## $isString

Determine if value is a string

VariableTypeDefaultDescriptionRequired
value

any

-

Value to evaluate

													✔
											

    Wee.$isString({});
    Wee.$isString('string');

    false
    true

## $map

Translate items in an array or selection to new array

The callback receives the current element as well as the index.

VariableTypeDefaultDescriptionRequired
target

array, [selection](/script#selection)

-

Array or selection

													✔
											
fn

[function](/script#functions)

-

Callback function

													✔
											
options

object

-

Callback options below

VariableTypeDefaultDescriptionRequired
args

array

-

Function arguments

scope

object

-

Function scope

### Array

    Wee.$map([1, 2, 3], function(val) {
        return val + 1;
    });

    [2, 3, 4]

### Selection

    Wee.$map('ref:element', function(el, i) {
        return $(el).text();
    });

    ["text", "text", ...]

## $merge

Extend object into global storage

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference or merge object

													✔
											
obj

any

-

Storage value or prepend value

    Wee.$merge('key', {
        key1: 'value'
    });
    Wee.$merge('key', {
        key2: 'value2'
    });

    {
        key1: "value",
        key2: "value"
    }

## $observe

Attach callback to data storage change

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

													✔
											
fn

[function](/script#functions)

-

Trigger method

													✔
											
options

object

-

Observation options below

### Options Object

VariableTypeDefaultDescriptionRequired
diff

boolean

false

Include diff in callback

once

boolean

false

Execute only once

recursive

boolean

false

Look for nested value changes

value

*

Specific value to trigger callback

### 
Basic

    Wee.$observe('key', function(data, type) {
        console.log(data);
    }, {
        recursive: true
    });
    Wee.$set('key.nested', 5);

    {
        nested: 5
    }

### 
Advanced

    Wee.$set('key', 1);
    Wee.$observe('key', function(data, type, diff) {
        if (type == 'set' && diff.before === 1) {
            console.log(data);
        }
    }, {
        diff: true,
        once: true,
        value: 2
    });
    Wee.$set('key', 2);

    2

## $parseHTML

Create document fragment from an HTML string

VariableTypeDefaultDescriptionRequired
html

string

-

HTML to convert

													✔
											

    var el = Wee.$parseHTML('<span class="testing">Testing</span>');
    Wee.$hasClass(el.childNodes, 'testing');

## $push

Push value into global array

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference or value

													✔
											
value

any

-

Storage value or prepend value

prepend

false

-

Prepend value to storage

    Wee.$push('key', 'Success');
    Wee.$push('key', 'Success 2');
    
    Wee.$get('key');
    Wee.$get('key.0');

    ["Success", "Success 2"]
    Success

## $serialize

Serialize

VariableTypeDefaultDescriptionRequired
obj

object

-

Object to serialize

													✔
											

    Wee.$serialize({
        key1: 123,
        key2: [
            'value 1',
            'value 2'
        ]
    });

    key1=123&key2[]=value+1&key2[]=value+2

Only the first level of the object is serialized.

## $set

Set global variable

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference value

													✔
											
value

any

-

Storage value or callback object

options

object

-

[Callback options](https://www.weepower.com/script#functions)

### Simple

    Wee.$set('key', 'Success');

    "Success"

### Callbacks

    Wee.$set('key', function() {
        return 5 * 5;
    });

    Wee.$set('key', 'controllerName:publicFunction', {
        scope: this,
        args: [
            'Hello',
            123
        ]
    });

## $setRef

Add ref elements to datastore

Available data-ref values are pushed into the global storage for later retrieval. This method can be called after dynamic content is injected to ensure new refs are available for selection.

VariableTypeDefaultDescriptionRequired
context

[selection](/script#selection)

document

Context selection

    <div data-ref="element"></div>

    Wee.$setRef();

    $('ref:element');

    <div data-ref="element"></div>

This function is called by default on page load and after relevant DOM manipulation. Subsequent calls clear the cache for the provided context and reset the references.

## $setVar

Add metadata variables to datastore

### Single Value

Available data-set values are pushed into the global storage for later retrieval.

    <div data-set="key" data-value="value"></div>

    Wee.$setVar();

    Wee.$get('key');

    "value"

### Value Array

To push into an array instead of setting a single value append array brackets to the end of the key.

    <div data-set="key[]" data-value="value1"></div>
    <div data-set="key[]" data-value="value2"></div>
    <div data-set="key[]" data-value="value3"></div>

    Wee.$get('key');

    ["value1", "value2", "value3"]

### Simple Object

To create a keyed object you can pass keys into the array notation

    <div data-set="obj.key1" data-value="value1"></div>
    <div data-set="obj.key2" data-value="value2"></div>
    <div data-set="obj.key3" data-value="value3"></div>

    Wee.$get('obj');

    {
        "key1": "value1",
        "key2": "value2"
        "key3": "value3"
    }

### Complex Object

You can also nest objects by continuing the array notation.

    <div data-set="obj.key1" data-value="value1"></div>
    <div data-set="obj.key2.sub1" data-value="value2"></div>
    <div data-set="obj.key2.sub2" data-value="value3"></div>

    Wee.$get('obj');

    {
        "key1": "value1",
        "key2": {
            "sub1": "value2",
            "sub2": "value2"
        }
    }

### JSON

    <div data-set="obj" data-value='{"key": true}'></div>

    Wee.$get('obj.key');

    true

This function is called by default on page load.

## $toArray

Cast value to array if it isn't one

VariableTypeDefaultDescriptionRequired
val

any

-

Value to convert to array

													✔
											

    Wee.$toArray(['test']);
    Wee.$toArray('test');

    ["test"]
    ["test"]

## $trigger

Execute matching observed callbacks

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

													✔
											

    Wee.$observe('key', function() {
        console.log('Success');
    });
    Wee.$trigger('key');

    Success

## $type

Determine the JavaScript type of an object

VariableTypeDefaultDescriptionRequired
obj

any

-

Object to evaluate

													✔
											

    Wee.$type([
        'string',
        'string2'
    ]);
    Wee.$type({});
    Wee.$type('string');

    array
    object
    string

## $unique

Create new array with only unique values from source array

VariableTypeDefaultDescriptionRequired
array

array

-

Value array

													✔
											

    Wee.$unique([1, 1, 2, 3, 3, 3, 4]);

    [1, 2, 3, 4]

## $unobserve

Remove callback from data storage change

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

### Remove All

    Wee.$unobserve();

### Remove Single

    Wee.$unobserve('key.nested');

## $unserialize

Convert serialized string back into an object

VariableTypeDefaultDescriptionRequired
str

string

-

Serialized string

													✔
											

    Wee.$unserialize('key1=123&key2[]=value+1&key2[]=value+2');

    {
        "key1": "123",
        "key2[]": [
            "value 1",
            "value 2"
        ]
    }

## $extend

Extend target object with source object(s)

VariableTypeDefaultDescriptionRequired
deep

boolean, object

false

Extend nested properties else target object

													✔
											
target

object

-

Target/source object

													✔
											
source

object

-

Source object

source

object

-

Additional objects...

### Clone Object

If the second argument is an empty object literal, the third object will be cloned.
```js
    Wee.$extend(true, {}, {
        key1: 'val1',
        key2: 'val2'
    });

    {
        key1: "val1",
        key2: "val2"
    }
```

### Merge Objects
```js
    Wee.$extend({
        key1: 'val1',
        key2: 'val2'
    }, {
        key2: 'val3',
        key3: 'val4'
    });

    {
        key1: "val1",
        key2: "val3",
        key3: "val4"
    }
```