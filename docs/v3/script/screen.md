# Screen

Attach events to matching breakpoint rules

Syncing media queries and JavaScript reliably can be tedious. Wee seamlessly combines and triggers breakpoint logic based on your configured project media queries.

## Values

You can easily disable any unneeded breakpoints by setting them to false in wee.json.

1. Portrait Mobile (320px)
2. Landscape Mobile (480px)
3. Portrait Tablet (768px)
4. Small Desktop (1024px)
5. Medium Desktop (1280px)
6. Large Desktop (1440px)

Wee uses the font family of the HTML element to reference the current breakpoint. You can add additional custom values by setting the value to a numeric string in your CSS. This would typically be done in a custom media query.

```css
@media (max-width: 600px) {
    html {
        font-family: '1.5';
    }
}
```

## Map

Watch single or set of screen events with specified options

|Variable|Type         |Default |Description            |Required|
|--------|-------------|--------|-----------------------|--------|
|sets    |object, array|-       |Object parameters below|✔		 |

### Set Object

|Variable |Type                         |Default |Description                                  |Required|
|---------|-----------------------------|--------|---------------------------------------------|--------|
|args     |array                        |-       |Callback arguments                           |-       |
|callback |[function](/script#functions)|-       |Matching callback                            |✔       |
|each     |boolean                      |false   |Execute callback for each matching breakpoint|-       |
|init     |boolean                      |true    |Immediately evaluate breakpoint logic        |-       |
|max      |number                       |-       |Maximum breakpoint value                     |-       |
|min      |number                       |-       |Minimum breakpoint value                     |-       |
|namespace|string                       |-       |Event namespace for granular resetting       |-       |
|once     |boolean                      |false   |Disable callback after first execution       |-       |
|scope    |object                       |-       |Callback scope                               |-       |
|size     |number                       |-       |Specific breakpoint value                    |-       |
|watch    |boolean                      |true    |Evaluate on screen size                      |-       |

You can setup as many breakpoint sets as you need. They are added to a global window resize event that evaluates once against all stored rules.

### Single

```js
Wee.screen.map({
    size: 4,
    callback: function(obj) {
        console.log(obj);
    }
});
```

An object with the direction, size, previous size, and init status is passed as the first callback argument.

|Variable|Type    |Default |Description                      |Required|
|--------|--------|--------|---------------------------------|--------|
|dir     |number  |-       |1 if sized up, 0 if sized down   |-       |
|init    |boolean |-       |true if run initially, else false|-       |
|prev    |number  |-       |1-6 representing previous value  |-       |
|size    |number  |-       |1-6 representing current value   |-       |

### Multiple

```js
Wee.screen.map([
    {
        size: 1,
        callback: [
            'common:mobile',
            'common:smallScreen'
        ]
    },
    {
        min: 3,
        max: 4,
        watch: false,
        callback: 'common:mediumScreen'
    },
    {
        min: 5,
        args: ['passThrough'],
        callback: function(obj, val) {
            console.log(val); // passThroughconsole.log(obj);
        }
    }
]);
```

## Reset

Reset all bound events

|Variable |Type    |Default |Description                 |Required|
|---------|--------|--------|----------------------------|--------|
|namespace|string  |-       |Namespace of events to reset|-       |

```js
Wee.screen.reset();
```

## Run

Evaluate the current breakpoint

```js
Wee.screen.run();
```

## Size

Get current screen value

The value is determined by the value of the HTML element font family which stores the current media query number. The response falls between 1 and 6.

```js
Wee.screen.size();
```

```js
5
```