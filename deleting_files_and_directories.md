# Deleting Files & Directories

By default the following directories are cleaned out for each build:

```text
"includes/js"
"includes/css"
"includes/fonts"
"includes/media"
"includes/images"
```

If you would like to add additional directories, you can do so by configuring a new instance of the `CleanWebpackPlugin`:

```javascript
const elixir = require("coldbox-elixir");
const CleanWebpackPlugin = require("clean-webpack-plugin");

elixir.config.mergeConfig({
    plugins: [
        new CleanWebpackPlugin(["my/custom/directory"], { root: elixir.rootPath })
    ]
});
```

