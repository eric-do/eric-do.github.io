---
layout: post
title: "Setting up Webpack for React"
comments: true
---
Continuing on our React development, today we go into using Webpack with React.

Recall from my [previous post](../Set-up-react-env/) you want to set up an environment with MySQL, Nodemon, and Babel.

This time we replace Babel with Webpack. Webpack will build and link your imports so you only need to include a bundle.js in your index.html. It also loads Babel so you don't need to run Babel concurrently.

The evironment in the previous post will then look like this: 
 - [ ] MySQL server
 - [ ] Nodemon (auto builds Node and Express BE, and serves your React app)
 - [ ] Webpack with Babel loader


# Setup
## Webpack
### Importing files
If you're using Webpack, *don't put your script imports in index.html*. You must import them intelligently in your files so webpack can watch for them.

Basically, index.js should look like this:
```javascript
import App from './components/App.jsx';
import ReactDOM from 'react-dom';
import React from 'react';

ReactDOM.render(<App />, document.getElementById('app'));
```

### File structure
Webpack is a little particular about its folder structure. You'll need to organize like below. There can be some differences like calling index.js something like app.js, since it's up to you to state the entry point to webpack.
```
 your-project
        -> client
            -> dist
                -> index.html
            -> src
                -> components
                    -> Component1.jsx
                    -> Component2.jsx
                    -> Component3.jsx
                -> index.jsx
```

### Webpack scripts
Webpack requires the webpack package as well as the webpack cli. You'll also need to install the babel loader, which transpiles ES6, and create a webpack.config.js file.
```
$ npm install webpack --save-dev
$ npm install webpack-cli --save-dev
$ npm install babel-loader @babel/core @babel/preset-env @babel/preset-react --save-dev
$ > webpack.config.js
```

Update package.json to run webpack
```
"scripts": {
    "react-dev": "webpack -d --watch"
  }
```  

Update webpack.config.json to use babel-loader
```javascript
module.exports = {
  entry: __dirname + '/client/src/index.jsx',
     module: {
       rules: [
         {
           test: /\.jsx$/,
           exclude: /node_modules/,
           use: {
             loader: 'babel-loader',
             options: {
              presets: ['@babel/preset-react', '@babel/preset-env']
            }
           }
         }
       ]
     },
    output: {
     filename: 'bundle.js',
     path: __dirname + '/client/dist'
   }
 };
 ```

After all that you're good to go. Just run webpack using the script you wrote earlier.
```
npm run react-dev
```
