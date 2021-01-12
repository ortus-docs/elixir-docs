# ContentBox Integration

ColdBox Elixir has a few helper methods when working in a ContentBox app.

```javascript
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.themes();
    mix.contentbox();
});
```

These two methods work just like a call to `mix.modules` with some different defaults set.

> For a refresher on how `mix.modules` and `elixir-module.js` files work, see the [modules docs.](coldbox_modules.md)

## `mix.themes`

This method will look inside the `modules_app/contentbox-custom/_themes` directory for any folders with a `elixir-theme.js` file. The `elixir-theme.js` file is identical to a `elixir-module.js` file.

## `mix.contentbox`

This method will look inside the `modules_app/contentbox-custom/_modules` directory for any folders with a `elixir-module.js` file.

