# Configuration Options

All of Elixir's configuration is to support Webpack.  Most of the custom changes you will make to Elixir will
come through the `mergeConfig` method.

```js
const elixir = require("coldbox-elixir");

elixir.config.mergeConfig({});
```

The `mergeConfig` method will intelligently merge your new config with the existing Webpack config (thanks to [`webpack-merge`](https://github.com/survivejs/webpack-merge)).

There are a few additional config options on the Elixir object.

+ `elixir.isProduction`
    + By default checks for the production flag from the terminal (`-p`)
+ `elixir.rootPath`
    + The root of the project
+ `elixir.config`
    + A configured instance of `ElixirConfig`
+ `elixir.versioning`
    + Defaults to `elixir.isProduction`
