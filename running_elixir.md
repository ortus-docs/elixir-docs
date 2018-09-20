# Running Elixir

Elixir is built on top of Webpack, so to run your Elixir tasks you only need to run the `webpack` command in your terminal.
Before running Webpack, you will need a `webpack.config.js` file in the root of your project.  Below is a simple example:

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.js("app.js");
});
```

Please note that by adding the `-p` flag to the command will turn on Webpack's production mode.
This will minify your CSS and JavaScript files as well as add long-term caching hashes to your compiled files.

## Watching Assets For Changes

For performance and convienence, you can run Webpack in watch mode by passing the `-w` or `--watch` flag.  Any changes
to your source files will automatically re-run your build.  Note that your build will be significantly faster on
subsequent changes than when running Webpack from scratch.

## NPM Scripts

The easiest way to run Webpack is to set up some NPM scripts.  Here are the following we recommend:

```json
"scripts": {
    "dev": "webpack --hide-modules",
    "watch": "npm run dev -- --watch",
    "prod": "npm run dev -- -p"
}
```

Then from the terminal you can run `npm run [scriptName for this example either dev, watch or prod]` to run the associated script.
