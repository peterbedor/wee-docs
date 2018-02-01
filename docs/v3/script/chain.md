# Chain

Wee allows many methods to be chained to selectors by omitting the first argument of the method. This often makes code more readable and permits multiple methods to be executed on the same selection.

## Animate

[$(sel).tween(values, options)](/docs/v3/script/animate?id=#tween)

In this example, the target is faded out to full transparency.

```js
    $('ref:element').tween({
        opacity: 0
    }, {
        duration: 600
    });
	```

## Core

[$(sel, context)](/docs/v3/script/script/core?id=#sel)

[$(sel).each(fn, options)](/docs/v3/script/core?id=##each)

[$(sel).map(fn, options)](/docs/v3/scriptscript/core?id=##map)

[$(sel).setRef()](/docs/v3/scriptscript/core?id=##setref)

[$(sel).setVar()](/docs/v3/script/core?id=#setvar)

### Reverse

The reverse method simply reverses the order of the selection results.

```js
    $('.element').reverse();
```

### toArray

Convert a Wee selection to a simple array
```js
    $('.element').toArray();
```

## DOM

- [$(sel).addClass(value)](/docs/v3/script/dom?id=addclass)
- [$(sel).after(source, remove)](/docs/v3/script/dom?id=after)
- [$(sel).append(source)](/docs/v3/script/dom?id=append)
- [$(sel).appendTo(target)](/docs/v3/script/dom?id=appendto)
- [$(sel).attr(a, b)](/docs/v3/script/dom?id=attr)
- [$(sel).before(source, remove)](/docs/v3/script/dom?id=before)
- [$(sel).children(filter)](/docs/v3/script/dom?id=children)
- [$(sel).clone()](/docs/v3/script/dom?id=clone)
- [$(sel).closest(filter, context)](/docs/v3/script/dom?id=closest)
- [$(sel).contains(descendant)](/docs/v3/script/dom?id=contains)
- [$(sel).contents()](/docs/v3/script/dom?id=contents)
- [$(sel).css(a, b)](/docs/v3/script/dom?id=css)
- [$(sel).data(a, b)](/docs/v3/script/dom?id=data)
- [$(sel).empty()](/docs/v3/script/dom?id=empty)
- [$(sel).eq(index, context)](/docs/v3/script/core?id=eq)
- [$(sel).filter(filter, options)](/docs/v3/script/dom?id=filter)
- [$(sel).find(filter)](/docs/v3/script/dom?id=find)
- [$(sel).first()](/docs/v3/script/core?id=first)
- [$(sel).get(index)](/docs/v3/script/core?id=eq)
- [$(sel).hasClass(className)](/docs/v3/script/dom?id=hasclass)
- [$(sel).height(value)](/docs/v3/script/dom?id=height)
- [$(sel).hide()](/docs/v3/script/dom?id=hide)
- [$(sel).html(value)](/docs/v3/script/dom?id=html)
- [$(sel).index()](/docs/v3/script/dom?id=index)
- [$(sel).insertAfter(target)](/docs/v3/script/dom?id=insertafter)
- [$(sel).insertBefore(target)](/docs/v3/script/dom?id=insertbefore)
- [$(sel).is(filter, options)](/docs/v3/script/dom?id=is)
- [$(sel).last(context)](/docs/v3/script/dom?id=last)
- [$(sel).next(filter, options)](/docs/v3/script/dom?id=next)
- [$(sel).not(filter, options)](/docs/v3/script/dom?id=not)
- [$(sel).offset(value)](/docs/v3/script/dom?id=offset)
- [$(sel).parent(filter)](/docs/v3/script/dom?id=parent)
- [$(sel).parents(filter)](/docs/v3/script/dom?id=parents)
- [$(sel).position()](/docs/v3/script/dom?id=position)
- [$(sel).prepend(source)](/docs/v3/script/dom?id=prepend)
- [$(sel).prependTo(target)](/docs/v3/script/dom?id=prependto)
- [$(sel).prev(filter, options)](/docs/v3/script/dom?id=prev)
- [$(sel).prop(a, b)](/docs/v3/script/dom?id=prop)
- [$(sel).remove(context)](/docs/v3/script/dom?id=remove)
- [$(sel).removeAttr(name)](/docs/v3/script/dom?id=removeattr)
- [$(sel).removeClass(value)](/docs/v3/script/dom?id=removeclass)
- [$(sel).replaceWith(source)](/docs/v3/script/dom?id=replacewith)
- [$(sel).scrollLeft(value)](/docs/v3/script/dom?id=scrollleft)
- [$(sel).scrollTop(value)](/docs/v3/script/dom?id=scrolltop)
- [$(sel).serialize(json)](/docs/v3/script/dom?id=serializeform)
- [$(sel).show()](/docs/v3/script/dom?id=show)
- [$(sel).siblings(filter)](/docs/v3/script/dom?id=siblings)
- [$(sel).slice(start, end)](/docs/v3/script/dom?id=slice)
- [$(sel).text(value)](/docs/v3/script/dom?id=text)
- [$(sel).toggle()](/docs/v3/script/dom?id=toggle)
- [$(sel).toggleClass(className, state)](/docs/v3/script/dom?id=toggleclass)
- [$(sel).val(value)](/docs/v3/script/dom?id=val)
- [$(sel).width(value)](/docs/v3/script/dom?id=width)
- [$(sel).wrap(html)](/docs/v3/script/dom?id=wrap)
- [$(sel).wrapInner(html)](/docs/v3/script/dom?id=wrapinner)

### Add

You can join selections using the add method.

```js
$('.element').add('ref:selection').hide();
```

### Example

DOM traversal is made easy with chaining.

```html
    <ul>
		<li>One</li>
		<li>Two</li>
		<li>Three</li>
	</ul>
```
```js
    $('li').eq(1).text();
```

## Events

- [$(sel).on(a, b, c)](https://www.weepower.com/script/events#on)

- [$(sel).off(a, b)](https://www.weepower.com/script/events#off)

- [$(sel).bound(event, fn)](https://www.weepower.com/script/events#bound)

- [$(sel).trigger(name)](https://www.weepower.com/script/events#trigger)

In this example, the selector is the element to which the event is bound.

```js
    $('.element').on('click', function() {
        // Click logic
    });
	```

Here the event is being triggered on the selector.

```js
    $('.element').trigger('click');
```

## Register

To register a new chainable method follow the pattern below.

```js
    Wee.$chain('setId', function(id) {
        this.attr('id', id);

        returnthis;
    });
```

Alternatively you can register methods in a jQuery-compatible syntax.

```js
    $.fn.setId = function(id) {
        this.data('id', id);

        returnthis;
    };
```

To execute the method use the following.

```js
    $('.element').setId(3).show();
```

Be sure to return `this` at the end of your method if the function’s purpose is not to return another value. This ensures the chain can continue.

## Shortcuts

All the core and DOM methods prefixed with `$` are shortcut when chaining is enabled. Just remove the method’s dollar sign and replace `Wee` with `$`.

### Examples
```js
    $.unique([1, 2, 2, 3]);
    $.get('key');
    $.height('ref:element');
```

## View

- [$(sel).render(data)](https://www.weepower.com/script/view#render)

The view chain method updated the content of a DOM element given a data object.

```html
    <div class="element">
		<span class="{{ className }}">{{ content }}</span>
	</div>
```

```js
$('.element').render({
    className: 'dynamic-class',
    content: 'Span contents'
});
```
