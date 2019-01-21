# Installation & Setup

## Installing Node

Before triggering Elixir, you must first ensure that [Node.js](https://nodejs.org/en/) is installed on your machine.
You will want at least the latest LTS version of Node.

```
node -v
```

## Installing ColdBox Elixir

If you generate a ColdBox application using any of our [elixir templates](https://github.com/coldbox-templates/) then you will find a `package.json` file in the root of the application already. Think of this like your `box.json` file, except it defines Node dependencies instead of ColdFusion (CFML) dependencies.  A typical example can look like this:


```js
{
  "private": true,
  "devDependencies": {
    "coldbox-elixir": "^3.0.0"
  }
}
```

It defines ColdBox Elixir as a dev dependency.  You may then install the dependencies it references by running:

```
npm install
```

This will install ColdBox Elixir and its dependencies into the `node_modules` folder in your root.  This folder has been already added to the `.gitignore` file as well, so no need to further ignore it.
