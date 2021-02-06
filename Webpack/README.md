Webpack
=
<h1><a href="https://medium.com/@chuanjen.wang/%E5%BE%9E%E9%9B%B6%E9%96%8B%E5%A7%8B%E4%BD%BF%E7%94%A8webpack-4-part-1-141d7a547c4a">從零開始使用Webpack 4 — Part 1</a></h1>

<h2>建立 package.json</h2>

    npm init
    npm init -y // 或用 -y 略過所有問題

<h2>安裝 webpack 與 webpack-cli</h2>

webpack-cli 是能在 Command Line 控制 Webpack 的 package

-— save-dev 代表在開發環境下加入這個 package

    npm install webpack webpack-cli --save-dev