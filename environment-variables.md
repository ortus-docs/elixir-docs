# Environment Variables

You will occassionally need to access environment variables in your JavaScript.  This is done using the `process.env` object like so: `process.env.YOUR_KEY_HERE`. But your user's browser won't have access to a `process` object.  How will we handle this?

### Webpack's EnvironmentPlugin

Webpack uses the [`EnvironmentPlugin`](https://webpack.js.org/plugins/environment-plugin/) to do this.  It takes an array of environment variable names to allow in your application.  Then all instances of `process.env.YOUR_KEY_HERE` will be replaced with the value in your environment. 

{% code title="Environment" %}
```bash
NODE_ENV=development
```
{% endcode %}

{% code title="webpack.config.js" %}
```javascript
module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.EnvironmentPlugin(["NODE_ENV"]),
  ]
};
```
{% endcode %}

{% code title="Source File" %}
```javascript
console.log(process.env.NODE_ENV);
```
{% endcode %}

{% code title="Output File" %}
```javascript
console.log("development");
```
{% endcode %}

If the environment variable allowed is missing, an error will be thrown during compilation, ensuring that you don't accidentally ship code without this value.

In addition to passing an array of key names, you may pass an object with the keys being environment variable names and the values being default values if the keys are not found in the environment.

{% code title="webpack.config.js" %}
```javascript
module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.EnvironmentPlugin({
      NODE_ENV: "development"
    }),
  ]
};
```
{% endcode %}

### mix.env

To make this process easier, Elixir has a `mix.env` method that passes through to `EnvironmentPlugin`.

{% code title="webpack.config.js" %}
```javascript
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
  mix.env(["NODE_ENV"]);  
});
```
{% endcode %}

This is the easiest way to define the environment variables your JavaScript bundle needs.

### Automatic NODE\_ENV

`NODE_ENV` is a very common environment variable used by many libraries to output additional debugging information or to enable optimizations.  Since Elixir already knows what environment you are building for, this value is defaulted for you.  If you desire to override that value, just define `NODE_ENV` in your environment and it will take precendence.

