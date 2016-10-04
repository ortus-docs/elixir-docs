# Changelog

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