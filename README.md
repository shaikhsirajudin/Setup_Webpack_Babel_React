# Setup_Webpack_Babel_React
Setting up Webpack, Babel and React from scratch
# Webpack
1) For a start, install [node and npm](https://nodejs.org/en/.)

2)create an empty folder. Navigate to it in the terminal.

3)Initialize npm (package.json) by running.

```
>npm init
```

4)Install babel core and it’s loader for webpack.

```

>npm install --save-dev webpack webpack-dev-server
*Tip: you can use npm i instead of npm install

*Tip: to be able to run webpack globally, you’ll need to install it using
>npm i --global webpack

*Create app/js/app.js with a simple console.log('hello world');
*create a webpack config file webpack.config.js with following contains

var path = require('path');
module.exports = {
  context: __dirname + "/app",

  entry: path.resolve("./js/app.js"),

  output: {
    filename: "app.js",
    path: __dirname + "/dist",
  }
};

#This tells webpack that our main application file (app.js) is the entry point, and bundled application should be outputted to the dist folder.
#__dirname is the name of the directory that the currently executing script resides in.

* Run below to generate dist/app.js
>node ./node_modules/webpack/bin/webpack.js

```
