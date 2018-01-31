# Assets

Dynamic loading for JavaScript, CSS, and Images

Don’t embed assets on requests where they aren’t needed, or needed immediately. Load what you need on demand to optimize page speed and preserve bandwidth. You can asynchronously (or synchronously) load scripts as well as CSS and images. Work with groups and callbacks to solve complex problems.

## $assets.load ##

Load assets with specified set of options

| Variable | Type   | Default | Description             | Required |
|----------|--------|---------|-------------------------|----------|
| options  | object | -       | Object parameters below | ✔        |

### Configuration Object

| Variable | Type          | Default | Description                                             | Required |
|----------|---------------|---------|---------------------------------------------------------|----------|
| async    | boolean       | true    | Loads assets asynchronously, only applicable to scripts | -        |
| cache    | boolean       | true    | Bust request cache with random querystring              | -        |
| styles   | string, array | -       | Single CSS path or array of CSS paths                   | ✔        |
| error    | function      | -       | Failure callback                                        | -        |
| files    | string, array | -       | Single file path or array of file paths                 | ✔        |
| group    | string        | -       | Optional reference for use with [ready](#ready)         | -        |
| images   | string, array | -       | Single image path or array of image paths               | ✔        |
| scripts  | string, array | -       | Single JavaScript path or array of JavaScript paths     | ✔        |
| root     | string        | -       | Root path or domain override for [root](#root)          | -        |
| success  | function      | -       | Success callback                                        | -        |

### Single File

```js
import $assets from'wee-assets';

$assets.load({
    files: '/path/to/alert.js',
    success() {
        // Success logic
    },
    error() {
        // Failure logic
    }
});
```

### Multiple Files

```js
import $assets from'wee-assets';

$assets.load({
    root: 'https://cdn.weepower.com',
    files: [
        '/path/to/alert.js',
        '/path/to/override.css',
        '/path/to/sample.png'
    ],
    success() {
        // Success logic
    },
    error() {
        // Failure logic
    }
});
```

If an absolute URL beginning with "//", "http://", or “https://” is requested the root option will be ignored.

### Group
```js
import $assets from'wee-assets';

$assets.load({
    files: '/path/to/alert.js',
    group: 'dynamicAssets'
});

$assets.ready('dynamicAssets', {
    success() {
        // Success logic
    },
    error() {
        // Failure logic
    }
});
```

## $assets.ready
When specified references are ready execute callback

| Variable | Type    | Default | Description                                         | Required |
|----------|---------|---------|-----------------------------------------------------|----------|
| group    | string  | -       | Group reference name                                | ✔        |
| options  | object  | -       | Override any load configuration options             | -        |
| poll     | boolean | false   | Poll the queue every 20 milliseconds for completion | -        |

### Check

```js
import $assets from'wee-assets';

$assets.ready('dynamicAssets');
```

```js
true
```

### Check and Set

```js
import $assets from'wee-assets';

$assets.ready('dynamicAssets', {
    success() {
        // Success logic
    }
});
```

## $assets.remove

Remove one or more files from the DOM

| Variable | Type          | Default | Description                                    | Required |
|----------|---------------|---------|------------------------------------------------|----------|
| files    | string, array | -       | Single file path or file array                 | ✔        |
| root     | string        | -       | Root path or domain override for [root](#root) | -        |

### Single File

```js
import $assets from'wee-assets';

$assets.remove('/samples/override.css');
```

### Multiple Files

```js
import $assets from'wee-assets';

$assets.remove([
    '/samples/override.css',
    '/samples/alert.js'
], 'https://cdn.weepower.com');
```

## $assets.root
Get current asset root or set with specified value

| Variable | Type   | Default | Description       | Required |
|----------|--------|---------|-------------------|----------|
| value    | string | -       | Root request path | ✔        |

### Set

The value set here is prepended to every request if not specifically overridden.

```js
import $assets from'wee-assets';

$assets.root('https://cdn.weepower.com');
```

### Get

Retrieve the current root which defaults to an empty string, unless previously set.

```js
import $assets from'wee-assets';

$assets.root();
```

```js
"https://cdn.weepower.com"
```

### Advanced

Only set the asset root to a CDN in the production [environment](/script/core#env).

```js
import { $env } from'core/core';
import $assets from'wee-assets';

if ($env() == 'prod') {
    $assets.root('https://cdn.weepower.com');
}
```

You can override the root on individual requests. For instance, you may want to load all your static assets from a CDN but pull JSON or other files from a local server.
