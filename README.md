# Convert the dfx web asset canister to a React App

This sample project converts the dfx-created web app into a react app.
The contents of this directory are the results of steps described in the README.md

You can clone this repository and use it as an initial template to host a React
WebApp on the IC.  Or you can initialize are new dfx project and follow the
steps described here.


# Steps:

## Install React dependency.

```
npm i react react-dom
```


## Install Dev dependencies (Webpack, css, sass, babel presets and Webpack loaders)

Install loader for babel
```
npm i -D babel-loader file-loader css-loader sass-loader sass
```


Install Webpack
```
npm i -D Webpack Webpack-cli Webpack-dev-server
```

Install transpilers
```
npm i -D @babel/core @babel/preset-env @babel/preset-react
```


## Configure .babel.rc or babel.config.js

babel.config.js
```
module.exports = {
    presets:[
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
```

babel.rc
```
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```


## Configure Webpack.config.js
```
const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
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
```


## Create React App

index.html -> entry point for the file

index.js -> will result in index.bundle.js which will be loaded by index.html

App.js -> will be loaded from index.js/index.bundle.js

App.csss -> style sheet etc

## build the React Webapp

```
# webpack
```

## Deploy the app on the local chain

```
dfx start --clean --background
dfx canister create --all
dfx build
dfx deploy

...
 Frontend:
    ic_bare_react_app_assets: http://127.0.0.1:8000/?canisterId=ryjl3-tyaaa-aaaaa-aaaba-cai
...

```
