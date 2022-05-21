# ic_bare_react_app

## Install React dependency.

npm i react react-dom

## Install Dev dependencies (Webpack, css, sass, babel presets and webpack loaders)

Install transpilers for react
npm i -D @babel/core @babel/preset-env @babel/preset-react

Install loader for babel
npm i -D babel-loader file-loader css-loader sass-loader sass

Install webpack
npm i -D webpack webpack-cli webpack-dev-server

## Configure .babel.rc or babel.config.js

```
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

```
module.exports = {
    presets:[
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
```


## Configure webpack.config.js

const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
    output: {
        path: path.join(__dirname, '/dist'),
        filename: 'index.bundle.js',
    },
    devServer: {
        port: 3010,
        watchContentBase: true,
    },
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            },
            {
                test: /\.scss$/,
                use: [
                    MiniCssExtractPlugin.loader,
                    'css-loader',
                    'sass-loader',
                ],
            }
        ]
    },
    plugins: [new MiniCssExtractPlugin()],
};

## Create React App

index.html -> entry point for the file

index.js -> will result in index.bundle.js which will be loaded by index.html

App.js -> will be loaded from index.js/index.bundle.js

App.csss -> style sheet etc

## build the React Webapp
package.json
script 
   "build": "webpack"

