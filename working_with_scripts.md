# Working With Scripts

You can compile scripts using the `mix.js` method. It accepts either a single file or an array of files to combine.
Each file will be crawled for dependencies by Webpack.

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.js("app.js");
    mix.js([
        "node_modules/jquery/dist/jquery.min.js",
        "node_modules/bootstrap-sass/assets/javascripts/bootstrap.min.js"
    ], {
        name = "vendor",
        entryDirectory = ""
    });
});
```

The second argument to `mix.js` is a configuration object.

```js
{
    name: this.withoutExtension(filename),
    outputDirectory: "includes/js/",
    entryDirectory: "resources/assets/js/"
}
```
