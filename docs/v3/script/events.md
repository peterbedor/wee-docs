# Events

Event binding to attach functionality to elements

Create organized interaction on your page with Wee’s simple event API. Support for mouseenter and mouseleave is baked in.

## addEvent

Add a custom event

|Variable|Type    |Default |Description     |Required|
|--------|--------|--------|----------------|--------|
|name    |string  |-       |Event name      |✔       |
|on      |function|-       |Enable function |✔       |
|off     |function|-       |Disable function|✔       |

```js
Wee.events.addEvent('pressHold', function(el, fn, conf) {
    var scope = this,
        duration = conf.duration || 400;

    Wee.events.on(el, 'mousedown.pressHold', function(e, el) {
        scope.timer = setTimeout(function() {
            scope.timer = false;

            fn.apply(conf.scope || el, W._slice.call(arguments));
        }, duration);
    }, conf);

    Wee.events.on(el, 'mouseup.pressHold', function() {
        if (scope.timer) {
            clearTimeout(scope.timer);
        }
    });
}, function(el, fn) {
    Wee.events.off(el, 'mouseup.pressHold', fn);
});

$('ref:element').on('pressHold', function(e, el) {
    // Trigger logic
});
```

## Bound

Get currently bound events to optional specified element, event, and function

|Variable|Type                          |Default |Description      |Required|
|--------|------------------------------|--------|-----------------|--------|
|target  |[selection](/script#selection)|-       |Target selection |-       |
|event   |string|-|Specific event name  |-       |-                |-       |
|fn      |[function](/script#functions) |-       |Specific callback|-       |

By default bound will return all bound events.

```js
Wee.events.bound();
```

```js
[Object, Object, ...]
```

### Selection

```js
Wee.events.bound('ref:element');
```

```js
[Object, Object, ...]
```

### Selection Event

```js
Wee.events.bound('ref:element', 'click');
```

```js
[Object, Object, ...]
```

## Off

Remove specified function to specified element and optional event and function

|Variable|Type                          |Default |Description                   |Required|
|--------|------------------------------|--------|------------------------------|--------|
|target  |[selection](/script#selection)|-       |Target selection              |✔       |
|a       |string                        |-       |Event name or object of events|-       |
|b       |[function](/script#functions) |-       |Callback to remove            |-       |

### Target

If no event or callback is provided all element events will be removed.

```js
Wee.events.off('ref:element');
```

### Selection Event

```js
Wee.events.off('ref:element', 'click');
```

### Selection Event Callback

```js
Wee.events.off('ref:element', 'click', function(e, el) {
    // Click logic
});
```

### Multiple Selections

```js
Wee.events.off({
    'ref:element': {
        mouseenter: function() {
            // Enter logic
        }
    },
    '.js-element': {
        click: function(e, el) {
            // Click logic
            e.preventDefault();
        }
    }
});
```

### Global

You can remove entire groups of namespaced events.

```js
Wee.events.off(false, '.namespace');
```

## On

Bind specified function to specified element and event

|Variable|Type                                 |Default |Description                     |Required|
|--------|-------------------------------------|--------|--------------------------------|--------|
|target  |[selection](/script#selection)       |-       |Target selection                |✔	      |
|a       |string, object                       |-       |Event name or object of events  |✔		  |
|b       |[function](/script#functions), object|-       |Event callback or options object|-       |
|c       |object                               |-       |option parameters below         |-       |

|Variable |Type                          |Default |Description                           |Required|
|---------|------------------------------|--------|--------------------------------------|--------|
|args     |array                         |-       |Callback arguments                    |-       |
|context  |[selection](/script#selection)|-       |Context selection                     |-       |
|delegate |[selection](/script#selection)|-       |Delegate selection                    |-       |
|namespace|string                        |-       |Apply namespace to all events         |-       |
|once     |boolean                       |false   |Remove the event after first execution|-       |
|scope    |object                        |-       |Callback scope                        |-       |

### Simple

```js
Wee.events.on('ref:element', 'click', function(e, el) {
    // Click logic
    e.preventDefault();
});
```

### Once

```js
Wee.events.on('ref:element', 'click', function(e, el) {
    // Click logic
    e.preventDefault();
}, {
    once: true
});
```

### Delegation

```js
Wee.events.on('.js-descendant', 'click', function(e, el) {
    // Click logic
    e.preventDefault();
}, {
    delegate: 'ref:element'
});
```

### Multiple Events

```js
Wee.events.on('ref:element', {
    click: function() {
        // Click logic
    },
    blur: function() {
        // Blur logic
    }
});
```

### Multiple Selections

```js
Wee.events.on({
    'ref:element': {
        mouseenter: function() {
            // Enter logic
        }
    },
    '.js-element': {
        click: function(e, el) {
            // Click logic
            e.preventDefault();
        }
    }
});
```

### Namespacing

Events can be namespaced by appending ‘.namespace’ to the end of the event name. Namespaced events can then be selected, modified, and destroyed as a group.

```js
Wee.events.on('ref:element', 'click.namespace', function(e, el) {
    // Click logic
    e.preventDefault();
});
```

```js
Wee.events.on({
    'ref:element': {
        click: function(e, el) {
        // Click logic
        e.preventDefault();
    },
    '.js-element': {
        click: function(e, el) {
            // Click logic
            e.preventDefault();
        }
    }
}, {
    namespace: 'namespace'
});
```

## Touch

Standard swipe events are available out of the box

|Variable|Type    |Default |Description                     |Required|
|--------|--------|--------|--------------------------------|--------|
|distance|integer |50      |Minimum swipe distance in pixels|-       |
|movement|integer |25      |Maximum opposing shift in pixels|-       |

The `swipeLeft`, `swipeRight`, `swipeUp`, `swipeDown` events are available and work just like standard events.

```js
Wee.on('ref:element', 'swipeRight', function() {
    // Swipe logic
}, {
    distance: 150,
    movement: 20
});
```

## Trigger

Execute event for each matching selection

|Variable|Type                           |Default |Description     |Required|
|--------|-------------------------------|--------|----------------|--------|
|target  |[selection](/script/#selection)|-       |Target selection|✔       |
|event   |string                         |-       |Event name      |-       |

```js
Wee.events.trigger('ref:element', 'click');
```