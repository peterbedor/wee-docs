# Events

Event binding to attach functionality to elements

Create organized interaction on your page with Wee’s simple event API. Support for mouseenter and mouseleave is baked in.

## $events.addEvent

Add a custom event

| Variable | Type     | Default | Description      | Required |
|----------|----------|---------|------------------|----------|
| name     | string   | -       | Event name       | ✔        |
| on       | function | -       | Enable function  | ✔        |
| off      | function | -       | Disable function | ✔        |

```js
import $events from'wee-events';

$events.addEvent('pressHold', function(el, fn, conf) {
    let scope = this;
    let duration = conf.duration || 400;

    $events.on(el, 'mousedown.pressHold', (e, el) => {
        scope.timer = setTimeout(function() {
            scope.timer = false;

            fn.apply(conf.scope || el, W._slice.call(arguments));
        }, duration);
    }, conf);

    $.on(el, 'mouseup.pressHold', () => {
        if (scope.timer) {
            clearTimeout(scope.timer);
        }
    });
}, (el, fn) => {
    $events.off(el, 'mouseup.pressHold', fn);
});

$events.on('ref:element', 'pressHold', (e, el) => {
    // Trigger logic
});
```

## $events.bound

Get currently bound events to optional specified element, event, and function

| Variable | Type                               | Default | Description         | Required |
|----------|------------------------------------|---------|---------------------|----------|
| target   | [selection](/script/dom#selection) | -       | Target selection    | -        |
| event    | string                             | -       | Specific event name | -        |
| fn       | function                           | -       | Specific callback   | -        |

By default bound will return all bound events.

```js|js
import $events from'wee-events';

$events.bound();

---

[Object, Object, ...]
```

### Selection

```js|js
$bound('ref:element');

---

[Object, Object, ...]
```

### @election Event

```js|js
$bound('ref:element', 'click');

---

[Object, Object, ...]
```

## $events.off

Remove specified function to specified element and optional event and function

| Variable | Type                           | Default | Description                    | Required |
|----------|--------------------------------|---------|--------------------------------|----------|
| target   | [selection](/script#selection) | -       | Target selection               | ✔        |
| a        | string                         | -       | Event name or object of events | -        |
| b        | [function](/script#functions)  | -       | Callback to remove             | -        |

### Target

If no event or callback is provided all element events will be removed.

```js
import $events from'wee-events';

$events.off('ref:element');
```

### Selection Event

```js
import $events from'wee-events';

$off('ref:element', 'click');
```

### Selection Event Callback

```js
import $events from'wee-events';

$events.off('ref:element', 'click', (e, el) => {
    // Click logic
});
```

### Multiple Selections

```js
import $events from'wee-events';

$events.off({
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
import $events from 'wee-events';

$events.off(false, '.namespace');
```

## $events.on

Bind specified function to specified element and event

| Variable | Type                               | Default | Description                      | Required |
|----------|------------------------------------|---------|----------------------------------|----------|
| target   | [selection](/script/dom#selection) | -       | Target selection                 | ✔        |
| a        | string, object                     | -       | Event name or object of events   | ✔        |
| b        | function, object                   | -       | Event callback or options object | -        |
| c        | object                             | -       | Option parameters below          | -        |

| Variable  | Type                               | Default | Description                            | Required |
|-----------|------------------------------------|---------|----------------------------------------|----------|
| args      | array                              | -       | Callback arguments                     | -        |
| context   | [selection](/script/dom#selection) | -       | Context selection                      | -        |
| delegate  | [selection](/script/dom#selection) | -       | Delegate selection                     | -        |
| namespace | string                             | -       | Apply namespace to all events          | -        |
| once      | boolean                            | false   | Remove the event after first execution | -        |
| scope     | object                             | -       | Callback scope                         | -        |

### Simple

```js
import $events from 'wee-events';

$events.on('ref:element', 'click', (e, el) => {
    // Click logic
    e.preventDefault();
});
```

### Once

```js
import $events from 'wee-events';

$events.on('ref:element', 'click', (e, el) => {
    // Click logic
    e.preventDefault();
}, {
    once: true,
});
```

### Delegation

```js
import $events from 'wee-events';

$events.on('.js-descendant', 'click', (e, el) => {
    // Click logic
    e.preventDefault();
}, {
    delegate: 'ref:element',
});
```

### Multiple Events

```js
import $events from'wee-events';

$events.on('ref:element', {
    click() {
        // Click logic
    },
    blur() {
        // Blur logic
    },
});
```

### Multiple Selections

```js
import $events from 'wee-events';

$events.on({
    'ref:element': {
        mouseenter() {
            // Enter logic
        }
    },
    '.js-element': {
        click(e, el) {
            // Click logic
            e.preventDefault();
        }
    }
});
```

### Namespacing

Events can be namespaced by appending ‘.namespace’ to the end of the event name. Namespaced events can then be selected, modified, and destroyed as a group.

```js
import $events from 'wee-events';

$events.on('ref:element', 'click.namespace', (e, el) => {
    // Click logic
    e.preventDefault();
});
```

```js
import $events from 'wee-events';

$events.on({
    'ref:element': {
        click(e, el) {
        // Click logic
        e.preventDefault();
    },
    '.js-element': {
        click(e, el) {
            // Click logic
            e.preventDefault();
        }
    }
}, {
    namespace: 'namespace',
});
```

## $events.trigger

Execute event for each matching selection

| Variable | Type                               | Default | Description      | Required |
|----------|------------------------------------|---------|------------------|----------|
| target   | [selection](/script/dom#selection) | -       | Target selection | ✔        |
| event    | string                             | -       | Event name       | ✔        |

```js
import $events from'wee-events';

$events.trigger('ref:element', 'click');
```
