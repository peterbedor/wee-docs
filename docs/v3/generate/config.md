# Config

The site generator is setup through a simple JSON-based configuration file to define the project structure and output.

## Config

The config object allows you to enable or disable core generator features.

```
"config": {
    "watch": true,
    "minify": true,
    "enhanceTypography": true,
    "removeIndex": true,
    "removeTrailingSlashes": true,
    "paths": {
        "content": "content",
        "helpers": "helpers",
        "partials": "partials",
        "target": "../../../public/guide/",
        "templates": "templates"
    }
}
```

### Watching


Setting this to true will set the Wee build process to watch for changes.

```
"watch": true
```

### Minification


When true the output HTML with be minified.

```
"minify": true
```

### Enhance Typography


Smart quotes and other typographic features can be enabled here.

```
"enhanceTypography": true
```

### Indexes


This will remove index.html from any path references. This should be used in conjunction with web server rewrite rules.

```
"removeIndex": true
```

### Trailing Slashes


Similar to removeIndex, this will remove trailing slashes from any output paths.

```
"removeTrailingSlashes": true
```

### Paths


Here you can set the default root paths for content, helpers, partials, and templates. By default they are at the same level as the site config file. You also set the target path which is where the output section targets are relative to.

```
"paths": {
    "content": "content",
    "helpers": "helpers",
    "partials": "partials",
    "target": "../../../public/guide/",
    "templates": "templates"
}
```

## Data

Any custom data that you may need for your site can be stored here. They can be nested as deep as necessary and the values are accessible in the templates.

```
"data": {
    "version": "2.1.0",
    "analyticsID": "UA-XXXXXXXX-1",
    "social": {
        "twitter": "weecss",
        "googlePageID": "+weecss"
    }
}
```

You can use them for paths and versions for instance.

```
<scriptsrc="/js/script.min.js?v"></script>
```

Data can also be set or overridden in individual content files or within the [section configuration](/docs/v3/generator/config?id=sections).

## Env

This is where you can specify environment-specific config values for use in your templates.

```
"env": {
    "prod": {
        "domain": "https://www.weepower.com",
        "cdnUrl": "https://cdn.weepower.com"
    },
    "default": {
        "domain": "https://weepower.dev",
        "cdnUrl": ""
    }
}
```

Here are a couple examples of how you might use them.

```

{{ #site.env|is('prod') }}
    <script>// Google Analytics script
    ga('create', '{{ site.analyticsID }}', 'auto');
    ga('send', 'pageview');
    </script>
{{ /site.env }}

```

### Environment Building


To compile your project for an environment other than the default pass the env argument to the generate command.

```
wee run:generate --env=prod
```

## General

These values are for your internal reference only.

```
"name": "Site Name",
"description": "Site description."
```