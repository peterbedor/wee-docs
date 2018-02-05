# Routes

Associate request endpoints to callbacks

Routes create independence between your markup and JavaScript.  It also allows us to easily integrate [HTML5 History](https://developer.mozilla.org/en-US/docs/Web/API/History).  Wee routing serves as the blueprint for your project's JavaScript.

## addFilter

Add conditional route filter

|Variable|Type          |Default |Description                         |Required|
|--------|--------------|--------|------------------------------------|--------|
|a       |object, string|-       |Multiple filter object or filter key|✔       |
|b       |function      |-       |Filter function                     |-       |

### Single

```js
Wee.routes.addFilter('isInternal', function(seg) {
    return ['admin', 'protected'].indexOf(seg) > -1;
});
```

### Multiple

```js
Wee.routes.addFilter({
    isInternal: function(seg) {
        return ['admin', 'protected'].indexOf(seg) > -1;
    },
    isExternal: function(seg) {
        return ['admin', 'protected'].indexOf(seg) < 0;
    }
});
```

## Filters

Included route filters

### Once

Evaluate the route only once.

```js
Wee.routes.map({
    '$any:once': 'common'
});
```

### Fire

Moves the route to the top of the evaluation order.

```js
Wee.routes.map({
    '$any:fire': 'common'
});
```

### Unload

Evaluates when navigating away from a route with [Wee.history](/script/history). A common use-case for this filter is to manage in-memory objects and unbind page-specific events when navigating away from a page to prevent memory leaks.

```js
Wee.routes.map({
    '$any:unload': 'common:unload'
});
```

### Pop

Evaluates when a history entry is changed. This will be triggered by doing a browser action such as a click on the back or forward button, or by calling history.back() or history.forward().

```js
Wee.routes.map({
    '$any:pop': 'common:pop'
});
```

### Eval

Move the segment pointer back one level.

```js
Wee.routes.map({
    '$customFilter:eval': {
        '$any': 'common',
        'products': 'products'
    }
});
```

### !

Negates route if prefixed by `js !`.

```js
Wee.routes.map({
    '!about': 'common'
});
```

## Map

Retrieve or add route endpoints to route storage

|Variable|Type    |Default |Description                |Required|
|--------|--------|--------|---------------------------|--------|
|a       |object  |-       |Mapping object             |-       |
|init    |boolean |false   |Immediately evaluate routes|-       |

### Set

Arguments can be nested as deep as necessary. Pass true as the second argument to immediately evaluate the specified routes from the first argument.

```js
Wee.routes.map({
    '$any': 'common',
    'script': {
        'routes': function() {
            // Current page
        }
    }
});
```

If using the `wee:fn`` format to call an init method you can exclude`:init` as it is assumed if no function is provided.

### Get

Retrieve all the routes currently in storage.

```js
Wee.routes.map();
```

```js
{
    "$any": "common",
    "script": {
        "routes": function(){}
    }
}
```

### Advanced

```js
Wee.routes.map({
    '$root': function(val) {
        console.log('root ' + val);
    },
    '$any': function() {
        console.log('root any');
    },
    'category': {
        '$root||$/^P[\\d]+$/': function(val) {
            console.log(val + ' root');
        },
        '$any': function() {
            console.log('category any');
        },
        'mens': function() {
            console.log('mens!');
        },
        '$/^(?!P[\\d]+).*$/': {
            '$root': function(cat) {
                console.log(cat + ' listing');
            },
            '$num': function(id) {
                console.log('product ID is ' + id);
            }
        }
    }
});

Wee.ready(function() {
    Wee.routes.run({
        path: 'category/name/123'
    });
});
```

## Run

Process stored route options with optional config

|Variable|Type    |Default |Description            |Required|
|--------|--------|--------|-----------------------|--------|
|options |object  |-       |Object parameters below|-       |

### Options Object

|Variable|Type    |Default |Description                   |Required|
|--------|--------|--------|------------------------------|--------|
|path    |string  |-       |Relative path from root domain|-       |
|routes  |object  |-       |Mapping object                |-       |

Without arguments, the currently bound path and routes will be evaluated.

```js
Wee.routes.run();
```

### Advanced

If an object is provided, only the passed routes will be evaluated.

```js
Wee.routes.run({
    routes: {
        '$any': 'common:init',
        'script': {
            'routes': function() {
                // Current page
            }
        }
    },
    path: '/script/routes'
});
```

## Segments

Get all segments or single segment at index

|Variable|Type    |Default |Description             |Required|
|--------|--------|--------|------------------------|--------|
|index   |integer |-       |Zero-based segment index|-       |

### Get all

Retrieve segment array from the currently bound path.

```js
Wee.routes.segments();
```

```js
["script", "routes"]
```

### Get single

Get single segment by defining zero-based index.

```js
Wee.routes.segments(1);
```

```js
"routes"
```

## URI

Get currently bound URI values or set URI data with a specified string or value object

|Variable|Type           |Default |Description            |Required|
|--------|---------------|--------|-----------------------|--------|
|value   |string, object |-       |Object parameters below|-       |

### Value Object

|Variable|Type    |Default |Description        |Required|
|--------|--------|--------|-------------------|--------|
|hash    |string  |-       |Hash value         |-       |
|path    |string  |-       |Relative path      |-       |
|Query   |object  |-       |Query string object|-       |

### Get

Based on “[https://www.weepower.com/script/routes?success=yes#uri](https://www.weepower.com/script/routes?success=yes#uri)” the following object would be returned.

```js
Wee.routes.uri();
```

```js
{
    hash: "uri",
    path: "/script/routes",
    query: {
        success: "yes"
    }
}
```

### Set String

The set method accepts either an absolute URL, a relative path, or just a #hash.

```js
Wee.routes.uri('another/page');
```

### Set Object

Only the properties you wish to update should be provided. They will be merged into the current values.

```js
Wee.routes.uri({
    hash: 'uri',
    path: '/script/routes',
    query: {
        success: 'yes'
    }
});
```

Setting the URI only updates the internal reference. It doesn’t navigate the page.