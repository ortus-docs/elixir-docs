# Changelog

## 3.0.0
- **Major upgrade** to ColdBox Elixir.  No longer mirroring Laravel Elixir.
- All compilation is done through Webpack instead of Gulp.
- Removed the following methods:
    - `mix.less`
    - `mix.stylus`,
    - `mix.scripts`
    - `mix.scriptsIn`
    - `mix.webpack`
    - `mix.browserify`,
    - `mix.rollup`
    - `mix.version`
    - `mix.exec`
    - `mix.task`
- The entire Elixir configuration object has changed.  See [Configuration Options](configuration_options.md) for details.
- PostCSS support is now automatic if a `postcss.config.js` file is found in the project root.
- The `elixir` and `elixirPath` helper functions in ColdBox 5.0.0 and earlier are incompatible with ColdBox Elixir 3.0.0.  Please see the [Versioning docs](versioning.md) for updated helper functions.


## 2.0.0
- Updated to stay current with Laravel Elixir 6.0.0.
- Deprecated `mix.babel()` in favor of `mix.browserify()`, `mix.webpack`, `mix.rollup`, or similar module bundlers.
- Nicer console output.
- Broke out first party extensions from the core (to keep in line with Laravel Elixir 6.0.0)
    - [`coldbox-elixir-browserify`](https://github.com/coldbox-elixir/extension-browserify)
    - [`coldbox-elixir-browsersync`](https://github.com/coldbox-elixir/extension-browsersync)
    - [`coldbox-elixir-rollup`](https://github.com/coldbox-elixir/extension-rollup)
    - [`coldbox-elixir-stylus`](https://github.com/coldbox-elixir/extension-stylus)
    - [`coldbox-elixir-vue`](https://github.com/coldbox-elixir/extension-vue)
    - [`coldbox-elixir-webpack`](https://github.com/coldbox-elixir/extension-webpack)
- Helpful warnings when trying to use methods provided by a first party extension.


## 1.1.0
- Travis Support
- BDD via TestBox fixes
- Updated all dependencies to latest versions
- Gulp tasks for compilation, tests and watchers
- Test App additions for testing direct gulp integrations
- If not tasks defined in the user's gulpfile, just a message is shown instead of an exception
- Removed coffeescript support, no longer needed
- Added new config map for `appPaths` to support all ColdBox conventions
- Vueify core support view browserify for Vue.js components
- Included a new `template` folder which helps setting up new elixir based projects


## 1.0.0
- Initial Port to ColdBox
