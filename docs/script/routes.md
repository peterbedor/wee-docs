# Routes

Associate request endpoints to specified application logic

Routes create independence between your markup and JavaScript.  It also allows us to easily integrate [HTML5 History](https://developer.mozilla.org/en-US/docs/Web/API/History).  Wee routing serves as the blueprint for your project's JavaScript.

## Lifecycle Methods

Lifecycle methods hook into the router and execute at key points in the route evaluation process.

The following methods can be registered in a [route handler](#route-handlers) and/or directly on [route records](#records). Lifecycle methods execute in the order that they are listed.

### Parameters

| Variable | Type     | Default | Description                                                    | Required |
|----------|----------|---------|----------------------------------------------------------------|----------|
| to       | object   | -       | Current [route match](#matches)                                | -        |
| from     | object   | -       | Previous [route match](#matches)                               | -        |
| next     | function | -       | Callback that continues route evaluation (before methods only) | -        |

### Before

The before method is available only to [route records](#records) and will execute after the route is matched and before any other registered methods are executed. This method receives a third parameter. This parameter is a function that must be executed before the other methods registered to the route will evaluate.

**Fetching Data**

Asynchronous actions can be taken from within `before`, preventing further evaluation of the matched route record until `next` is executed.

```js
import $router from 'wee-routes';
import admin from './admin';
import $fetch from 'wee-fetch';

$router.map([
    {
        path: '/admin',
        handler: admin,
        before(to, from, next) {
            $fetch('/data.json').then(() => next());
        }
    }
]).run();
```

**Guards**

Because the `next` function must be executed for evaluation of the route record to continue, before methods can act as a guard. You can halt evaluation of the route record by passing `false` to the `next` function.

```js
import $router from 'wee-routes';
import admin from './admin';

$router.map([
    {
        path: '/admin',
        handler: admin,
        before(to, from, next) {
            if (notAuthorized) {
              // Stop evaluation and go no further
              next(false);
            } else {
              // Continue
              next();
            }
        }
    }
]).run();
```

### Before Init

The beforeInit method is the same as the before method except that it is available only to [route handlers](#route-handlers). It will execute after the route is matched and before any other registered methods are executed except a before method registered on the matched [record](#records). This method fires only if the previously matched route record is different from the currently matched record.

### Before Update

The beforeUpdate method is the same as the before method except that it is available only to [route handlers](#route-handlers). It will execute after the route is matched and before any other registered methods are executed except a before method registered on the matched [record](#records). This method fires if the user navigates to the same page as they were previously.

### Init

The init method fires only if the previously matched route record is different from the currently matched record. In simpler terms, the init method fires the first time that the user visits a section of a website. This makes it easier to distinguish initialization of a page from logic that updates a page.

```js
import $router from 'wee-routes';

$router.map([
    { path: '/', init(to, from) {} }
]).run();
```

### Update

The update method fires if the user navigates to the same page as they were previously. A common example of this would be when a filter of some kind is updated by the user that changes the query string value of the URL. The same route record will match, however the page will need to be adjusted to match the constraints of the updated filter.

```js
import $router from 'wee-routes';

$router.map([
    { path: '/', init(to, from) {}, update(to, from) {} }
]).run();
```

### Unload

The unload method evaluates when navigating away from a route. This is relevant when [PJAX](#pjax) has been enabled and navigation on the site is using [History](https://developer.mozilla.org/en-US/docs/Web/API/History). In this case, we may need to clean up after ourselves to prevent a memory leak. The unload method makes it easy to do this.

This method takes either function or a namespace. If a namespace is provided, Wee will destroy anything generated or bound by `wee-events`, `wee-screen`, and `wee-store` registered with the same namespace.

```js
import $router from 'wee-routes';
import admin from './admin';
import home from './home';

$router.map([
    { path: '/admin', handler: adminHandler, unload(to, from) {} }, // Providing function
    { path: '/', handler: home, unload: 'home' } // Providing namespace
]).run();
```

### After

The after method will execute after all other methods have completed. Unlike the before method, this method is not passed a `next` function.

```js
import $router from 'wee-routes';

$router.map([
    { path: '/admin', after(to, from) {} }
]).run();
```

## Matches

A route match represents the state of the current active or previous route. This object is passed as the `to` and `from` parameters that are passed into [lifecycle methods](#methods) as well as to other configuration methods such as `scrollBehavior` and `transition`.

### Properties

| Variable   | Type   | Default | Description                                                   | Required |
|------------|--------|---------|---------------------------------------------------------------|----------|
| name       | string | -       | Name of route record                                          | -        |
| meta       | object | { }     | Meta data passed from route record                            | -        |
| path       | string | -       | URL path                                                      | -        |
| hash       | string | -       | URL hash                                                      | -        |
| query      | object | { }     | Query string parsed from URL                                  | -        |
| search     | string | -       | Raw URL query string                                          | -        |
| segments   | array  | [ ]     | URL path segments                                             | -        |
| params     | object | { }     | Parameters extracted from URL path based on route record path | -        |
| fullPath   | string | -       | URL path, query, and hash                                     | -        |
| matched    | object | -       | All nested path segments of the current route record          | -        |
| transition | object | null    | Transition specified on route record                          | -        |

## Records

Route records are objects that map a URL to parts of your application.

When a route record is matched, the callbacks defined on that record are executed in a specific order. At a minimum, route records must consist of a `path` and either a `handler` or `init` property.

### Properties

| Variable   | Type                | Default | Description                                                                                                      | Required |
|------------|---------------------|---------|------------------------------------------------------------------------------------------------------------------|----------|
| path       | string              | -       | The URL to be matched                                                                                            | ✔        |
| handler    | RouteHandler, array | -       | Route handler(s) to be evaluated when route is matched                                                           |          |
| children   | array               | -       | Nested routes                                                                                                    |          |
| name       | string              | -       | The name of the route object. Records can be referenced by name instead of path                                  |          |
| meta       | object              | -       | Custom properties to be passed to matched route record functions                                                 |          |
| before     | function            | -       | Executes at the beginning of matched route evaluation and before any registered route handler `before` callbacks |          |
| init       | function            | -       | Evaluates the first time that the route is matched                                                               |          |
| update     | function            | -       | Evaluates in place of `init` when immediately preceding route match is same as current route match               |          |
| after      | function            | -       | Executes at the end of matched route evaluation and after any registered route handler `after` callbacks         |          |
| unload     | function            | -       | Evaluates when navigating away from current route record                                                         |          |
| transition | object              | -       | Transition specific to route (overrides global transition)                                                       |          |

### Path

The path is the url that you wish to match. Paths can take an assortment of syntaxes. The full list of possible options are described in [path-to-regexp](https://github.com/pillarjs/path-to-regexp), the package that Wee Routes uses for evaluating routes. Below is a description of some of these options.

**Wildcards and Parameters**

You may use `*` to indicate a wildcard segment.  If you wish to capture that segment and pass it to your function, you use parameters which are names preceded by a colon, i.e `:id`.  Route parameters will be accessible in the route object which is passed to the various callbacks registered on a matched route record.

```js
import $router from 'wee-routes';
import { blog } from './blog';

$router.map([
    { path: '/blog/:id', handler: blog },
    { path: '*', init(to, from) {} }
]).run();

// and in `./scripts/blog`exportfunctionblog(route) {
// route.params.id will now be the matched segment.
}
```

**Optional Parameters**

You can make parameters in a path optional by adding a `?` to the end of the parameter. For example we could change the path example above:

```js
{ path: '/blog/:id?', handler: blog }
```

This route record would now match for either `/blog` or `/blog/1`.

### Name

The routes name allows you to reference the route by name, regardless of any changes to the path.

```js
import $router from 'wee-routes';
import adminHandler from './admin';

$router.map([
    { name: 'admin', path: '/admin', handler: adminHandler }
]).run();
```

### Meta

Sometimes you may want to pass specific properties into the registered functions for a route record. This can be accomplished through the meta property.

```js
import $router from 'wee-routes';
import adminHandler from './admin';

$router.map([
    { path: '/admin', handler: adminHandler, meta: { isAdmin: true } }
]).run();

// and in './scripts/admin'exportdefault

new RouteHandler {
    init(to) {
        console.log(to.meta.isAdmin); // true
    }
}
```

### Handler

The handler property can take a [Route Handler](#route-handlers) or an array of Route Handlers.

```js
import $router from 'core/router';
import blogHandler from './blog';
import commonHandler from './common';
import socialHandler from '../components/social';
import commentsHandler from '../components/comments';

const common = [commonHandler];

$router.map([
    { path: '/', handler: common },
    {
        path: '/blog/:id',
        handler: [blogHandler, socialHandler, commentsHandler, ...common],
    },
]).run();
```

### Children

You may nest routes under the `children` key.  It will accept an array of routes, structured exactly as the original route record is structured and supports all of the same options.

***Note:**  You must omit the parent segment from the child paths

When a child route is matched, this causes both the child route and it's parent route to be evaluated (parent -> children).

```js
import $router from 'wee-routes';
import adminHandler from './admin';
import postHandler from './post';

$router.map([
    {
        path: '/admin',
        handler: adminHandler,
        children: [
            { path: 'post', handler: postHandler }
        ]
    }
]).run();
```

## Route Handlers

Route Handlers are special objects that are used throughout an application to define router functionality. They can greatly clean up your route mapping by housing the various functions in their own file/module.

```js
import $router from 'wee-routes';
import about from './about';

$router.map([
    {
        path: '/about',
        before() {},
        init() {},
        update() {},
        after() {}
    }
]).run();

// becomes
$router.map([
    { path: '/about', handler: about }
]).run();
```

In the `about` module, you would export a `RouteHandler` instance with some or all of the following methods:

```js
import { RouteHandler } from 'wee-routes';

export default new RouteHandler({
    beforeInit(to, from, next) {
        // ...
    },
    init(to, from) {
        // ...
    },
    beforeUpdate(to, from, next) {
        // ...
    },
    update(to, from) {
        // ...
    },
    unload: 'about',
    after(to, from) {

    }
});
```

There are other, larger benefits to using Route Handlers besides cleaning up your main route file. Since Route Handlers will live inside page-specific modules, your Route Handler functions will have access to all page-specific variables and data. This works the other direction as well. If you need to dynamically retrieve any data with an AJAX request in a `beforeInit` hook for a particular page, for example, you can easily pass that data to your page-specific code.

Lastly, Route Handlers can be shared between multiple route records. This can be advantageous because you may, for example, have a common set of logic that you want triggered on every page. However, you may need that common module updated independently, rather than initialized, when the route record is being processed for the first time because the route handler was already initialized on a different route. This is easily achievable with Route Handlers.

```js
import $router from 'wee-routes';
import common from './common';
import home from './home';
import about from './about';

$router.map([
    { path: '/', handler: [common, home] },
    { path: '/about', handler: [common, about] }
]);

$router.run('/'); // home.init and common.init will fire
$router.run('/about'); // about.init and common.update will fire
```

### Handler Methods

Route Handlers have a specific set of possible methods/properties. Many of these are the same as route records, however there are some important additions. `beforeUpdate` and `beforeInit` are added to give more control over possible data fetching or module bootstrapping.

| Option       | Description                                | Required |
|--------------|--------------------------------------------|----------|
| beforeInit   | Executes before `init`                     | -        |
| beforeUpdate | Executes before `update`                   | -        |
| init         | Executes on first evaluation of handler    | -        |
| update       | Executes after first evaluation of handler | -        |
| unload       | Executes when leaving route record         | -        |
| after        | Executes after all other methods           | -        |

## Router

The router is a method that can take an options object. This configuration object will affect how routing behaves.It also has all of the route API methods chained to it. This allows us to initialize routes in one of two ways:

```js
import $router from 'wee-routes';

// With custom configuration
$router({
    scrollBehavior() {},
    transition: {},
}).map().run();

// Using router defaults
$router.map().run();
```

### Options

| Variable       | Type     | Default | Description                                          | Required |
|----------------|----------|---------|------------------------------------------------------|----------|
| scrollBehavior | function | -       | Defines scroll position of new page after navigation | -        |
| transition     | object   | -       | Transition during navigation                         | -        |

### Scroll Behavior

When navigating a user with [History](https://developer.mozilla.org/en-US/docs/Web/API/History), we may want to scroll to the top of the page, or preserve the scrolling position of history entries just like the browser does during a full page reload (or some other custom behavior). This is controlled with the `scrollBehavior` function. The default scroll functionality would look like this if passed in manually to the router:

```js
import $router from 'wee-routes';

$router({
    scrollBehavior(to, from, savedPosition) {
        if (savedPosition) {
            return savedPosition;
        } else {
            return { x: 0, y: 0 };
        }
    }
});
```

### Parameters

| Variable      | Type   | Default | Description                      | Required |
|---------------|--------|---------|----------------------------------|----------|
| to            | object | -       | Current [route match](#matches)  | -        |
| from          | object | -       | Previous [route match](#matches) | -        |
| savedPosition | object | -       | Saved x and y values             | -        |

The savedPosition parameter exists if the navigation was triggered with the [popstate event](https://developer.mozilla.org/en-US/docs/Web/Events/popstate) and therefore has the saved scroll state from when the page was previously visited.

### Transitions

Transitions allow for a smooth experience when navigating with the router. The most basic implementation looks something like the following:

```js
import $router from 'wee-routes';

$router({
    transition: {
        target: 'body',
        class: '-is-loading',
        timeout: 200,
    },
});
```

Here we are telling the router to apply a given modifier class to a single container element on the page that we want to transition out and back in again.

**Note:** Make sure transition class target is is not being replaced by `PJAX`, or the transition will fail.

The expectation with this implementation is that the designated class is applying a CSS transition which means that the target element must stay on the DOM throughout the navigation process. The timeout property is recommended to ensure that transitions work consistently. The value of the timeout property would typically be the same length of time as the transition applied on the target or longer.

**Note:** The need for a timeout will be corrected in a future version of Wee.

The other implementation uses custom callbacks and looks like the following:

```js
import $router from 'wee-routes';

$router({
    transition: {
        leave(to, from, next) {
            // Custom logic for exiting previous pageif (! transitionSuccessful) {
              next(newError('something went wrong'));
            }

            next();
        },
        enter(to, from) {
            // Custom logic for entering newly navigated page
        }
    }
})
```

### Parameters

| Variable | Type     | Default | Description                                                | Required |
|----------|----------|---------|------------------------------------------------------------|----------|
| to       | object   | -       | Current [route match](#matches)                            | -        |
| from     | object   | -       | Previous [route match](#matches)                           | -        |
| next     | function | -       | Callback that continues transition evaluation (leave only) | -        |

This implemenation allows you to do anything you can dream up. Passing an error instance will cause the navigation to stop processing and return to the previous page, again same as a `before` hook.

Transitions can be configured globally or per route. Transitions on a route record will take precedence:

```js
import $router from 'wee-routes';

$router({
    transition: {
        target: 'body',
        class: '-is-loading',
        timeout: 200,
    },
}).map([
    {
        path: '/',
        transition: {
            leave() {},
            enter() {},
        },
    },
]);
```

## $router.onError

Register global error handler

This method registers global router error handlers. These handlers will be executed if anything goes wrong with navigation and/or route processing (including PJAX navigations). An error that is thrown within the router will differ in the properties they contain. However, these are the properties you can count on to determine the action you should take in your error callback:

### Error Properties

| Variable  | Type   | Default | Description                    | Required |
|-----------|--------|---------|--------------------------------|----------|
| errorType | string | -       | Name of error constructor      | -        |
| message   | string | -       | Description of what went wrong | -        |

```js
import $router from 'wee-routes';

$router.map([
    { path: '/', init(to, from) {} },
]).onError((error) => {
    // Handle error
}).run();
```

All custom errors in Wee extend `Error`. Babel cannot currently extend built-in types so we cannot use `instanceof` inspections of our custom errors to determine the type, hence `errorType` is added to all custom errors in Wee to fill this need.

## $router.push

Navigate with History API

This method allows you to navigate to a url and add the navigation to the browser's history. It also hooks into [PJAX](#pjax) if enabled on router, allowing you to override partial targets or pause partial replacement during the request. This method returns a promise.

### Parameters

| Variable   | Type            | Default | Description                                                                              | Required |
|------------|-----------------|---------|------------------------------------------------------------------------------------------|----------|
| path       | string          | -       | Destination URL                                                                          | ✔        |
| modifyPjax | boolean, object | false   | Modify/pause PJAX during request. Passing `true` will pause PJAX altogether for request. | -        |

### Modify PJAX

| Variable | Type  | Default | Description                          | Required |
|----------|-------|---------|--------------------------------------|----------|
| partials | array | -       | Targets used for partial replacement | -        |

```js
$router.push('/about');
```

```js
$router.push('/about', true);
```

```js
$router.push('/about', { partials: ['.some-other-target'] });
```

## $router.replace

Navigate with History API, replacing browser history entry

This method allows you to navigate to a url and replace the most recent browser history entry. It also hooks into [PJAX](#pjax) if enabled on router, allowing you to override partial targets or pause partial replacement during the request. This method returns a promise.

### Parameters

| Variable   | Type            | Default | Description                                                                              | Required |
|------------|-----------------|---------|------------------------------------------------------------------------------------------|----------|
| path       | string          | -       | Destination URL                                                                          | ✔        |
| modifyPjax | boolean, object | false   | Modify/pause PJAX during request. Passing `true` will pause PJAX altogether for request. | -        |

### Modify PJAX ### (.doc__label .doc__variables__label)

| Variable | Type  | Default | Description                          | Required |
|----------|-------|---------|--------------------------------------|----------|
| partials | array | -       | Targets used for partial replacement | -        |

```js
$router.replace('/about');
```

```js
$router.replace('/about', true);
```

```js
$router.replace('/about', { partials: ['.some-other-target'] });
```

## $router.afterEach

Register global after method

The function passed to `afterEach` will be executed at the very end of the matched route record's evaluation. Like `beforeEach`, you can register as many as you like, and they will execute in the order they were registered.

```js
import $router from 'wee-routes';
import common from './common';
import about from './about';

$router.map([
    { path: '/', handler: common },
    { path: '/about', handler: about },
])
.afterEach((to, from) => {})
.run();
```

## $router.beforeEach

Register global before method

The function passed to `beforeEach` will be executed before any route record specific before methods and can act as a guard in the same way that [before](#methods) does for an individual route record. This function is passed the same parameters as all other before methods. You can register as many `beforeEach` methods as you like, and they will execute in the order they are registered.

```js
import $router from 'wee-routes';
import common from './common';
import about from './about';

$router.map([
    { path: '/', handler: common },
    { path: '/about', handler: about },
]).beforeEach((to, from, next) => {
  // ...
  next();
}).run();
```

## $router.run

Evaluate routes against current URL

```js
import $router from 'wee-routes';
import common from './common';
import about from './about';

$router.map([
    { path: '/', handler: common },
    { name: 'about', path: '/about', handler: about },
]).run().catch((error) => {
  // Run returns a promise// Do something with error
});
```

##  $router.notFound

Add 404 style wildcard route

This method takes a route record object, excluding the `path` or `name` properties of a normal route record.  This route record will be evaluated if no other routes match. `notFound` is simply a convenience method. You can achieve the same functionality by registering a wildcard route record at the end of your map array with `path: '*'` and `name: 'notFound'`. This method, however, is  a little more expressive.

```js
import $router from 'wee-routes';
import common from './common';
import about from './about';
import unknown from './404';

$router.map([
    { path: '/', handler: common },
    { path: '/about', handler: about }
])
.notFound({ handler: unknown })
.run();
```

## $router.map

Define routes for application

### Parameters

| Variable | Type  | Default | Description                        | Required |
|----------|-------|---------|------------------------------------|----------|
| routes   | array | -       | Array of [route records](#records) | ✔        |

```js
import $router from 'wee-routes';
import common from './common';
import about from './about';

$router.map([
    { path: '/', handler: common },
    { path: '/about', handler: about },
]).run();
```

## $router.pjax

Enable and configure global PJAX behavior

This function enables a specific implementation of history navigation in which html partials are returned and replaced on the DOM rather than a full page load. This works very well to make websites that use static templates feel more like a single page application.

| Variable | Type   | Default | Description           | Required |
|----------|--------|---------|-----------------------|----------|
| options  | object | -       | Configuration options | -        |

### Options Object

| Variable | Type                     | Default           | Description                                                | Required |
|----------|--------------------------|-------------------|------------------------------------------------------------|----------|
| bind     | object, array            | { click: 'a' }    | Target for binding events that will trigger navigation     | -        |
| partials | array                    | ['title', 'main'] | DOM targets to be replaced                                 | -        |
| replace  | function                 | -                 | Hook for manipulating returned HTML                        | -        |
| request  | [$fetch](/scripts/fetch) | -                 | Custom fetch instance if request configuration is required | -        |
| context  | string, HTMLElement      | document          | Context for elements defined in `bind` option              | -        |
| onError  | function                 | -                 | Execute callback if pjax triggered navigation fails        | -        |

```js
import $router from 'wee-routes';
import about from './about';
import common from './common';

$router.pjax({
    bind: {
        click: 'a',
    },
    partials: ['title', 'main'],
}).map([
    { path: '/', handler: common },
    { path: '/about', handler: about },
]).run();
```

**URL Validity**

When `pjax` is executed, it binds events to designated targets on the DOM that will trigger an AJAX request for the destination page's HTML and then navigate to the destination URL. During this binding phase, the URL of each DOM target will be evaluated to ensure the URL is valid. The following criteria determine a valid URL.

- URL exists (either `href` if DOM target is `<a>` or `data-url` if another DOM element)
- URL does not open new window (checks for `_blank` attribute)
- URL is absolute URL, not relative (`https://something.com/about` vs `/about`)
- Target is not a download link
- Target does not have `data-static` attribute
- URL is not external link
- URL is current page, only with hash added
