# ColdBox Helper Methods

ColdBox v4.3.0 has two methods in the HTML Helper object: `elixir() and elixirPath()` to specifically help with versioned assets exclusively.  

However, you can leverage versioned assets in any version of ColdBox by adding the following methods to your ColdBox Application Helper or Views Helper file that is set in your application's `ColdBox.cfc`.  Please note that these methods are identical to the one in ColdBox v4.3.0:

```js
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
		buildDirectory="build",
		boolean sendToHeader=true,
		boolean async=false,
		boolean defer=false
	){
		html.addAsset(
			elixirPath( arguments.fileName, arguments.buildDirectory ),
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
	string function elixirPath( required string fileName, buildDirectory="build" ){
		var includesConvention 	= "includes";
		var mapping 			= event.getCurrentModule() != "" ? event.getModuleRoot() : controller.getSetting( "appMapping" );
		var filePath 			= expandPath( "#mapping#/#includesConvention#/#arguments.buildDirectory#/rev-manifest.json" );
		var href 				= "#mapping#/#includesConvention#/#arguments.fileName#";
		
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

		return "#mapping#/#includesConvention#/#arguments.buildDirectory#/#json[ arguments.fileName ]#";
	}
</cfscript>
```

You can then just use them in your layouts or views to include versioned files:

```html

<head>
  #elixir( "css/myapp.css" )#
</head>
<body>
   ...

  #elixir( "js/app.js" )#
</body>


```
