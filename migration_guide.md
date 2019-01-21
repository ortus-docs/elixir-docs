# Migration Guide

If you used a previous version of ColdBox Elixir a lot has changed. This guide will step you through the changes.

## Dependencies

ColdBox Elixir no longer requires `gulp`. You can uninstall it.

ColdBox Elixir will install all necessary dependencies when installing or updating it from NPM.
There are other dependencies which may be installed on-demand once as you use them.

## Running Elixir

Since ColdBox Elixir doesn't use `gulp` any more, we need to make some changes to our `gulpfile.js`.

1. Rename `gulpfile.js` to `webpack.config.js`.
2. Export the result of `elixir()`

```js
// webpack.config.js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    // ....
});
```

3. (Optional) Create some NPM scripts to make build commands easier to remember. This let's us run `npm run dev` or `npm run watch` to build our project.

```json
{
    "scripts": {
        "dev": "webpack",
        "watch": "npm run dev -- --watch",
        "build": "npm run dev -- -p"
    }
}
```

## Asset Names

Due to the way Webpack processes css files, you can no longer have a css file named `vendor`.

## Tasks

The following tasks have been removed from ColdBox Elixir.

-   `mix.less`
-   `mix.combine`
-   `mix.browserify`
-   `mix.rollup`
-   `mix.exec`

If you rely on any of these methods you can either stay with ColdBox Elixir v2
or you can [recreate the task yourself.](writing_elixir_extensions.md)

## Method Changes

### `mix.styles`

`mix.styles` should be replaced with `mix.css`.

The method signature for `mix.css` is has changed.

| Name                    | Type   | Required | Default                                        | Description                                                                      |
| ----------------------- | ------ | -------- | ---------------------------------------------- | -------------------------------------------------------------------------------- |
| filename                | String | `true`   |                                                | The filename to bundle.                                                          |
| options                 | Object | `false`  | (see below)                                    | An object for additional options. Any missing keys will use their default value. |
| options.name            | String | `false`  | The name of the filename without the extension | The name of the outputed bundle                                                  |
| options.outputDirectory | String | `false`  | `includes/css`                                 | The output directory for the built file.                                         |
| options.entryDirectory  | String | `false`  | `resources/assets/css/`                        | The directory where the filename is located.                                     |

### `mix.scripts`

`mix.scripts` should be replaced with [`mix.js`](working_with_scripts.md). `mix.js` will automatically run the
code through Babel. Babel is preconfigured with `babel-preset-env`, but it can be customized by specifying
your own `.babelrc` file in the root of your project. See the [Babel docs](https://babeljs.io/docs/en/babelrc)
for more information.

The method signature for `mix.scripts` has changed.

| Name                    | Type   | Required | Default                                        | Description                                                                      |
| ----------------------- | ------ | -------- | ---------------------------------------------- | -------------------------------------------------------------------------------- |
| filename                | String | `true`   |                                                | The filename to bundle.                                                          |
| options                 | Object | `false`  | (see below)                                    | An object for additional options. Any missing keys will use their default value. |
| options.name            | String | `false`  | The name of the filename without the extension | The name of the outputed bundle                                                  |
| options.outputDirectory | String | `false`  | `includes/js`                                  | The output directory for the built file.                                         |
| options.entryDirectory  | String | `false`  | `resources/assets/js/`                         | The directory where the filename is located.                                     |

### `mix.webpack`

`mix.webpack` should be replaced with either [`mix.js`](working_with_scripts.md) or [`mix.vue`](vuejs_integration.md)
depending on your use case. `mix.vue` includes some extra dependencies and configuration to process `.vue` files
while `mix.js` will just process your files through Babel.

The method signature for `mix.js` and `mix.vue` are the same.

| Name                    | Type   | Required | Default                                        | Description                                                                      |
| ----------------------- | ------ | -------- | ---------------------------------------------- | -------------------------------------------------------------------------------- |
| filename                | String | `true`   |                                                | The filename to bundle.                                                          |
| options                 | Object | `false`  | (see below)                                    | An object for additional options. Any missing keys will use their default value. |
| options.name            | String | `false`  | The name of the filename without the extension | The name of the outputed bundle                                                  |
| options.outputDirectory | String | `false`  | `includes/js`                                  | The output directory for the built file.                                         |
| options.entryDirectory  | String | `false`  | `resources/assets/js/`                         | The directory where the filename is located.                                     |

### `mix.sass`

The method signature for `mix.sass` has changed.

| Name                    | Type   | Required | Default                                        | Description                                                                      |
| ----------------------- | ------ | -------- | ---------------------------------------------- | -------------------------------------------------------------------------------- |
| filename                | String | `true`   |                                                | The filename to bundle.                                                          |
| options                 | Object | `false`  | (see below)                                    | An object for additional options. Any missing keys will use their default value. |
| options.name            | String | `false`  | The name of the filename without the extension | The name of the outputed bundle                                                  |
| options.outputDirectory | String | `false`  | `includes/css`                                 | The output directory for the built file.                                         |
| options.entryDirectory  | String | `false`  | `resources/assets/sass/`                       | The directory where the filename is located.                                     |

### `mix.version`

Versioning is now the default for a production build (`webpack -p`). You can also control if the files are versioned
by setting the `elixir.versioning` config property in your `webpack.config.js` file.

### `mix.stylesIn` and `mix.scriptsIn`

These methods should be replaced with individual calls to `mix.css` and `mix.js`.

## Extensions

Extensions that were made for ColdBox Elixir v2 are not compatible with v3.
See [_Writing Elixir Extensions_](writing_elixir_extensions.md) for more information
on how to create v3 compatible extensions.

## Elixir Config File

The Elixir config file has changed completely.
The available configuration options are available in [_Configuration Options._](configuration_options.md)
