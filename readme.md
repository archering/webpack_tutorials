# webpack4/5 总结

1 准备环境

    nodejs 10+ 

2 安装

> 使用webpack 4 或者之后的版本需要装两个软件 webpack 和 webpack-cli

全局安装

    npm install -g webpack

    npm install -g webpack-cli

本地安装

    npm install --save-dev webpack

    npm install --save-dev webpack-cli


本地安装的webpack 需要配置package.json 的script脚本以方便使用

    "scripts": {
        "build":"node_modules/.bin/webpack --config webpack.development.js"
    },

使用

    npm run build

3 配置文件

从4版本开始，webpack增加了一个mode配置，需要指明是development 还是 production

#### production 模式下 webpack 会对代码进行优化，如减小代码体积，删除只在开发环境用到的代码。

> 其实是因为 production 的默认设置 会对文件进行压缩合并

配置文件的基本格式如下：

    module.exports = {
    mode: "production", // "production" | "development" | "none"
    entry: "./app/entry", // string | object | array 应用的入口，如果是多入口应用，写数组
    output: {},
    module: {
        rules: [] 
    },
    plugins: [] //webpack只能处理js文件里面的东西，当你需要处理别的文件时需要借助plugin
    }

多应用入口（非单页面应用）； 参考例子2.start_multi

    module.exports = {
        mode:"development",
        entry:{
            "home":"./src/home.js",
            "index":"./src/index.js"
        },
        output:{
            path:path.resolve(path.join(__dirname,"./dist"))
        }
    }

4 解释说明

module 里面设置的都是loader，loader的作用是：

webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph.

loader的标准设置形式就两个属性： test ，use


    module.exports = {
        output: {
            filename: 'my-first-webpack.bundle.js'
        },
        module: {
            rules: [
            { test: /\.txt$/, use: 'raw-loader' }
            ]
        }
    };

注意：loader只能处理js文件中引入的第三方包，包括css文件，图片文件等...


plugin

    plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

        plugins: [
            new HtmlWebpackPlugin({template: './src/index.html'})
        ]

