# ES Modules

Over time, the JavaScript community has had to overcome the increasingly complex ways in which JavaScript is being utilized. As complexity grows, so does the need to manage that complexity in a way that will make a codebase maintainable. One concept that is core to this goal is modularity, or the loose coupling of highly distinct pieces of functionality.

Until somewhat recently, JavaScript had no good way of building code in a modular fashion. Everything that is written inside of a standard script tag is exposed to the global namespace. There is no inherent separation between different scripts, and therefore the possibility of colliding functions and variables is a very real challenge. One approach to combat this was to nest an entire library of functionality (e.g., jQuery) inside of one big object. That single object would then be the only variable that could be collided with by some other script on the page. Wee historically has used this same basic approach.

Whether using the single global object described above, the [module pattern](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html), or a [modular format](https://addyosmani.com/writing-modular-js/) such as CommonJS or AMD, developers have been forced to come up with manual solutions to this problem. However, since the release of ES2015, JavaScript now has it's very own module system. Let's take a look at a simple example:

**Module A**
```javascript
export function greeting() {
    return 'hello world!';
}
```

**Module B**
```javascript
import { greeting } from './module-a.js';

console.log(greeting()); // hello world!
```

From the example above, we notice a few things:

- We are defining the function `greeting` and making it available outside of module A by putting the `export` statement in front of the function.
- The `greeting` function is made available to module B by using the `import` statement at the top of the file.
- Once imported, we can execute  the imported function`greeting`.

Let's expand on the mechanisms we have identified so far.

## Definition of Terms

### Module
A module is a decoupled and distinct piece of code. This ensures that duplication throughout a codebase is reduced. As a result, modules are often built with reusability in mind. Modules should also have their own scope. That means that variable definitions will not pollute the global namespace, but will be contained to the module where they are written. Any part of a module that is exposed to or brought in from the outside world must be explicitly exposed or included. This allows us to enforce a strict and predictable system for dependent modules to work within.

### Export
The [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) statement is used to expose a value from a given module. Multiple values can be exported from a single file. Also, a single `default` export can be defined in a module. Default exports make import statements a little cleaner.

**Named Exports**
```javascript
// Module - Example A
const myVariable = true;

export { myVariable }; // exports a variable that was declared earlier
export const foo = 'bar'; // exports the variable declaration directly
```

**Default Exports**
```javascript
// Module - Example B
export default function() {};
```

**Combined**
```javascript
// Module - Example C
export const foo = 'bar';
export default function() {}
```

### Import
The [import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) statement is used to import a value into a module from other outside modules.

**Note:** Examples below are direct continuations of the export examples above.

**Importing individual members**
```javascript
// Imported from Example A
import { myVariable, foo } from '/path/to/example-a.js';
```

**Importing entire module's contents**
```javascript
// Imported from Example A
import * from '/path/to/example-a.js';
```

**Importing default export**
```javascript
// Imported from Example B
import exampleB from '/path/to/example-b.js';
```

**Importing default and named exports**
```javascript
// Imported from Example C
import exampleC, { foo } from '/path/to/example-c.js';
```

## Module Bundling
As you can hopefully see, ES Modules are great. Unfortunately, they are not supported yet in all browsers. This is where [Webpack](https://webpack.js.org/) comes in. Webpack is a powerful build tool for compiling JavaScript modules together. It solves the problem of browser support for modules by bundling and wrapping all the modules of your application in a browser-compatible way that still retains the integrity of the module system. Unfortunately, this bundling process adds some extra size to the end script file that is served to the browser. Still, we feel that this is a small price to pay for the benefits that modules, and Webpack, bring to Wee.

Because ES modules explicitly define the dependencies of an application ahead of time with a static structure, Webpack can eliminate dead code (code not imported in the application) in a process known as tree shaking. This can have potentially large reductions in script size for a website. Other optimization techniques such as [common module chunking](https://webpack.js.org/plugins/commons-chunk-plugin/#src/components/Sidebar/Sidebar.jsx) are also available within Wee's build process that utilizes Webpack.

## Wee Implementation
Normally, modules are imported by referencing the exact location of a module in the file system relative to the module you are importing from. However, Webpack allows for exceptions to this rule. In the case of Wee, `node_modules` and `wee-core/scripts` are aliased so that importing can be done with brevity.

**Node Modules**
```javascript
// Without aliasing - importing from /source/scripts
import Vue from '../../node_modules/vue';

// With alias
import Vue from 'vue';
```

**Wee Core**
```javascript
// Without aliasing - importing from /source/scripts
import $router from '../../node_modules/wee-core/scripts/wee-routes';

// With alias
import $router from 'wee-routes';
```
