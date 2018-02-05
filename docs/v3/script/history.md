# History

HTML5 history and PJAX helper to create dynamic experiences

Using the Wee History feature you can make partial DOM replacements while manipulating the URL to create smooth, efficient navigation.

## Bind

Bind element events and form submit events to PJAX

|Variable|Type                                   |Default |Description                                                       |Required|
|--------|---------------------------------------|--------|------------------------------------------------------------------|--------|
|events  |object                                 |-       |{event: selector} object to bind                                  |✔|
|a       |object,[selection](/script/#selection) |-       |Context or same options available to [go method](/script/history#go)|-|
|context |[selection](/script/#selection)        |document|Context selection                                                 |-|

### Basic

```js
Wee.history.bind({
    click: 'a',
    submit: '.element'
});
```

### Advanced

```js
Wee.history.bind({
        click: 'a:not([data-static])'
    },
    'ref:element',
    {
        extensions: [
            'html',
            'php',
        ],
        partials: 'title, .js-sidebar, ref:inner',
        request: {
            root: '/pjax',
            success: function() {
                ga('send', 'pageview');
            }
        }
    }
});
```

## Go

Navigate to a new path or within the browser history

|Variable|Type    |Default |Description            |Required|
|--------|--------|--------|-----------------------|--------|
|options |object  |-       |Object properties below|✔		|

### Options Object

|Variable     |Type                                   |Default      |Description                                          |Required|
|-------------|---------------------------------------|-------------|-----------------------------------------------------|--------|
|action       |string                                 |'replace'    |Either 'replace' or 'append' content                 |-       |
|extensions   |array                                  |-            |Whitelist of path extensions to support              |-       |
|partials     |[selection](/script/#selection)        |'title, main'|Elements to replace from response                    |-       |
|path         |string                                 |-            |Path to local resource                               |✔       |
|processErrors|boolean                                |false        |Process replacements on error responses              |-       |
|push         |boolean                                |true         |Push the path to the browser URL                     |-       |
|request      |object                                 |-            |Pass-through object to [Wee.data](/script/history#go)|-       |
|run          |boolean                                |true         |Evaluate routing rules                               |-       |
|scrollTop    |number, [selection](/script/#selection)|0            |Vertical offset to scroll                            |-       |
|title        |string                                 |-            |Set or override the returned page title              |-       |

### Basic

```js
Wee.history.go({
    path: '/page/path'
});
```

### Advanced

```js
Wee.history.go({
    path: '/page/path',
    partials: '.element',
    request: {
        complete: function() {
            // Complete logic
        }
    }
});
```

## Init

Set the initial state and popstate event, and bind global actions

|Variable|Type  |Default |Description            |Required|
|--------|------|--------|-----------------------|--------|
|options |object|-       |Object properties below|-       |

### Options

|Variable     |Type                           |Default      |Description                                                     |Required|
|-------------|-------------------------------|-------------|----------------------------------------------------------------|--------|
|bind         |object, boolean                |-            |[Bind object format](/script/history#bind)                      |-       |
|extensions   |array                          |-            |Whitelist of path extensions to support                         |-       |
|partials     |[selection](/script/#selection)|'title, main'|Elements to replace from response                               |-       |
|processErrors|boolean                        |false        |Process replacements on error responses                         |-       |
|push         |boolean                        |true         |Push the path to the browser URL                                |-       |
|request      |object                         |-            |Pass-through object to [Wee.data](/script/data#request)         |-       |
|run          |boolean                        |true         |Evaluate routing rules                                          |-       |
|begin        |object                         |-            |Before request is made                                          |-       |
|replace      |object                         |-            |Manipulations to returned html can be made here before replacement|-     |

### Default

```js
Wee.history.init();
```

### Advanced

```js
Wee.history.init({
    bind: {
        click: 'a:not([data-static])'
    },
    extensions: [
        'html',
        'php',
    ],
    partials: 'title, .js-sidebar, ref:inner',
    processErrors: true,
    request: {
        root: '/pjax',
        success: function() {
            ga('send', 'pageview');
        }
    }
});
```

### Lifecycle

The following events are available in this order at different stages throughout the History lifecycle.

```js
options.begin(config); // return false to abort process
```

```js
options.replace(html); // before replacement is made
```

```js
options.request.send(); // before actual request is made
```

```js
options.request.success(data); // logic to execute on if request is successful
```

```js
options.request.error(xhr); // logic for handling errors returned during request
```

```js
options.request.complete(xhr); // logic to remove any css modifer classes
```

```js
options.pushstate({
    dir: [-1, 1],
    path: 'string',
    prev: 'string'
});
```

```js
options.popstate({
    dir: [-1, 1],
    path: 'string',
    prev: 'string'
});
```

```js
options.complete({
    dir: [-1, 1],
    path: 'string',
    prev: 'string'
});
```

## Lifecycle

The following events are available in this order at different stages throughout the History lifecycle.

All examples below could use `Wee.history.go` as well.

### Begin

Triggers before any history state or data request occurs. Returning false will halt process entirely.

```js
Wee.history.init({
    ...
    begin: function(config) {
        // config is the entire configuration object passed into init method
    }
});
```

### Send

Triggers when data request is initially sent.

```js
Wee.history.init({
    ...
    request: {
        send: function() {
            //...
        }
    }
});
```

### Replace

Triggers once HTML from data request is received but before the received markup is placed onto the DOM. Returned HTML is passed as parameter to this method. The return value will be treated as the HTML to be appended to DOM. If return value is `js false`, HTML will be prevented from being appended.

```js
Wee.history.init({
    ...
    replace: function(html, config) {
        //...optionally modify htmlreturn html;
    }
});
```

### Success

Triggers when the data request is returned successfully and after markup has been replaced on DOM.

```js
Wee.history.init({
    ...
    request: {
        success: function(html, xhr) {
            //...
        }
    }
});
```

### Error

Triggers when the data request is not returned successfully.

```js
Wee.history.init({
    ...
    request: {
        error: function(xhr) {
            //...
        }
    }
});
```

### Complete

Triggers when the data request is returned successfully and after either the success or error callback fires.

```js
Wee.history.init({
    ...
    request: {
        complete: function(xhr) {
            //...
        }
    }
});
```

### Pushstate

Triggers when new history entry is added to browser history.

```js
Wee.history.init({
    ...
    push: true, // Default is true
    pushstate: function(history) {
        history.dir // Browser navigation direction (1)
        history.path // New URL path
        history.prev // Old URL path
    }
});
```

### Popstate

Triggers when a history entry is changed.

```js
Wee.history.init({
    ...
    pop: true,
    popstate: function(history) {
        history.dir // Browser navigation direction (-1 or 1)
        history.path // New URL path
        history.prev // Old URL path
    }
});
```

### End

Triggers at the very end of process.

```js
Wee.history.init({
    ...
    end: function(history) {
        history.dir // Browser navigation direction (-1 or 1)
        history.path // New URL path
        history.prev // Old URL path
    }
});
```