# html-webpack-scripts-plugin
`html-webpack-scripts-plugin` is a plugin for [Webpack](https://webpack.js.org/).

## Why
By default Webpack will generate plain scripts with like `/bundle/vendor.0a78e31b5c440.js`. In order to serve these script assets and  other generated assets by Webpack (like stylesheets) you should have index.html file and include those assets manually or a plugin that generates HTML and includes those assets automatically, like [`html-webpack-plugin`](https://www.npmjs.com/package/html-webpack-plugin).
More likely you'll use the second option and generate HTML automatically.

However [`html-webpack-plugin`](https://www.npmjs.com/package/html-webpack-plugin) will add plain scripts into generated HTML like
`<script type="text/javascript" src="/bundle/vendor.0a78e31b5c440.js"></script>`. It won't give you additional control over those scripts.

But if you want to get additional control over those scripts `html-webpack-scripts-plugin` will help!

Usage
----------------------
##### Add specific attributes like `async` `defer` `id` `charset`:
```js

// webpack.config.js

let HtmlWebpackScriptsPlugin = require('html-webpack-scripts-plugin')
...
module.exports = {
...
  plugins: [
    new HtmlWebpackScriptsPlugin({
      'defer charset=utf8': /vendor/,
      'async id=appscript': /app/
     })
  ]
}
```

##### Add custom attributes like `data-*`
```js
```

##### Make scripts inline:
```js
// vendor.0a78e31b5c440.js (generated by webpack)
var helloWebpack = 'hello webpack'

// app.4234fe71c300ea.js (generated by webpack)
var app = 'App'
var hello = 'hello'
var helloWebpack = app + hello
console.log(helloWebpack)
```
```js
// Generated scripts by containing 'vendor'
plugins: [
  new HtmlWebpackScriptsPlugin({ inline: /vendor/ })
 ]
```
=>
```js
<script type="text/javascript">
var helloWebpack = 'hello webpack'
</script>

<script type="text/javascript">
var app = 'App'
var hello = 'hello'
var helloWebpack = app + hello
console.log(helloWebpack)
</script>

```
