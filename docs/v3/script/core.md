# Core

## $

Get matches to specified selector or return parsed HTML

| Variable      | Type                                                   | Default  | Description                     | Required  |
| ------------- |:------------------------------------------------------:| --------:| -------------------------------:| ---------:|
| selector     	| [selection](https://www.weepower.com/script#selection) | -        | Target selection or HTML string | ✔         |
| context      	| [selection](https://www.weepower.com/script#selection) | document | Context selection               | -         |


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

Note: References can’t be chained like `$('ref:element .child')`. To scope a selection within a reference pass the ref selector as the context argument like `$('.child', 'ref:element')`.

### Multiple

Multiple selectors can be concatenated with commas. You can even mix refs with standard selectors.

```js
    Wee.$('ref:element, .js-element li');
```

```js
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

| Variable  | Type           | Default  | Description                     | Required  |
| --------- |:--------------:| --------:| -------------------------------:| ---------:|
| a     	| string, object | -        | Controller name or core methods | ✔         |
| b     	| object         | -        | Public methods and properties   | -         |
| c     	| object         | -        | Private methods and properties  | -         |

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

| Variable  | Type     | Default  | Description                    | Required  |
| --------- |:--------:| --------:| ------------------------------:| ---------:|
| name     	| string   | -        | Controller name                | ✔         |
| pub     	| object   | -        | Public methods and properties  | ✔         |
| priv    	| object   | -        | Private methods and properties | -         |
| options   | object   | -        | Object properties below        | -         |

### Options Object

| Variable  | Type     | Default  | Description                                                       | Required  |
| --------- |:--------:| --------:| -----------------------------------------------------------------:| ---------:|
| args     	| object   | -        | Passed to _construct method (both public and private) if defined  | -         |
| instance  | boolean  | true     | Instructs make method to instantiate controller                   | -         |

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

```js
    Wee.fn.make('controllerName', {
        _destruct: function() {
            this.save();
        }
    });
```

Note: The construct and destruct methods can be placed in the public object and/or the private object.

### Inheritance

You can easily leverage existing controllers to extend into new controllers by using ‘childController:parentController’ controller name syntax.

```js
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
```

## $concat

Concatenate values into global storage

| Variable  | Type     | Default  | Description                    | Required  |
| --------- |:--------:| --------:| ------------------------------:| ---------:|
| key    	| string   | -        | Storage reference or value     | ✔         |
| value     | any      | -        | Storage value or prepend value | -         |
| prepend   | boolean  | false    | Prepend value to storage       | -         |  

```js
    Wee.$concat('key', 1);
    Wee.$concat('key', [2, 3], true);
```

```js
    [2, 3, 1]
```

## $diff

Generate a delta from two objects

| Variable  | Type     | Default  | Description     | Required  |
| --------- |:--------:| --------:| ---------------:| ---------:|
| a   	    | object   | -        | Original object | ✔         |
| b         | object   | -        | Compared object | ✔         |
								
```js
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
```

```js
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
```

## $drop

Remove key or value from global array

| Variable  | Type    | Default  | Description                          | Required  |
| --------- |:-------:| --------:| ------------------------------------:| ---------:|
| key   	| string  | -        | Storage reference or value           | ✔         |
| value     | any     | -        | Storage key, value, or prepend value | -         |
| prepend   | boolean | false    | Prepend value to storage             | -         |

### Key

```js
    Wee.$set('key', {
        key1: 'Don',
        key2: 'Draper'
    });
    Wee.$drop('key.key2');
```
```js
    {
        key1: 'Don'
    }
```

### Value

```js
    Wee.$set('key', [1, 2, 3]);
    Wee.$drop('key', 2);
```

```js
    [1, 3]
```

## $each

Execute function for each matching selection

| Variable  | Type                            | Default  | Description               | Required  |
| --------- |:-------------------------------:| --------:| -------------------------:| ---------:|
| target  	| [selection](/script#selection)  | -        | Target selection          | ✔         |
| fn        | [function](/script#functions)   | -        | Callback function         | ✔         |
| options   | object                          | -        | Object properties below   | -         |

### Options Object

| Variable  | Type                           | Default  | Description                      | Required  |
| --------- |:------------------------------:| --------:| --------------------------------:| ---------:|
| args 	    | array                          | -        | Callback arguments               | -         |
| context   | [selection](/script#selection) | document | Callback context                 | -         |
| scope     | object                         | -        | Callback scope                   | -         |
| reverse   | boolean                        | false    | Reverse the order of execution   | -         |

### Simple

```js
    Wee.$each('ref:element', function(el, i) {
        // Callback logic
    });
```
### Advanced

```js
    Wee.$each('ref:element', function(el, i) {
        // Callback logic
    }, {
        reverse: true,
        scope: this
    });
```

Note: The element and index are injected as the first two callback parameters.

## $env

Get current environment or set current environment against specified object

| Variable  | Type   | Default  | Description            | Required  |
| --------- |:------:| --------:| ----------------------:| ---------:|
| rules	    | object | -        | Environmental rules    | -         |
| fallback  | string | "local"  | Default environment    | -         |

### Set

The key values can either be strings for a direct match or a [functions](/script#functions) for more complex evaluation. If a function is provided the response should be a boolean. If no match is found the default environment value is used.

```js
    Wee.$env({
        prod: 'www.weepower.com',
        stage: 'stage.weepower.com'
    });
```

```js
    "prod"
```

### Get
```js
    Wee.$env();
```

```js
    "prod"
```
## $envSecure

Determine if the current environment is SSL encrypted
```js
    Wee.$envSecure();
```

```js
    true
```
## $equals

Compare two values for strict equality

| Variable  | Type   | Default  | Description       | Required  |
| --------- | ------:| --------:| -----------------:| ---------:|
| a	        | object | -        | original value    | ✔         |
| b         | object | -        | compared value    | ✔         |
								
```js
    Wee.$equals(1, 2);
    Wee.$equals({
        key: true
    }, {
        key: false
    });
    Wee.$equals([1, 2, 3], [1, 2, 3]);
```

```js
    false
    false
    true
```
## $exec

Execute specified function or controller method

| Variable | Type                                |Default | Description          | Required |
| -------- |-------------------------------------|--------|--------------------- |----------|
|fn        |[function](/script#functions), array | -      |Functions to execute  | ✔	    |
|options   | object                              | -      |Function options below| -        |

|Variable  |Type                                 |Default |Description           |Required  |
|----------|-------------------------------------|--------|----------------------|----------|
|args      |array                                |-       |Function arguments    |-         |
|scope     |object                               |-       |Function scope        |-         |

```js
    Wee.$exec('controllerName:methodName');
```
```js
    Wee.$exec('controllerName:methodName', {
        scope: this,
        args: [
            'Hello',
            123
        ]
    });
```
```js
    Wee.$exec(function() {
        //
    });
```
```js
    Wee.$exec([
        'controllerName:methodName',
        'controllerName2:methodName2'
    ]);
```

Note: This method is mostly intended for external use although it can be used anywhere. Controller methods are best executed in the form of `Wee.controllerName.methodName()`.

## $get

Get global variable

|Variable|Type    |Default |Description                          |Required|
|--------|--------|--------|-------------------------------------|--------|
|key     |string  |-       |Storage reference                    |-       |
|fallback|any     |null    |Default value if not set             |-       |
|set     |boolean |false   |Set default permanently              |-       |
|options |object  |-       |[Callback options](/script#functions)|-       |

```js
    Wee.$get('key');
    Wee.$get('key', 'Fallback');
    Wee.$get('key');
    Wee.$get('key', 'Fallback', true);
    Wee.$get('key');
```

```js
    null
    Fallback
    null
    Fallback
    Fallback
```
### Get All

```js
    Wee.$get();
```

```js
    {object}
```

## $has

Check if storage criteria is set

|Variable|Type    |Default |Description         |Required|
|--------|--------|--------|--------------------|--------|
|key     |string  |-       |Storage reference   |✔       |
|value   |any     |-       |Storage key or value|-       |

### Key

```js
    Wee.$set('key', {
        key1: 'Don'
    });
    Wee.$has('key.key1');
```

```js
    true
```

### Value

```js
    Wee.$set('key', [1, 2, 3]);
    Wee.$has('key', 4);
```

```js
    false
```
## $isArray

Determine if value is an array

|Variable|Type    |Default |Description      |Required|
|--------|--------|--------|-----------------|--------|
|value   |any     |-       |Value to evaluate| ✔      |
											
```js
    Wee.$isArray([
        'string',
        'string2'
    ]);
    Wee.$isArray('string');
```

```js
    true
    false
```

## $isFunction

Determine if value is a function


|Variable|Type    |Default |Description      |Required|
|--------|--------|--------|-----------------|--------|
|value   |any     |-       |Value to evaluate| ✔      |

```js
    Wee.$isFunction({});
    Wee.$isFunction('string');
    Wee.$isFunction('controller:fn');
    Wee.$isFunction(function() {});
```
```js
    false
    false
    true
    true
```
## $isObject

Determine if value is an object

|Variable|Type    |Default |Description      |Required|
|--------|--------|--------|-----------------|--------|
|value   |any     |-       |Value to evaluate|✔		  |
										
```js
    Wee.$isObject({});
    Wee.$isObject('string');
```

```js
    true
    false
```
## $isString

Determine if value is a string

|Variable|Type    |Default |Description      |Required|
|--------|--------|--------|-----------------|--------|
|value   |any     |-       |Value to evaluate| ✔      |
											
```js
    Wee.$isString({});
    Wee.$isString('string');
```

```js
    false
    true
```
## $map

Translate items in an array or selection to new array

The callback receives the current element as well as the index.

|Variable|Type                                 |Default |Description           |Required|
|--------|-------------------------------------|--------|----------------------|--------|
|target  |array, [selection](/script#selection)|-       |Array or selection    | ✔      |
|fn      |[function](/script#functions)        |-       |Callback function     | ✔      |
|options |object                               |-       |Callback options below| -      |

|Variable|Type    |Default|Description       |Required|
|--------|--------|-------|------------------|--------|
|args    |array   |-      |Function arguments|-       |
|scope   |object  |-      |Function scope    |-       |

### Array
```js
    Wee.$map([1, 2, 3], function(val) {
        return val + 1;
    });
```

```js
    [2, 3, 4]
```

### Selection

```js
    Wee.$map('ref:element', function(el, i) {
        return $(el).text();
    });
```
```js
    ["text", "text", ...]
```

## $merge

Extend object into global storage

|Variable|Type    |Default |Description                      |Required|
|--------|--------|--------|---------------------------------|--------|
|key     |string  |-       |Storage reference or merge object|✔       |
|obj     |any     |-       |Storage value or prepend value   |-       |

Storage value or prepend value
```js
    Wee.$merge('key', {
        key1: 'value'
    });
    Wee.$merge('key', {
        key2: 'value2'
    });
```

```js
    {
        key1: "value",
        key2: "value"
    }
```

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

### Basic
```js
    Wee.$observe('key', function(data, type) {
        console.log(data);
    }, {
        recursive: true
    });
    Wee.$set('key.nested', 5);
```
```js
    {
        nested: 5
    }
```
### Advanced
```js
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
```
```js
    2
```
## $parseHTML

Create document fragment from an HTML string

VariableTypeDefaultDescriptionRequired
html

string

-

HTML to convert

													✔
											
```js
    var el = Wee.$parseHTML('<span class="testing">Testing</span>');
    Wee.$hasClass(el.childNodes, 'testing');
```

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
```js
    Wee.$push('key', 'Success');
    Wee.$push('key', 'Success 2');
    
    Wee.$get('key');
    Wee.$get('key.0');
```
```js
    ["Success", "Success 2"]
    Success
```

## $serialize

Serialize

VariableTypeDefaultDescriptionRequired
obj

object

-

Object to serialize

													✔
```js										
    Wee.$serialize({
        key1: 123,
        key2: [
            'value 1',
            'value 2'
        ]
    });
```

```js
    key1=123&key2[]=value+1&key2[]=value+2
```

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
```js
    Wee.$set('key', 'Success');
```
```js
    "Success"
```
### Callbacks

```js
    Wee.$set('key', function() {
        return 5 * 5;
    });
```

```js
    Wee.$set('key', 'controllerName:publicFunction', {
        scope: this,
        args: [
            'Hello',
            123
        ]
    });
```
## $setRef

Add ref elements to datastore

Available data-ref values are pushed into the global storage for later retrieval. This method can be called after dynamic content is injected to ensure new refs are available for selection.

VariableTypeDefaultDescriptionRequired
context

[selection](/script#selection)

document

Context selection

```html
    <div data-ref="element"></div>
```

```js
    Wee.$setRef();
```

```js
    $('ref:element');
```

```html
    <div data-ref="element"></div>
```

Note: This function is called by default on page load and after relevant DOM manipulation. Subsequent calls clear the cache for the provided context and reset the references.

## $setVar

Add metadata variables to datastore

### Single Value

Available data-set values are pushed into the global storage for later retrieval.

```html
    <div data-set="key" data-value="value"></div>
```

```js
    Wee.$setVar();
```

```js
    Wee.$get('key');
```

```js
    "value"
```

### Value Array

To push into an array instead of setting a single value append array brackets to the end of the key.

```html
    <div data-set="key[]" data-value="value1"></div>
    <div data-set="key[]" data-value="value2"></div>
    <div data-set="key[]" data-value="value3"></div>
```

```js
    Wee.$get('key');
```

```js
    ["value1", "value2", "value3"]
```

### Simple Object

To create a keyed object you can pass keys into the array notation
```html
    <div data-set="obj.key1" data-value="value1"></div>
    <div data-set="obj.key2" data-value="value2"></div>
    <div data-set="obj.key3" data-value="value3"></div>
```

```js
    Wee.$get('obj');

    {
        "key1": "value1",
        "key2": "value2"
        "key3": "value3"
    }
```

### Complex Object

You can also nest objects by continuing the array notation.
```html
    <div data-set="obj.key1" data-value="value1"></div>
    <div data-set="obj.key2.sub1" data-value="value2"></div>
    <div data-set="obj.key2.sub2" data-value="value3"></div>
```

```js
    Wee.$get('obj');

    {
        "key1": "value1",
        "key2": {
            "sub1": "value2",
            "sub2": "value2"
        }
    }
```

### JSON

```html
    <div data-set="obj" data-value='{"key": true}'></div>
```

```js
    Wee.$get('obj.key');
```

```js
    true
```

This function is called by default on page load.

## $toArray

Cast value to array if it isn't one

VariableTypeDefaultDescriptionRequired
val

any

-

Value to convert to array

													✔
											
```js
    Wee.$toArray(['test']);
    Wee.$toArray('test');
```

```js
    ["test"]
    ["test"]
```

## $trigger

Execute matching observed callbacks

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

													✔
											
```js
    Wee.$observe('key', function() {
        console.log('Success');
    });
    Wee.$trigger('key');
```

```js
    Success
```

## $type

Determine the JavaScript type of an object

VariableTypeDefaultDescriptionRequired
obj

any

-

Object to evaluate

													✔
											
```js
    Wee.$type([
        'string',
        'string2'
    ]);
    Wee.$type({});
    Wee.$type('string');
```
```js
    array
    object
    string
```
## $unique

Create new array with only unique values from source array

VariableTypeDefaultDescriptionRequired
array

array

-

Value array

													✔
											
```js
    Wee.$unique([1, 1, 2, 3, 3, 3, 4]);
```

```js
    [1, 2, 3, 4]
```

## $unobserve

Remove callback from data storage change

VariableTypeDefaultDescriptionRequired
key

string

-

Storage reference

### Remove All
```js
    Wee.$unobserve();
```
### Remove Single
```js
    Wee.$unobserve('key.nested');
```
## $unserialize

Convert serialized string back into an object

VariableTypeDefaultDescriptionRequired
str

string

-

Serialized string

													✔
											
```js
    Wee.$unserialize('key1=123&key2[]=value+1&key2[]=value+2');
```
```js
    {
        "key1": "123",
        "key2[]": [
            "value 1",
            "value 2"
        ]
    }
```

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