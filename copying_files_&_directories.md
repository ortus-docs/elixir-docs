# Copying Files & Directories

The `copy` method may be used to copy files and/or directories to new locations. All operations are relative to the project's `root` directory:


```js
elixir( function( mix ){
    mix.copy( 'vendor/foo/bar.css', 'public/css/bar.css' );
} );

elixir( function( mix ){
    mix.copy( 'vendor/package/views', 'resources/views' );
} );
```

> **Tip**: The first argument can be a file or folder path or an array of paths. You can also use any globbing patterns.