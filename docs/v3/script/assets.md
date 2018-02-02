# Assets

Dynamic loading for JavaScript, CSS, and images

Don’t embed assets on requests where they aren’t needed, or needed immediately. Load what you need on demand to optimize page speed and preserve bandwidth. You can asynchronously (or synchronously) load scripts as well as CSS and images. Work with groups and callbacks to solve complex problems.

## Load

Load specified assets with specified set of options

|Variable|Type    |Default |Description            |Required|
|--------|--------|--------|-----------------------|--------|
|options |object  |-       |Object parameters below|✔       |

### Configuration Object

|Variable|Type                         |Default |Description                                                   |Required|
|--------|-----------------------------|--------|--------------------------------------------------------------|--------|
|async   |boolean                      |true    |Load assets asynchronously, only applicable to scripts        |-       |
|cache   |boolean                      |true    |Bust request cache with random querystring                    |-       |
|css     |string, array                |-       |Single CSS path or array of CSS paths                         |✔	    |
|error   |[function](/script#functions)|-       |Failure callback                                              |-       |
|files   |string, array                |-       |Single file path or array of file paths                       |✔		|
|group   |string                       |-       |Optional reference for use with [ready](/script/assets#ready) |-       |
|img     |string, array                |-       |Single image path or array of image paths                     |✔		|
|js      |string, array                |-       |Single JavaScript path or array of JavaScript paths           |✔       |
|root    |string                       |-       |Root path or domain override for [ready](/script/assets#root) |-       |
|success |[function](/script#functions)|-       |Success callback                                              |-       |

### Single File

```js
Wee.assets.load({
    files: '/path/to/alert.js'
});
```

### Multiple Files

```js
Wee.assets.load({
    root: 'https://cdn.weepower.com',
    files: [
        '/path/to/alert.js',
        '/path/to/override.css',
        '/path/to/sample.png'
    ],
    success: function() {
        // Success logic
    },
    error: function() {
        // Failure logic
    }
});
```

If an absolute URL beginning with "//", "http://", or “https://” is requested the root option will be ignored.

### Group

By providing a group name you can optionally check against the group later for completion.

```js
Wee.assets.load({
    files: '/path/to/alert.js',
    group: 'dynamicAssets'
});
```

## Ready

When specified references are ready execute callback

|Variable|Type    |Default |Description                                        |Required|
|--------|--------|--------|---------------------------------------------------|--------|
|group   |string  |-       |Group reference name                               |✔		|
|options |object  |-       |Override any load configuration options            |        |
|poll    |boolean |false   |Poll the queue every 20 milliseconds for completion|        |

### Check

```js
Wee.assets.ready('dynamicAssets');
```

```js
true
```

### Check and Set

```js
Wee.assets.ready('dynamicAssets', {
    success: function() {
        // Success logic
    }
});
```

## Remove

Remove one or more files from the DOM

|Variable|Type         |Default |Description                                                 |Required|
|--------|-------------|--------|------------------------------------------------------------|--------|
|files   |string, array|-       |Single file path or file array                              |✔		  |
|root    |string       |-       |Root path or domain override for [root](/script/assets#root)|-       |

### Single File

```js
Wee.assets.remove('/samples/override.css');
```

### Multiple Files

```js
Wee.assets.remove([
    '/samples/override.css',
    '/samples/alert.js'
], 'https://cdn.weepower.com');
```

## Root

Get current asset root or set with specified value

|Variable|Type    |Default |Description      |Required|
|--------|--------|--------|-----------------|--------|
|value   |string  |-       |Root request path|-       |

### Set

The value set here is prepended to every request if not specifically overridden.

```js
Wee.assets.root('https://cdn.weepower.com');
```

### Get

Retrieve the current root which defaults to an empty string, unless previously set.

```js
Wee.assets.root();
```

```js
"https://cdn.weepower.com"
```

### Advanced

Only set the asset root to a CDN in the production [environment](/script/core#env).

```js
if (Wee.$env() == 'prod') {
    Wee.assets.root('https://cdn.weepower.com');
}
```

You can override the root on individual requests. For instance, you may want to load all your static assets from a CDN but pull JSON or other files from a local server.