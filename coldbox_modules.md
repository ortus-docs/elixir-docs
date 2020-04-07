# Mixing in tasks from ColdBox Modules

ColdBox Modules can be an excellent way to structure your project, and ColdBox Elixir is the perfect companion. Use all the Elixir methods you know and love in your modules, and Elixir will build them all for you with just one command.

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.modules();
});
```

## `elixir-module.js`

To specify what Elixir functions to run a module needs to define an `elixir-module.js` file. This file looks very similar to your `webpack.config.js`. Here is an example of one:

```js
module.exports = mix => {
    mix.sass("app.scss");
};
```

The function here is exactly the same function you would write inside the `elixir` call in your main `webpack.config.js` file. Every method installed in your main `webpack.config.js` file is available here.

Elixir will scope the changes to the current module's directory. This means, for example, that:

```js
mix.sass("app.scss");
```

Inside of a module with a path `/modules_app/my-module/elixir-module.js` will look for an `app.scss` file inside of `/modules_app/my-module/resources/assets/sass/app.scss` and compile it to `/modules_app/my-module/includes/css/app.css`.

### Includes, Excludes, and File name

You can specify and array of folders to include, folders to exclude, or change the default file name if you wish:

| Argument   | Default Value       |
| ---------- | ------------------- |
| `includes` | `["modules_app"]`   |
| `excludes` | `[]`                |
| `fileName` | `elixir-module.js` |

## Running a Single Module

You can compile a single module's assets by using `mix.module()` passing in the module's name:

```js
// /gulpfile.js
elixir(mix => {
    mix.module("my-module");
});
```

This will look for the following file: `/modules_app/my-module/elixir-module.js` and add the resulting mix function to the gulp tasks. If the file does not exist or is not a function, Elixir will show an error and continue on with the other build tasks.

The second parameter is a configuration object to change the folderName or fileName to look for:

```js
elixir(mix => {
    mix.module("my-module", {
        folderName: "new_base_directory",
        fileName: "new-filename.js"
    });
});
```

## Module alias

If you want use alias for your import in a module, you must use:

```js
import store from '@moduleName/store.js'
```

This would look in `/new_base_directory/my-module/new-filename.js` for the mix function.
