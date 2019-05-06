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
        name: "bootstrap",
        entryDirectory: ""
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

## `runtime.js` and `vendor.js`

Using `mix.js` or any methods that depend on it create up to two additional files
that you should be aware of: `runtime.js` and `vendor.js`. `runtime.js` is the
Webpack runtime and should be included as the first script on your page.  Without
this script, your other files will fail silently.  The `vendor.js` is comprised
of any dependencies pulled from `node_modules`.  This allows your users to keep
using the cached `vendor.js` file even when you change your application code.
This file should be included after `runtime.js` and before any of your application
code.
