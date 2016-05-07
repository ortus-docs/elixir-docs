# Versioning Cache Busting

Many developers suffix their compiled assets with a timestamp or unique token to force browsers to load the fresh assets instead of serving stale copies of the code. Elixir can handle this for you using the `version` method.

The `version` method accepts a file name relative to the `includes` directory, and will append a unique hash to the filename, allowing for cache-busting. For example, the generated file name will look something like: `all-16d570a7.css`:

```js
elixir( function( mix ){
    mix.version( 'css/all.css' );
} );
```

## Versioning Multiple Files

You may pass an array to the `version` method to version multiple files:

```js
elixir( function( mix ){
    mix.version( [ 'css/all.css', 'js/app.js' ] );
} );
```

## Custom Output Directory
By default the `version` task will create a `build` folder in your `includes` folder that will contain a revision json file and the versioned assets according to `js` or `css` type.  You can change the destination using the second argument:

```js
elixir( function( mix ){
    mix.version( [ 'css/all.css', 'js/app.js' ], "includes/versioned" );
} );
```

