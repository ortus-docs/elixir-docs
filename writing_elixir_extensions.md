# Writing Elixir Extensions

## `mergeConfig`

Occasionally you will need to extend Webpack in ways not supported by ColdBox Elixir. In these moments, you can provide your own configuration using the `mergeConfig` method.

```javascript
const elixir = require("coldbox-elixir");

elixir.config.mergeConfig({
    // custom webpack config goes here
});
```

The `mergeConfig` method will merge the object provided with the existing Webpack config using the excellent [`webpack-merge` library](https://github.com/survivejs/webpack-merge).

## Custom Ingredients

Ingredients are the name for the methods available on the `mix` object. You can add an ingredient to your Elixir instance like so:

```javascript
const elixir = require("coldbox-elixir");

elixir.config.addIngredient("nameOfIngredient", () => {
    // function to run when called (mix.nameOfIngredient());
    // any parameters passed to the `mix.nameOfIngredient()` call will be available in the function.
    // The `this` scope refers to the ElixirConfig object, so methods like `this.mergeConfig` are available.
})
```

The main use cases for using an ingredient over custom config are:

1. Need to call multiple times each time for different file\(s\)
2. Want to re-use across projects

Especially in the second case, feel free to publish the ingredient on NPM if you feel it could be useful to other developers.

