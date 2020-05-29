# -init-react-webpack-babel


npm init 
npm install react -S
npm install react-dom -S


npm install webpack -D
npm install webpack-cli -D

npm i babel-loader  -S-D
npm i @babel/core -S-D
npm i @babel/preset-env -S-D
npm i @babel/preset-react -S-D
npm i @babel/plugin-transform-runtime -S-D
npm i @babel/plugin-proposal-decorators -S-D
npm i @babel/plugin-proposal-class-properties -S-D

npm i html-webpack-plugin -S-D
npm i webpack-dev-server -S-D

-----------------------------------------------------------------------------------------

webpack.config.js

const path = require('path')
const HtmlWebPackPlugin = require('html-webpack-plugin')

module.exports = {
	entry: './src/index.js',
    resolve: {
        extensions: ['.wasm', '.mjs', '.js', '.json', '.jsx']
    },
    module: {
        rules: [
            {
                test: /\.jsx?$/, // jsx/js文件的正则
                exclude: /node_modules/, // 排除 node_modules 文件夹
                use: {
                    // loader 是 babel
                    loader: 'babel-loader',
                    options: {
                        // babel 转义的配置选项
                        babelrc: false,
                        presets: [
                            // 添加 preset-react
                            require.resolve('@babel/preset-react'),
                            [require.resolve('@babel/preset-env'), {modules: false}]
                        ],
                        cacheDirectory: true
                    }
                }
            }
        ]
    },
    devServer: {
	    port: 8080,
	    historyApiFallback: true
	  },
    plugins: [
        new HtmlWebPackPlugin({
            template: './src/index.html',
            filename: 'index.html',
            inject: true
        })
    ]
};

-----------------------------------------------------------------------

package.json

{
  "name": "gis-mvp2",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack --mode production",
    "start": "webpack-dev-server --mode development --open"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.10.1",
    "@babel/preset-env": "^7.10.1",
    "babel-loader": "^8.0.6",
    "html-webpack-plugin": "^4.3.0",
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  },
  "dependencies": {
    "@babel/plugin-proposal-class-properties": "^7.10.1",
    "@babel/plugin-proposal-decorators": "^7.10.1",
    "@babel/plugin-transform-runtime": "^7.10.1",
    "@babel/preset-react": "^7.10.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-router-dom": "^5.2.0",
    "webpack-dev-server": "^3.11.0"
  }
}


