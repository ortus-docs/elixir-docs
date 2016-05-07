# Installation & Setup

## Installing Node

Before triggering Elixir, you must first ensure that [Node.js](https://nodejs.org/en/) is installed on your machine.

```
node -v
```

## Installing Gulp

Next, you'll want to pull in Gulp as a global NPM package so you have it available for any ColdBox application.

```
npm install --g gulp
```

If you use a version control system, you may wish to run the npm [shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap) to lock your NPM requirements:

```
npm shrinkwrap
```
 
Once you have run this command, feel free to commit the `npm-shrinkwrap.json` into source control.

## Installing ColdBox Elixir

The only remaining step is to install Elixir! If you generate a ColdBox application using any of our [elixir templates](https://github.com/coldbox-templates/) then you will find a `package.json` file in the root of the application already. Think of this like your `box.json` file, except it defines Node dependencies instead of ColdFusion (CFML) dependencies.  A typical example can look like this:


```js
{
  "private": true,
  "devDependencies": {
    "gulp": "^3.9.1"
  },
  "dependencies": {
    "bootstrap-sass": "^3.3.6",
    "coldbox-elixir": "^1.1.0",
    "jquery": "^2.2.3"
  }
}
```

It defines ColdBox Elixir, Bootstrap and jQuery as your dependencies.  You may then install the dependencies it references by running:

```
npm install
```

This will install ColdBox Elixir, Bootstrap and jQuery into the `node_modules` folder in your root.  This folder has been already added to the `.gitignore` file as well, so no need to further ignore it.

> **Note** : If you are developing on a Windows system or you are running your VM on a Windows host system, you may need to run the `npm install` command with the `--no-bin-links` switch enabled: `npm install --no-bin-links`

<br>

> **Tip** : If you are integrating with Vue.js, please see our [Vue.js](https://github.com/ColdBox/elixir/wiki/Vue.js-Integration) section
