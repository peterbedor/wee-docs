# Animate

Smoothly transition attribute or property values

While CSS animation is typically preferred for supported transitions, sometimes JavaScript is necessary for tweening certain attributes or properties. Wee gives you the bare minimum to make that happen.

## addEasing

Add additional easing function(s)

|Variable|Type          |Default |Description                       |Required|
|--------|--------------|--------|----------------------------------|--------|
|a       |object, string|-       |Multiple ease object or easing key|✔       |
|b       |function      |-       |Easing function                   |-       |

### Single

```js
Wee.animate.addEasing('split', function(t) {
    return t / 2;
});
```
### Multiple

```js
Wee.animate.addEasing({
    split: function(t) {
        return t / 2;
    },
    slow: function(t) {
        return t < 1 ? 1 : (t / 3);
    }
});
```

## Tween

Transition an attribute or property value

|Variable|Type                          |Default |Description                                 |Required|
|--------|------------------------------|--------|--------------------------------------------|--------|
|target  |[selection](/script#selection)|-       |Target selection                            |	✔      |
|props   |object                        |-       |Key/value object of attributes or properties| ✔	   |
|options |object                        |-       |Object parameters below                     |-       |

### Options Object

|Variable|Type                         |Default |Description                               |Required|
|--------|-----------------------------|--------|------------------------------------------|--------|
|complete|[function](/script#functions)|-       |Callback function                         |-       |
|duration|number                       |400     |Transition duration in milliseconds       |        |
|ease    |string                       |'ease'  |ease, linear, or name of registered easing|        | 

### Simple

```js
Wee.animate.tween('ref:element', {
    height: 200
});
```

### Advanced

```js
Wee.animate.tween('ref:element', {
    height: 200,
    marginTop: 100
}, {
    duration: 500,
    ease: 'linear',
    complete: function() {
        // Complete logic
    }
});
```

If no unit is provided then pixel values will be assumed when tweening CSS attributes.