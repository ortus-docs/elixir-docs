# Calling Gulp Tasks

If you need to call an existing Gulp task from Elixir, you may use the `task` method. As an example, imagine that you have a Gulp task that simply speaks a bit of text when called:

```
gulp.task( 'speak', function() {
    var message = 'Tea...Earl Grey...Hot';

    gulp.src( '' ).pipe( shell( 'say ' + message ) );
});
```

If you wish to call the `speak` task from Elixir, use the `mix.task` method and pass the `name` of the task as the only argument to the method:

```js
elixir( function( mix ){
    mix.task( 'speak' );
});
```

## Custom Watchers

If you need to register a watcher to run your custom task each time some files are modified, pass a regular expression as the second argument to the `task` method:

```
elixir( function( mix ){
    mix.task( 'speak', 'tests/**/*.cfc' );
});
```
