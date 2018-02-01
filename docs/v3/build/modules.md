# Modules

Logically group script and style for internal use or distribution

Modules are an excellent way to separate your codebase into isolated, reusable sections of JavaScript and CSS. This can be very useful for reusability and maintainability in large projects, or simply a way of abstracting common functionality into a sharable format.

## Config

Modules are configured much like the Wee core

These properties are for internal or distributed reference.

```json
"name": "Module Name",
"version": "1.0.0",
"description": "Module description.",
"homepage": "https://www.weepower.com",
"author": "Wee",
```

### Settings


When autoload is set to true, the scripts and styling will be compiled directly into the global style.min.css and script.min.js files. If set to false, separate minified files will be compiled into public/assets/modules/moduleName/.

The extension setting, when set to true gives your Less access to all the custom variables, mixins, etc from your core project. In most scenarios you want this to be false to create true isolation between the module and the root project.

```json
"autoload": true,
"extension": false
```

### Global Data


As with the wee.json, sharing global data across your script and style is simple. Set key-value pairs to be made available to both. You can also set data specifically in either the script or style config blocks to limit the scope.

```json
"data": {
    "brandColor": "#0f0"
}
```

### Script and Style

These optional blocks work just like they do in the [core configuration](/docs/v3/build/config) however paths are relative to the module.json file instead.

```json
"style": {
    "build": [
        "css/variables.less",
        "css/screen.less"
    ]
},
"script": {
    "build": [
        "js/script.js"
    ]
}
```

## Structure

Similar organization to the core Wee setup

The heart of the code in a module should reside inside the core directory. Beyond permanent modifications by the original author, the core directory should be left alone and any specific overrides be set in the module.json. Check out the [style](/docs/v3/build/config?id=style) and [script](/docs/v3/build/config?id=script) docs to understand where autoloaded modules fit into the build process.

```
module.json

core/
css/
screen.less
variables.less
breakpoints/
js/
script.js
views/
load/
css/
fonts/
img/
js/
```

All the directories and files in the module are optional.

You can run the [make command](/docs/v3/build/commands?id=make) to create one using the Wee CLI.
