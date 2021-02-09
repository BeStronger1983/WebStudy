學習 Webpack
=
## 參考資料

1. [從零開始使用Webpack 4 — Part 1](https://medium.com/@chuanjen.wang/%E5%BE%9E%E9%9B%B6%E9%96%8B%E5%A7%8B%E4%BD%BF%E7%94%A8webpack-4-part-1-141d7a547c4a)
2. [從零開始使用Webpack 4 — Part 2](https://medium.com/@chuanjen.wang/%E5%BE%9E%E9%9B%B6%E9%96%8B%E5%A7%8B%E4%BD%BF%E7%94%A8webpack-4-part-2-80127720a232)

## 建立 package.json

    npm init
    npm init -y // 或用 -y 略過所有問題

## 安裝 webpack 與 webpack-cli

webpack-cli 是能在 Command Line 控制 Webpack 的 package

-— save-dev 代表在開發環境下加入這個 package

    npm install webpack webpack-cli --save-dev

## 新增簡單的 JavaScript 函式

### src/fullname.js

    const fullname = (lastname, firstname) => lastname + ',' + firstname;

    export default fullname;

### src/index.js

    import fullname from './fullname';

    const person = fullname('Lastname', 'Firstname');
    console.log(person);

## 新增 webpack.config.js

entry：專案從 index.js 開始執行

output：專案打包後的輸出點，包含輸出檔案的檔案名稱與檔案路徑

    const path = require('path');

    module.exports = {
        entry: './src/index.js',
        output: {
            filename: 'bundle.js',
            path: path.resolve(__dirname,'dist')
        }
    }

## 建立 index.html 加入打包過後的 bundle.js

    <head>
    </head>
    <body>
        <script src="dist/bundle.js"></script>
    </body>

## 在 package.json 中設定執行 Webpack 的 script

    "scripts": 
    {
        "start": "webpack --mode=development",
        "build": "webpack --mode=production"
    }

## 執行 npm run start

webpack 會在 dist 資料夾產生 development 版的 bundle.js

## 執行 npm run build

webpack 會在 dist 資料夾產生 production 版的 bundle.js，內容較少

## 執行 open index.html

打開瀏覽器後，打開開發人員工具，在 Console 中會看到 Lastname,Firstname，表示執行成功。

## [Loader](https://webpack.js.org/concepts/loaders/)

Loader 把 ES6 以上語法、TypeScript 轉換成瀏覽器支援的 JavaScript。甚至還可以讓 CSS、圖片像是程式碼一樣被 import 進來。

## 安裝 Babel

    npm install -D babel-loader @babel/core @babel/preset-env

* [babel-core](https://babeljs.io/docs/en/babel-core) 是 Babel 的核心模組。
* [babel-loader](https://github.com/babel/babel-loader) 讓 Babel 跟 Webpack 可以轉譯 JavaScript 檔案。
* [babel-preset-env](https://babeljs.io/docs/en/babel-preset-env) 是一個聰明的 preset，讓我們可以使用最新版本的 JavaScript 而不用擔心目標環境不同。

## 在 webpack.config.js 中設定 babel-loader

    const path = require('path');

    module.exports = {
        entry: './src/index.js',
        output: {
            filename: 'bundle.js',
            path: path.resolve(__dirname, 'dist')
        },
        module: {
            rules: [
                {
                    use: 'babel-loader',
                    test: /\.js$/,
                    exclude: /node_modules/
                },
            ]
        }
    }

## webpack.config.js 的 module 介紹

module 中設定 Webpack 要使用的 Loader 及規則

use 為要使用的 Loader

test 是正規表達式，符合條件的檔案就使用這個 Loader 處理

exclude 則是排除要使用這個 Loader 處理的資料夾

# 設定 .babelrc

可設定於 webpack.config.js，也可以拉出來放在 .babelrc 方便重複使用

    {
        "presets": [
            "env"
        ]
    }
