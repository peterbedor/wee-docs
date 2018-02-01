# Commands

Wee includes an extensible CLI with some useful default commands

## Make

Quickly scaffold core Wee structures

### Controller

| Variable | Type   | Default | Description                       | Required |
|----------|--------|---------|-----------------------------------|----------|
| name     | string | -       | camelCase controller name         | ✔        |
| type     | string | base    | Define controller template to use | -        |

```bash
wee make:controller --name=controllerName
```

You can also create a controller using the `extensions` or `api` template by specifying the type name.

In this case, the type is also used as the name variable.

The Extensions controller allows you to use several chainable variations of `-is-active` and `-is-disabled classes`.

```bash
wee make:controller --type=extensions
```

```js
Wee.fn.make('extensions', {
    _construct: function() {
        var disabled = '-is-disabled',
            active = '-is-active';

        $.chain({
            disable: function() {
                this.addClass(disabled);

                returnthis;
            },

            enable: function() {
                this.removeClass(disabled);
            },

            isDisabled: function() {
                returnthis.hasClass(disabled);
            },

            isEnabled: function() {
                return ! this.hasClass(disabled);
            },

            activate: function() {
                this.addClass(active);

                returnthis;
            },

            deactivate: function() {
                this.removeClass(active);

                returnthis;
            },

            isActive: function() {
                returnthis.hasClass(active);
            },

            isInactive: function() {
                return ! this.hasClass(active);
            }
        });
    }
});
```

The API controller scaffolding provides a convenient interface to Wee’s data request, allowing you to consolidate your data request logic in one place.

```bash
wee make:controller --type=api
```

```js
Wee.fn.make('api', {
    get: function(conf) {
        this.$private.send(conf);
    },

    post: function(conf) {
        this.$private.send(Wee.$extend(true, {
            method: 'post'
        }, conf));
    },

    put: function(conf) {
        this.$private.send(Wee.$extend(true, {
            method: 'put'
        }, conf));
    },

    delete: function(conf) {
        this.$private.send(Wee.$extend(true, {
            method: 'delete'
        }, conf));
    }
}, {
    send: function(conf) {
        Wee.fetch.request(conf);
    }
});
```

### Module

| Variable    | Type    | Default | Description                 | Required |
|-------------|---------|---------|-----------------------------|----------|
| name        | string  | -       | camelCase module name       | ✔        |
| author      | string  | -       | Module author               | -         |
| autoload    | boolean | true    | autoload toggle             |  -        |
| extension   | boolean | false   | Extension toggle            |   -       |
| website     | string  | -       | Website reference           |    -      |
| description | string  | -       | Internal module description | -        |

```bash
wee make:module --name=moduleName --extension=true
```

### Test

| Variable | Type   | Default | Description           | Required |
|----------|--------|---------|-----------------------|----------|
| name     | string | -       | Title Cased test name | ✔        |

```bash
wee make:test --name="Test Name"
```

## Reset

Remove unnecessary files and sample assets from the default install

```bash
wee reset
```

## Validate

Enforce code quality and formatting

Wee leverages [JSHint](jshint.com) and [JSCS](jscs.info) for automatic and manual code validation. JSHint serves as more of a high-level quality check and JSCS is focused on code consistency and formatting. In wee.json you can disable either independently or point them to custom configurations.

To run validation on demand execute the command below

```bash
wee validate
```
