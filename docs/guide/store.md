# Store

[local-storage]: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
[session-storage]: https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage

The store module is for managing data in an application. It is not intended to drive an entire single page application. Instead, it is meant to organize and improve a standard website by making common data shareable across a codebase without contaminating the global namespace. It also allows for easy integration with [LocalStorage][local-storage] and [SessionStorage][session-storage].

```javascript
import $store from 'wee-store';

$store.set('globalProp', true);
$store.get('globalProp'); // true
```

## Using markup to set variables

With any website that is serving only static HTML files, it is a common need to provide data to our JavaScript directly from our markup. Wee has a specific convention for this use-case:

```html
<html>
	<head></head>
	<body>
	  <meta data-set="prop" data-value="test">
	</body>
</html>
```

Any element on the DOM may be given a `data-set` and `data-value` attribute. This will set a property in the store module called `prop` with the value of `test`. You could then access that property like this:

```javascript
import $store from 'wee-store';

$store.setVar();

let prop = $store.get('prop');
console.log(prop); // 'test'
```

You'll notice how we executed `setVar` in the example above. That is how our JavaScript knows to look through the DOM and find these `data-set` and `data-value` pairs, converting those to variables in our `store` module. `setVar` is executed by default in our `bootstrap` module that is imported in Wee's default entry point `app.js`. If you have a custom entry point for your application, make sure to import `bootstrap` or call `setVar` before trying to access those properties.

## Store scope

The default import for the `store` module is an instance of the `Store` class. This means that we can create any number of new `store` instances that can be used however you desire.

```javascript
import $store from 'wee-store';

$store.set('globalProp', true);
$store.get('globalProp'); // true

const $local = $store.create('local'); // returns instance of Store

$local.set('localProp', true);
$local.get('localProp'); // true
$local.get('globalProp'); // undefined
```

It is important to note that `setVar` will set properties on the main `store` module by default. In order to store properties on a custom `store` instance, you need to add another attribute to your markup:

```html
<meta data-store="local" data-set="prop" data-value="test">
```

Adding the `data-store` attribute to the example will reserve that property for when `setVar` is called on the `store` instance with the name of `local`.

## Local and Session Storage

The store module can utilize either [LocalStorage][local-storage] or [SessionStorage][session-storage] to persist data. When using this feature, there are a few things to keep in mind.

By default, all data added to a `store` instance will be saved in JavaScript, regardless of whether local or session storage is activated on that instance. This is to keep everything functioning as fast as possible. If it is not desirable to house all data in JavaScript, setting `keepInMemory` to `false` will cause the `store` instance to retrieve data directly from local/session storage anytime `$store.get` is called which will be less performant. This may be a preferable option if there is a large-ish (local and session storage limits can be as low as 2mb on certain mobile devices) amount of data in a `store` instance that will be retrieved infrequently. Otherwise, it is best to leave the default settings alone.
