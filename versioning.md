# Versioning Cache Busting

By default, Elixir will version all your compiled assets when compiling for production `webpack -p`.

This produces a file with a unique hash in the filename. This hash will only change if the contents of the file change.

You can change or turn off the versioning by setting the `elixir.versioning` property in your `webpack.config.js` file.

Additionally, Elixir will generate an `/includes/manifest.json` file. This file maps the original file name to the hashed file name. This lets you still use the original file name in your code and not have to update your templates whenever your assets change.

ColdBox \(5.1+\) ships with some helper methods for this purpose. You can also copy the code below for use in your own projects.

```javascript
<cfscript>
    /**
    * Adds the versioned path for an asset to the view
    * @filename The asset path to find relative to the includes convention directory
    * @buildDirectory The build directory inside the includes convention directory
    * @sendToHeader Send to the header via htmlhead by default, else it returns the content
    * @async HTML5 JavaScript argument: Specifies that the script is executed asynchronously (only for external scripts)
    * @defer HTML5 JavaScript argument: Specifies that the script is executed when the page has finished parsing (only for external scripts)
    */
    function elixir(
        required filename,
        boolean sendToHeader=true,
        boolean async=false,
        boolean defer=false
    ){
        html.addAsset(
            elixirPath( arguments.fileName ),
            arguments.sendToHeader,
            arguments.async,
            arguments.defer
        );

        return this;
    }

    /**
    * Finds the versioned path for an asset if leveraging ColdBox Elixir
    * @returns The path
    */
    string function elixirPath( required string fileName ){
        var includesConvention     = "includes";
        var mapping             = event.getCurrentModule() != "" ? event.getModuleRoot() : controller.getSetting( "appMapping" );
        var filePath             = expandPath( "#mapping#/#includesConvention#/manifest.json" );
        var href                 = "#mapping#/#includesConvention#/#arguments.fileName#";

        if ( ! fileExists( filePath ) ) {
            return href;
        }

        var fileContents = fileRead( filePath );
        if ( ! isJSON( fileContents ) ) {
            return href;
        }

        var json = deserializeJSON( fileContents );
        if ( ! structKeyExists( json, arguments.fileName ) ) {
            return href;
        }

        return "#mapping#/#includesConvention#/#json[ arguments.fileName ]#";
    }
</cfscript>
```

You can then just use them in your layouts or views to include versioned files:

```markup
<head>
    #elixir( "css/myapp.css" )#
</head>
<body>
    <!-- ... -->

    <script src="#elixirPath( "js/app.js" )#"></script>
</body>
```

