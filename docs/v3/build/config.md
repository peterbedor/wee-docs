# Config

Building your project with Wee is easy

Wee is setup through a simple configuration file called `wee.json` to define your project structure and output.

## General

The name property is for internal reference only.

```json
"name": "Project Name"
```

### Paths

To accommodate different publish configurations, Wee needs to know your directory structure. The root and source paths are relative to wee.js and the asset directory is relative to the root directory.

```json
"paths": {
    "root": "public",
    "assets": "assets",
    "source": "source"
}
```

The “root” path is your public HTML directory. Common values include "www", "public", and "public_html".

### Global Data

Sharing global data across your script and style is simple. Set key-value pairs to be made available to both. You can also set data specifically in either the script or style config blocks to limit the scope.

```json
"data": {
    "brandColor": "#0f0"
}
```

To access global script data use the following syntax.

```js
Wee.$get('global.brandColor');
```

Style data can be accessed by the key name in Less as follows.

```less
body {
    color: @brandColor;
}
```

### Default Command

By default if you execute `wee` the `wee run:static` command is run. You can override that value with any working command in this field.

```json
"defaultCommand": "run:static"
```

## Generator

You can disable all generator integration by setting enable to false. Add as many static generator config paths to the build array as needed.

```json
"generator": {
    "enable": true,
    "build": [
        "source/modules/guide/generate.json"
    ]
}
```

## Script

Wee comes with several standard JavaScript features such as asset loading, chaining, DOM manipulations, event binding and more. You can also compile and/or build in your own scripts.

### Core

The core section allows you to enable or disable core features. For instance, if your project requires jQuery, you may choose not to include Wee’s DOM functionality.

```json
"core": {
    "enable": true,
    "namespace": "Wee",
    "features": {
        "animate": true,
        "assets": true,
        "chain": true,
        "data": true,
        "dom": true,
        "events": true,
        "history": true,
        "routes": true,
        "screen": true,
        "touch": true,
        "view": true
    }
}
```

Setting the primary enable value to false disables all core features.

### Build

This works the same as the CSS section. You can build any script into the primary compiled file.

```json
"build": [
    "path/to/one.js",
    "path/to/two.js"
]
```

### Compile

This works the same as the CSS section. If you have JavaScript files that you would like to compile and minify, but not include in your primary JavaScript output, this is where you can specify them.

```json
"compile": {
    "ie9.min.js": [
        "polyfill/wee.placeholder.js",
        "polyfill/wee.slice.js"
    ]
}
```

### Validate

The validation section controls which settings are used for [JSCS](jscs.info) and [JSHint](jshint.com) code style and quality tools. Set either to false to disable them otherwise you can update the path to point to any config file or modify the default files provided in the source directory. Setting watch to false disables continuous validation and only allows [on-demand validation](https://www.weepower.com/build/commands#validate).

```json
"validate": {
    "watch": true,
    "jscs": "source/.jscs.json",
    "jshint": "source/.jshintrc"
}
```

### Source Maps

Source maps allow modern browsers to map compiled and minified code to original source scripts. This is useful when tuning and debugging.

```json
"sourceMaps": true
```

## Server

When Wee is running and serving your site through the proxy, you can choose to have it mirror actions between connected browsers. That means if you have a browser open to your proxy URL on perhaps a mobile device on the same network, and your local development device, when you scroll, click, or take an action on one browser, it will be replicated in the other.

```json
"ghostMode": false
```

### Host

If you need to override the hostname do it here. By default your current public IP will be used.

```json
"host": "auto"
```

### Port

If for some reason you are having a port conflict, you can update the port here.

```json
"port": 9000
```

### Inject

Add paths to the injection array to dynamically add them to your pages requested through the proxy server.

```json
"inject": [
    "/source/js/custom/testing.js"
]
```

### Reload

This allows you to enable or disable reloading whenever CSS, JavaScript, or static files change. It also allows specifying certain paths and extensions to watch for efficiency. If you want to ignore specific paths from proxy handling add them to the ignore array.

```json
"reload": {
    "enable": true,
    "ignore": [

    ],
    "watch": {
        "root": true,
        "paths": [

        ],
        "extensions": [
            "html"
        ]
    }
}
```

### Tasks

With the `wee run:local` task, Wee needs to know your local server address. It then uses a proxy to sit between your browser and the development server to inject changes.

With wee `run:static` you can set whether to use HTTPS.

## Style

The core block allows disabling styling features as well as setting breakpoint values. By setting any key to false that feature or breakpoint is suppressed.

If an ID or class “namespace” is set all mixins will be prefixed to prevent collisions with class names since Less does not differentiate between the two.

```json
"core": {
    "namespace": false,
    "features": {
        "buttons": true,
        "code": true,
        "forms": true,
        "print": true,
        "tables": true
    },
    "responsive": {
        "enable": true,
        "offset": 25,
        "breakpoints": {
            "mobileLandscape": 480,
            "tabletPortrait": 768,
            "desktopSmall": 1024,
            "desktopMedium": 1280,
            "desktopLarge": 1440
        }
    }
}
```

The offset value is used to decrement breakpoint values by a set number of pixels which is useful when testing media queries widths in desktop browsers.

### Build

Wee outputs one primary CSS file. The build array specifies additional CSS or Less files that you want included.

```json
"build": [
    "path/to/one.css",
    "path/to/two.less"
]
```

Paths are relative to the Wee CSS source directory unless prefixed with `./` making them relative to `wee.js`.

###  Compile

If you have CSS or Less files that you would like to compile, but not include in your primary stylesheet (to serve specific styling to certain pages), this is where you can define them.

```json
"compile": {
    "array.css": [
        "path/to/one.css",
        "path/to/two.less"
    ],
    "ie9.min.css": "./source/css/custom/ie9.less",
    "globbing.css": "path/to/*.less"
}
```

You can use any globbing conventions (such as wildcards and exclusions).

```json
"file.css": [
    "*",
    "**/*",
    "*.less",
    "*.{css,less}",
    "**/*.css",
    "!**/*.less"
]
```
