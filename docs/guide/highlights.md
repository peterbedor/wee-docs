[lewis-site]: https://www.lewiscommunications.com/

## Less to SASS/PostCSS
Until now, Wee has used Less as the pre-processor of choice. For those who are new to the concept of CSS pre-processors, Less enabled us to do things like [set variables](http://lesscss.org/features/#features-overview-feature-variables), [nest CSS selectors](http://lesscss.org/features/#features-overview-feature-nested-rules), and utilize [mixins](http://lesscss.org/features/#features-overview-feature-nested-rules) to dramatically improve the structure of our stylesheets. Pre-processors have proven to be a fantastic tool for creating clean and maintainable CSS. That being said, things can always get better.

[PostCSS](http://postcss.org/) by definition, is simply a tool for transforming CSS with JavaScript. What sets PostCSS apart is the flexibility of its plugin based design. With it, we have the ability to completely customize the way that our CSS is processed. We can choose from the ever-growing collection of plugins out there, or if we need, we can build our own plugins!

See the guide on [PostCSS](/guide/postcss) for more details on exactly how we are utilizing this powerful tool.

## ES2015 and Beyond
Creating Wee 4 provided us the opportunity to bring Wee's JavaScript library up to current standards. As a result, the entire Wee codebase was refactored with ES2015+ syntax. We are very excited at the improvements this brought to the core library, but we are even more excited about the direct benefits for developers using Wee to build their projects.

Wee has traditionally used a construct known as controllers. They brought organization to the chaos, tying different core parts of the Wee library together and promoting modular design. This worked well, but now we have a construct built right into the language: [ES Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/). Like controllers, they provide a way to build an application with independent and reusable pieces of code. However, they also provide other really great benefits like explicit dependency declaration and the possibility for static code analysis which enables [tree shaking](https://webpack.js.org/guides/tree-shaking/).

The incorporation of ES2015+ features requires that we transpile our code down to ES5 before serving it to the browser to ensure that older browsers can understand it. For this, we turned to [Babel](https://babeljs.io/) and [Webpack](https://webpack.js.org/).  Read the guide on [ES Modules](/guide/es-modules) to learn why and to gain a more in depth understanding of the benefits of this new architecture.

## Components
Wee 4 comes with a component-based approach to front-end development. For years now, the front-end community has been moving towards building user interfaces based on components. This trend has many different implementations, however the basic concepts are the same which is to encapsulate reusable code. By breaking down a website into a system of reusable components, we can build complex user interfaces in a more structured, manageable way.

Typically, a component is composed of a template (HTML), JavaScript, and CSS. Frameworks such as [Vue.js](https://vuejs.org/) and [React](https://facebook.github.io/react/) work under the assumption that the template will be defined and manipulated in JavaScript. However, the majority of projects at [Lewis Communications][lewis-site] generate the entire HTML document from the CMS. Although server-side rendering is possible for both of these example frameworks, the range of CMS we use is written in PHP and utilize Twig or some other templating language for generating the document. As a result, a standard component in Wee 4 contains only JavaScript and CSS. This standard component will then directly correspond to a template partial in our CMS by name.

There are other cases in which the requirements of the website justify the use of a framework like the ones mentioned above. This is why we have made [Vue.js](https://vuejs.org/) a first-class citizen in Wee 4. It is our first choice when creating more advanced user interfaces.

Based on the explanation above, we have two different components that can be created in Wee 4: standard and Vue components. These can be generated with the [Wee CLI](https://www.npmjs.com/package/wee-cli) by executing `wee component -n componentName`. To specify a Vue component, just add the `v` flag `wee component -n componentName -v`. More on components can be found in the guide on [components](/guide/components).

## Build Process
Over time, the Wee build process had become quite complex. As Wee 4 was taking shape, it was clear that major structural changes to the project, and therefore the build process, would need to take place. For one, we were removing [Wee Modules](/build/modules) and putting in place a components directory. In addition, we were introducing new platforms like PostCSS and Webpack into the mix. These new tools were challenging the logic of our folder names and structures. Finally, Grunt was the task runner for the build process. We were ready to move on from its verbose syntax and [dwindling community](https://www.sitepoint.com/front-end-tooling-trends-2017/) (see also the[ Front-end Tooling Survey](https://ashleynolan.co.uk/blog/frontend-tooling-survey-2016-results#js-task-runners)).

Wee 4 is now driven by [npm scripts](https://docs.npmjs.com/misc/scripts). No more Grunt or Gulp. Establishing the build process on npm has been a great experience. Here are a few advantages we have seen so far:

- No more waiting on Grunt plugin authors - Many plugins in the Grunt/Gulp ecosystem are merely wrappers around other packages. One inconvenient side-effect this has is that you are now dependent on the author of the wrapper plugin you are using when the core package it wraps has been updated. In our experience, this was starting to become an issue in the Grunt community in particular.
- Build process transparency - It is very easy to take a peek at how the build process is working. All you need to do is look at the `package.json` and analyze the `scripts` block.
- CLI packages are all you need... for the most part - Most packages like Babel or Webpack have a 1st party CLI package. For most cases, this is all you need, and they work great. In our case, we had to create a couple of Node scripts for PostCSS and compressing images, however they were quite easy and were only necessary because of our specific needs.

Though using npm scripts, we still utilize the [Wee CLI](#), however, some of the commands are simply calling a corresponding npm script defined in the package.json with some basic options passed in.

**Note:** It is best to have Node 8 and NPM 5 to take advantage of the package-lock.json file that comes with Wee 4.

### NPM Script Resources

- [Why I Left Gulp and Grunt for npm Scripts](https://medium.freecodecamp.org/why-i-left-gulp-and-grunt-for-npm-scripts-3d6853dd22b8)
- [How to Use npm as a Build Tool](https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/)
- [Why npm Scripts](https://css-tricks.com/why-npm-scripts/)
- [Npm build boilerplate](https://github.com/damonbauer/npm-build-boilerplate/blob/master/package.json)

## Core Changes
Wee 4 was rethought from the ground up. The following core libraries are new or re-written:

###  [Routes](/script/routes)
The routes module serves as the blueprint for a project. In Wee 4, the router has a completely new API. Here's a basic example:

```javascript
import $router, { RouteHandler } from 'wee-routes';

// These would be imported from other files
const foo = new RouteHandler({
    init(to, from) {
      // Initialize page specific functionality
    },
});
const bar = new RouteHandler({
    init(to, from) {
      // Initialize page specific functionality
    },
});

$router.map([
  { path: '/foo', handler: foo },
  { path: '/bar', handler: bar },
]).run();
```

Here are some of the highlights of the new routes module:

- We have greatly simplified the route matching logic. It is much easier to reason about than the previous router because only one route endpoint matches at a time.
- [Wee History](/script/history) is now part of the router. This allows for configuring websites to utilize History navigation and partial template replacement (PJAX) more intuitively. You can also make manual page navigations with the History API with the `push` and `replace` methods that hook directly into the router.
- The new `RouteHandler` provides powerful route lifecycle hooks for bootstrapping a page and cleaning up when navigating away. For example, you could now make an AJAX request in a handler's `before` hook to retrieve data before the page is loaded. `before` hooks can also act as guards, telling the router if the route should not be matched based on certain criteria.

### [Fetch](/script/fetch)
The fetch module is used for making AJAX requests. It is now promise-based and boosted with additional options. Here is an example:

```javascript
import $fetch from 'wee-fetch';

$fetch.get('https://weepower.com/data.json')
    .then(response => console.log(response.data))
    .catch(error => console.error);
```

### [Store](/script/store)
The store module was essentially extracted from controllers from Wee 3. It allows for storing and managing data in a logical fashion. It also can be configured to sync data with either [SessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage) or [LocalStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage). Here is an example:

```javascript
import $store from 'wee-store';

$store.set('foo', 'Hello world!');
$store.get('foo'); // 'Hello world!'
```

### [Mediator](/script/mediator)
The mediator module is aptly named for the reason that it is based on the mediator design architecture. It promotes loose coupling of different parts of an application by keeping each from referring directly to one another in their codebase. Here is an example:

```javascript
import $mediator from 'wee-mediator';

// Listen for publication to 'newMessage' topic
$mediator.on('newMessage', (message) => console.log(message));

// In another module
// Will cause module above to log 'Hello world!' in console
$mediator.emit('newMessage', 'Hello world!');
```

### [Location](/script/location)
The location module was extracted from the old routes module. It has two methods for viewing information about the current browser URL: `uri` and `segments`. `uri` parses the current URL into all it's distinct anatomy, and `segments` provides easy access to the current URL's path.

### ESLint
We want to also mention that we have moved from [JSHint](http://jshint.com/) to [ESLint](https://eslint.org/). It is easily customizable and works well with Webpack. We think this will be a major improvement in code styling feedback.
