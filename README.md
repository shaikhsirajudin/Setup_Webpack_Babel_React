# Setup_Webpack_Babel_React
Setting up Webpack, Babel and React from scratch
# Webpack
1) For a start, install [node and npm](https://nodejs.org/en/.)

2) create an empty folder. Navigate to it in the terminal.

3) Initialize npm (package.json) by running.

```
>npm init
```

4) Install babel core and it’s loader for webpack.

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

* Run the below to generate dist/app.js
>node ./node_modules/webpack/bin/webpack.js

```
5) Add the Babel transpiler goodness by Install babel core and it’s loader for webpack and presets for ES6 (aka ES2015) and React

```
>npm i --save-dev babel-loader babel-core babel-preset-es2015 babel-preset-react
```
6) Create .babelrc in the project root folder and add presets
```
{
  "presets": [
    "es2015",
    "react"
  ]
}
```
7) Add js/jsx loader to your webpack config, as well as extensions we want to resolve 
```
 resolve: {
    extensions: ['', '.js', '.jsx', '.json']
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loaders: ["babel-loader"]
      }
    ]
  }
  
  * Tip:Webpack accepts the array of the loaders. Loader has a test for the filenames, in our case it matches all of the .js and .jsx files. Then it applies babel loader to it. Basically this will transpile our fancy ES6 to ES5 which can be understood by browsers.
  
```

8) Install react and react DOM
```
>npm i react react-dom --save
```
9) We’ll need file loader for it
```
>npm install file-loader --save-dev
```
10) Update webpack config to add entry
```
  entry: {
    javascript: "./js/app.js",
    html: "./index.html",
  }
```
11) and add loader
```
  {
    test: /\.html$/,
    loader: "file?name=[name].[ext]",
  }
  
  *Tip:Now when we run webpack again, we’ll get index.html and app.js in dist folder.
```
12) Install webpack development server, and run it
```
>npm install --save-dev webpack webpack-dev-server
>node ./node_modules/webpack-dev-server/bin/webpack-dev-server.js
*Tip: Same as with webpack, you can install it globally npm i --global webpack-dev-server and run it using webpack-dev-server.
```
13) Add hot reloading.
```
>npm install react-hot-loader --save-dev
```
14) Update webpack js/jsx loader to use hot reloading
```
  {
    test: /\.jsx?$/,
    exclude: /node_modules/,
    loaders: ["react-hot", "babel-loader"],
  }
```
15) Add two more options when running dev server --hot and --inline. We will also add --history-api-fallback which will be useful when we add react router. This option tells server to fallback to index.html which will handle routing (as we are building single page app).
```
>node ./node_modules/webpack-dev-server/bin/webpack-dev-server.js --hot --inline

*Tip:Not only the hot reload watches the changes and updates the browser, but it injects the code and keeps the application state. Note that not all modules can be replaced. The code in app/js/app.js cannot be reloaded and will cause a full page reload but changing the children components will trigger a hot module replacement.
```
16) To make things easier, we’ll add our script to the package.json file.
```
"scripts": {
    "dev": "node ./node_modules/webpack-dev-server/bin/webpack-dev-server.js --hot --inline --history-api-fallback"
  }
  
  *Tip: Now we can run only >npm run dev
```


