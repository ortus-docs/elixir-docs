# Mixing in tasks from ColdBox Modules

ColdBox Modules can be an excellent way to structure your project, and ColdBox Elixir is the perfect companion.  Use all the Elixir methods you know and love in your modules, and Elixir will build them all for you with just one command.

```js
elixir( function( mix ){
	mix.modules();
});
```

## `elixir-module.js`
To specify what Elixir functions to run, a module needs to define an `elixir-module.js` file.  This file looks very similar to a `gulpfile`.  Here is an example of one:

```js
module.exports = function( mix ){
	mix.sass( "app.scss" );
};
```

The function here is exactly the same function you would write inside the `elixir` call in your main `gulpfile`.  Every method installed in your main `gulpfile` is available here. The one **important** difference is that this function must be exported so that Elixir can pick it up and add it to the build steps.

Elixir will scope the changes to the current module's directory.  This means, for example, that:

```js
mix.sass( "app.scss" )
```

Inside of a module with a path `/modules_app/my-module/elixir-module.js` will look for an `app.scss` file inside of `/modules_app/my-module/resources/assets/sass/app.scss` and compile it to `/modules_app/my-module/includes/css/app.css`.

Watch mode works exactly as you would expect — modules add their scoped mixes to the watch tasks just like every other Elixir task.


## Running a Single Module

You can compile a single module's assets by using `mix.module()` passing in the module's name:

```js
// /gulpfile.js
elixir( function( mix ){
	mix.module( "my-module" );
});
```

This will look for the following file: `/modules_app/my-module/elixir-module.js` and add the resulting mix function to the gulp tasks.  If the file does not exist or is not a function, Elixir will show an error and continue on with the other build tasks.

You can pass more than file in by using an array for the first parameter:

```js
// /gulpfile.js
elixir( function( mix ){
	mix.module( [ "my-module", "my-second-module" ] );
});
```

The second and third parameters change the conventions and should be used less frequently.

```js
// /gulpfile.js
elixir( function( mix ){
	mix.module( "my-module", "new_base_directory", "new-filename.js" );
});
```

This would look in `/new_base_direectory/my-module/new-filename.js` for the mix function.

## Running a folder of modules

There is a shortcut to build all compatible modules in with Elixir:

```js
elixir( function( mix ){
	mix.modules();
});
```

You can call this function with no arguments.  It will find all modules in the default base modules directory (`/modules_app`) with the default filename (`elixir-module.js`) and add their tasks to the build.

You can further customize this function by passing in an array of includes directories as the first argument.

```js
elixir( function( mix ){
	mix.modules( [ "modules_app", "lib/modules" ] );
});
```

This will mix all compatible modules in both directories.

Also, you can pass an array of exclude module names as the second parameter.  These modules (if they exist in the source directories) will be ignored.

```js
elixir( function( mix ){
	mix.modules(
		null, /* passing null uses the default of /modules_app */
		[ "my-old-fashioned-module" ]
	);
});
```

Explicitly ignoring modules doesn't need to be done often since modules missing the mix filename (`elixir-module.js` by default) are ignored when calling `mix.modules()`

Finally, the mix filename can be overridden as the third argument:

```js
elixir( function( mix ){
	mix.modules(
		null, /* passing null here uses the default of /modules_app */
		null, /* passing null here uses the defeault of [] */
		"mixfile.js"
	);
});
```

But this is a lot of work for really no benefit, so just stick to the conventions, yeah?