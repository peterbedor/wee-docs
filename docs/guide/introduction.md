# Introduction

Wee is a front-end framework built and maintained at [Lewis Communications](https://lewiscommunications.com) that provides a powerful set of tools for building websites. It provides a thoughtful workflow to a team or individual's front-end development as well as consolidates and decreases the dependencies required to build a variety of web products.

## Demo
To see Wee in action, we have created a [demo project](https://github.com/weepower/wee-demo). Follow these simple steps to get up and running:

- Clone down the repository - `git clone https://github.com/weepower/wee-demo.git`
- Navigate to the new `wee-demo` directory - `cd wee-demo`
- Install dependencies - `npm install`
- Navigate to the `server` directory
- Install dependencies - `npm install`
- Navigate back to the demo
- Launch site - `npm run demo`
- Open `http://localhost:3000` in a browser of your choice

**Note:** If you already have [wee-cli](https://github.com/weepower/wee-cli) installed, you can combine the last two steps by calling `wee demo`.

We will refer to the this demo site throughout the guide, so it will be helpful to have it set up.

## Getting Started
[wee-cli]: https://github.com/weepower/wee-cli
[wee-core]: https://github.com/weepower/wee-core

To start a new project with Wee, you can do one of the following:

- Install [Wee CLI][wee-cli] - `npm i -g wee-cli`
- Start a new project - `wee init project-name`
- Follow the series of prompts to set up your project

We highly recommend installing [Wee CLI][wee-cli] as it will improve your overall development experience, however it is not required to start a project. You can also:

- Download [Wee](https://github.com/weepower/wee/archive/master.zip)

## Structure
It can be helpful to have a basic knowledge of the internal organization and makeup of Wee in order to fully harness it's potential as well as to troubleshoot potential issues.

### Wee Core
Wee is powered by a single npm package called [Wee Core][wee-core]. You will find it in the list of dependencies in a project's `package.json`. Wee Core contains all the `wee-` prefixed JavaScript modules that are accessible in a standard project. It also contains all the base styling provided by Wee as well as the majority of the [Wee CLI][wee-cli] commands.

### Configuration Files
Wee's build process can be configured by editing a file called `wee.json`. It is located on the top level of a Wee project. These settings are explained in detail in the [Build Configuration](/build/config) documentation.

The other main configuration file for a project is the [package.json](https://docs.npmjs.com/getting-started/using-a-package.json). All project dependencies should be specified in this file.

### Project Structure
There are three top level directories that exist in a Wee project. The names of these directories are configurable in the `wee.json` file:

**Source**

This is where a developer will spend most/all of their time. The code written and the assets added to the source directory is bundled up and optimized by the build process and placed in the `public/assets` directory.

```
source/
    commands/  // Custom CLI commands
    components/
    fonts/
    images/
    scripts/
    styles/
```

**Public**

The `public` directory is the web root of a project. Anything that you want accessible to the browser should go here. Note that nothing should be manually placed in `public/assets` as the build process erases and overwrites the contents of this directory based on the contents of the source directory.

**Build**

The build process tasks and configuration files live inside of the `build` directory.
