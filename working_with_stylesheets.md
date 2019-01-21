# Working With Stylesheets

Elixir processes all CSS files through Webpack. This brings with it some nifty Webpack properties such as [automatic url resolution](https://github.com/webpack-contrib/css-loader).

# CSS

> Due to the way Webpack processes css files, you can no longer have a css file named `vendor`.

You can mix traditional css with webpack using `mix.css`. You can pass one file or an array of files.

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.css("app.css");
    mix.css([
        "node_modules/normalizecss/normalize.css"
        "resources/assets/css/normalize_overrides.css"
    ], {
        name: "normalize.css",
        entryDirectory: ""
    });
});
```

`mix.css` accepts a configuration object as the second parameter:

```js
{
    name: this.withoutExtension(filename),
    outputDirectory: "includes/css/",
    entryDirectory: "resources/assets/css/"
}
```

# PostCSS

If you add a `postcss.config.js` file to the root of your project, Elixir will process all of your styles through PostCSS.
To learn more about PostCSS, visit [their documentation](https://postcss.org/).

# Sass

The `sass` method allows you to compile [Sass](http://sass-lang.com/) into CSS.
Assuming your Sass files are stored at `resources/assets/sass`, you may use the method like so:

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.sass("app.scss");
});
```

Like the `css` method you may compile multiple Sass files into a single CSS file, and even customize the output directory of the resulting CSS:

```
elixir( function( mix ){
    mix.sass([
        "app.scss",
        "controllers.scss"
    ], {
        outputDirectory: "public/assets/css"
    });
} );
```

# Other Pre-processors

Elixir can be extended with any other pre-processor you would like. See our docs on [writing your own extensions](writing_elixir_extensions.md) for others!
