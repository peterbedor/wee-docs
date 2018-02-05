# View

Powerful template rendering engine for dynamic data

Views provide a powerful way to inject data into complex strings and markup structures. With a powerful API you can extend the default [helpers](/script/view#helpers) for infinite possibilities.

## addView

Add views to store for on-demand reference

|Variable|Type    |Default |Description|Required|
|--------|--------|--------|-----------|--------|
|name    |string  |-       |View name  |✔       |
|value   |string  |-       |View valu  |✔       |

```js
Wee.view.addView('copyright', '<small>&copy; {{ year }}</small>');
```

```js
var template = '{{> copyright }}',
    data = {
        year: 2015
    };

Wee.view.render(template, data)
```

```js
"<small>&copy; 2015</small>"
```

You can also add views to the store and then reference them when creating apps or rendering.

```js
Wee.view.addView('viewName', 'My name is {{ firstName }} {{ lastName }}');
```

```js
Wee.view.render('viewName', {
    firstName: 'Don',
    lastName: 'Draper'
});
```

```js
Wee.app.make('appName', {
    view: 'viewName',
    model: {
        firstName: 'Don',
        lastName: 'Draper'
    }
});
```

## Helpers

Add helper to run additional processing on tag data

## Render

Parse data into template string

|Variable|Type    |Default |Description    |Required|
|--------|--------|--------|---------------|--------|
|template|string  |-       |Template string|✔       |
|data    |object  |-       |Data object    |✔       |

### Simple

```js
var template = 'My name is {{ firstName }} {{ lastName }}',
    data = {
        firstName: 'John',
        lastName: 'Smith'
    };

Wee.view.render(template, data);
```

```js
"My name is John Smith"
```

### Fallback Values

```js
var template = 'My name is {{ firstName }} {{ lastName| |'Doe' }}',
    data = {
        firstName: 'John'
    };

Wee.view.render(template, data);
```

```js
"My name is John Doe"
```

### Changing Context

```js
var template = '{{ #child }}{{ #child }}{{ name }}\'s dad is {{ ../name }} and his grandad is {{ $root.name }}.{{ /child }}{{ /child }}',
    data = {
        name: 'John',
        child: {
            name: 'Jimmy',
            child: {
                name: 'Charlie'
            }
         }
    };

Wee.view.render(template, data);
```

```js
"Charlie's dad is Jimmy and his grandad is John."
```

### Helpers

```js
var template = 'My name is {{ firstName }}{{ #lastName|notEmpty }} {{ lastName }}{{ /lastName }}',
    data = {
        firstName: 'John',
        lastName: 'Smith'
    };

Wee.view.render(template, data);
```

```js
"My name is John Smith"
```

### Loop Variables

Within tag pairs there are a handful of variables made available automatically.

- {{ $key }} - The key when iterating over an object
- {{ . }} - The single currently iterated value
- {{ # }} - Zero-based loop index
- {{ ## }} - One-based loop index

```js
var template = '{{ #names }}{{ # }} | {{ ## }} | {{ . }} | {{ $key }}<br>{{ /names }}',
    data = {
        names: {
            'John': 45,
            'Jane': 42,
            'Jimmy': 18,
            'Jenny': 15
        }
    };

Wee.view.render(template, data);
```

```js
0 | 1 | 45 | John<br>
1 | 2 | 42 | Jane<br>
2 | 3 | 18 | Jimmy<br>
3 | 4 | 15 | Jenny<br>
```

### Advanced

The render method does more than simple variable output. It can traverse as deep into the provided object as you need for multi-level output.

```js
var template = '<p>My Name is {{ firstName }}{{ #lastName|notEmpty }} {{ lastName }}{{ /lastName }}</p>' +
    '{{ #children|notEmpty }}' +
        '<p>My Children are:</p>' +
        '<ul>{{ #.|each }}' +
            '<li>{{ name }} - {{ age }}</li>' +
        '{{ /. }}</ul>' +
    '{{ else }}' +
        '<p>I have no children.</p>' +
    '{{ /children }}',
    data = {
        firstName: 'John',
        lastName: 'Smith',
        children: [
            {
                name: 'Judy',
                age: '12'
            },
            {
                name: 'James',
                age: '9'
            }
        ]
    };

Wee.view.render(template, data);
```

```html
<p>My Name is John Smith</p>
<p>My Children are:</p>
<ul>
	<li>Judy - 12</li>
	<li>James - 9</li>
</ul>
```