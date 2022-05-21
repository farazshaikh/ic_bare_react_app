# Convert dfx web asset canister to a React App

This sample project converts the dfx-created web app into a react app.
The contents of this repository are the results of steps described in this README.md

You can clone this repository and use it as an initial template to host a React
Web App on the IC.  Or you can initialize are new dfx project and follow the
steps described here.


# Steps:

## Create a dfx project

Install dfx

```
https://smartcontracts.org/docs/current/developer-docs/build/install-upgrade-remove/
 sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
```

Create dfx project

```
dfx create ic_bare_react_app
```

## Install React dependency.

```
cd ic_bare_react_app
npm i react react-dom
```


## Install Dev dependencies (Webpack, css, sass, babel presets and Webpack loaders)

Install loader for babel
```
cd ic_bare_react_app
npm i -D babel-loader file-loader css-loader sass-loader sass
```


Install Webpack
```
cd ic_bare_react_app
npm i -D Webpack Webpack-cli Webpack-dev-server
```

Install transpilers
```
ic_bare_react_app
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

Modify the existing webpack.config.js to use the babel-loader for .js and .jsx files. Add similar section to specify the css loaders

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

Create a minimal React app by placing the following files.

```
ls ./src/ic_bare_react_app_assets/src/
App.js      App.scss    index.html  index.js
```

- index.html -> entry point for the react web app

- index.js -> will be transformed into index.bundle.js which will be loaded by index.html

- App.js -> will be loaded from index.js/index.bundle.js

- App.csss -> style sheet etc

## build the React Web app

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
