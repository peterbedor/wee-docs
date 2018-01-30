# CLI

Wee includes an extensible CLI with useful default [commands](/cli/commands). Wee 4 makes starting a new project easy by adding the [init](/cli/commands/init) command, and the CLI was remade on top of [Commander](https://www.npmjs.com/package/commander) to make a more consistent and robust CLI experience. This guide is going to explain how to register custom commands for your project as well as how best to utilize the CLI's built in functionality.

## In and Out of a Project
The majority of Wee's commands are registered within [Wee Core](https://github.com/weepower/wee-core). As a result, the help menu `wee --help` seen before creating your first project will not contain most commands listed in the documentation. When `wee --help` is executed inside of a project, the full menu of commands will be available.

## Custom Commands
Wee CLI makes it possible to generate and register your own commands. Inside of a current wee project, do the following:

- Generate a new command with the CLI - `wee command -n new-command`
- Configure the newly generated command. It will be located in `source/commands/new-command.js`

The `new-command.js` file will look something like this:

```javascript
const { logError, logSuccess } = require('../../node_modules/wee-core/utils');

module.exports = {
	name: 'newCommand',
	description: 'newCommand description here',
	usage: '- wee newCommand [options]',
	options: [
		['-t, --test <name>', 'option with a value'],
		['-t2, --test2', 'option without a value']
	],
	action(config, options) {
		// Require test option be provided
		// if (typeof options.test !== 'string') {
		// 	logError('--test is required');
		// 	process.exit();
		// }

		logSuccess('newCommand command successful');
	}
};
```

The command can now be executed as `wee newCommand`. It will print `newCommand command successful` to the terminal when called. Let's look at the properties of this command:

- `name` - The name by which the command is registered.
- `description` - The description that will be printed out in the CLI help menu. Make sure to update this property.
- `usage` - The value will output to the help menu for the `newCommmand`.
- `options` - The set of possible flags that can be passed in with the command.
- `action` - The logic of the command.

A couple helper functions are imported into the command: `logError` and `logSuccess`. These can be used when needing to print feedback to the terminal in a formatted way.

An important note is that [ES Modules](/guide/es-modules) are not used in commands. This is because we are using the module system used in Node.js (CommonJS), the platform that Wee CLI and the build process are built on. So if you need to import any dependencies into a command, use `require` instead of `import`.

## Wee 3
If you have projects that are using Wee 3, you will notice that the v2 of Wee CLI is not compatible. This could make it difficult since Wee CLI is most likely globally installed on your machine. A workaround for this is to install [wee3-cli](https://www.npmjs.com/package/wee3-cli).

```bash
npm i -g wee3-cli
```

Once installed, you can refer to the Wee 3 compatible CLI with `wee3` as the command.

```bash
wee3 run:local
```

You can also install a Wee 3 compatible version locally per project if you would rather.

```bash
cd /to/project/directory
npm install wee-cli@1.1.0
```

Once installed locally , you can utilize npm to run your local version of the CLI by creating an npm script in your project's `package.json`. When calling a CLI command inside of an npm script, npm first looks for the executable inside of your local `node_modules`. So for example, we could add a script called `start` that will call the CLI command.

```json
"scripts": {
	"start": "wee"
}
```

Now when you run `npm start` in the console, you should notice that your `defaultCommand` that is defined in your `wee.json` is executed. If you need to add additional arguments, add `--` in between the npm script and your arguments.

```bash
npm start -- run:local
```
