# Commands

## Custom

Tap into the Wee CLI with your own commands

You can register your own commands by adding JavaScript files to the `source/commands` directory. The name of the file is exposed as the command name. For instance, “copy.js” would be available as `wee copy`. Here is an example of a command.

```js
(function() {
    'use strict';

    module.exports = function(config) {
        var heading = chalk.bold.underline.cyan;

        console.log(heading('Project'));
        console.log(config.project.name);
        console.log();

        console.log(heading('Options'));
        console.dir(config.options, {
            colors: true
        });
        console.log();

        console.log(heading('Arguments'));
        console.dir(config.args, {
            colors: true
        });
        console.log();
    };
})();
```

A configuration object is passed to the command module with the following properties:

- options - Command line options as defined below
- args - Command line arguments as defined below
-rootPath - The full system path to the root of the project
-project - The entire JSON configuration from wee.json

Options are set in the form of `wee copy:option1:option2` and arguments with `--arg1=value1 --arg2=value2`.

## Init

Create a new project

## Run

Run development server

## Update

Get notified if there is a newer version of Wee

```js
wee update
```