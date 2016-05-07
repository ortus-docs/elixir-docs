# BrowserSync


[BrowserSync](https://www.browsersync.io/) automatically refreshes your web browser after you make changes to your front-end resources. You can use the `browserSync` method to instruct Elixir to start a BrowserSync server when you run the `gulp watch` command:

```js
elixir( function( mix ){
    mix.browserSync();
});
```

After running this command you will see directions to add a script tag to the bottom of your website like this:

```bash
[BS] Copy the following snippet into your website, just before the closing </body> tag
<script id="__bs_script__">//<![CDATA[
    document.write("<script async src='http://HOST:3000/browser-sync/browser-sync-client.2.12.5.js'><\/script>".replace("HOST", location.hostname));
//]]></script>
```

Add that snippet to your `layouts/Main.cfm` file and reload to enable BrowserSync!

## Specifying a Proxy

Instead of copying the script tag into you app, you can tell BrowserSync to proxy your existing CFML server:

```cfc
elixir( function( mix ){
    mix.browserSync( {
        proxy : 'localhost:50608'
    } );
} );
```

Running `gulp watch` will now open up `localhost:3000` which proxies to your app!  No need for that BrowserSync script tag anymore!

## Custom Options

In addition to the `proxy` option, you may pass any BrowserSync option here as the first argument.  A list of the BrowserSync options can be found [here](http://www.browsersync.io/docs/options/).

