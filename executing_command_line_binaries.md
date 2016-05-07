# Executing Command Line Binaries

You may use the `exec()` method to execute any command line shell script.  Just pass a normal string that will be evaluated by the shell of the Operating System you are on. Like CommandBox integration for example!

```js
elixir( function( mix ){
	mix.exec( "box testbox run" );
} );
```

## Attaching Watchers

You can also attach a watcher to the command execution.  Let's say you want all the Tests to execute if there are any changes to them:

```js
elixir( function( mix ){
	mix.exec( "box testbox run", "tests/**/*.cfc" );
} );
```
