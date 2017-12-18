# API

## 简介

  - 官方定义
    - `Module Bundler` （模块加载器）， 目的是把有依赖关系的各种文件，打包成一系列静态资源。

  - `webpack`解决的问题
    - 用来解决模块之间的依赖，从而解决引入模块顺序问题；
    - 解决模块内的同名变量被覆盖的问题。

  - `webpack`支持的模块方式
    - 默认支持 commonjs/AMD/UMD/ES6模块；
    - 不支持`ES6`关键字和函数（用`loader`来处理）。
  
  ![what-is-webpack](../images/what-is-webpack.png)

## 安装

  - 全局安装

  ```js
  $ npm i webpack -g
  ```

  - 本地安装## 

  ```js
  // 进入项目目录
  // 确定已经有 package.json，没有通过 npm init 创建
  // 安装 webpack 依赖
  $ npm i webpack --save-dev

  // 查看 webpack 版本信息
  $ npm info webpack

  // 安装指定版本的 webpack
  $ npm i webpack@1.12.x --save-dev
  ```

  - 安装 webpack 开发工具

  ```js
  $ npm i webpack-dev-server --save-dev
  ```

## 核心概念
  - 入口(Entry) 
    + 单个入口
      ```js
        const config = {
          // entry: './path/to/my/entry/file.js'
          entry: {
            main: './path/to/my/entry/file.js'
          }
        }
        module.exports = config;
      ```

    + 对象语法
      ```js
        const config = {
          entry: {
            app: './src/app.js',
            vendors: './src/vendors.js'
          }
        }       
      ```

    + 常见场景

      - 分离 应用程序和第三方入口

        ```js
        const config = {
          entry: {
            app: './src/app.js',
            vendors: './src/vendors.js'
          }
        }
        ```

        - 多页面应用程序

          ```js
          const config = {
            entry: {
              pageOne: './src/pageOne/index.js',
              pageTwo: './src/pageTwo/index.js',
              pageThree: './src/pageThree/index.js'
            }
          }
          ```

          ​

  - 输出(Output)

    > 配置`output`选项可以控制`webpack`如何向硬盘写入编译文件。即使存在多个入口起点，也只可指定一个输出配置。

      - 基本用法

        ```js
        const config = {
          output: {
            filename: 'bundle.js',  // 输出文件的文件名
            path: '/home/proj/public/assets'  // 目标输出目录的绝对路径
          }
        }
        module.exports = config;
        ```

      - 多个入口起点

        ```js
        {
          entry: {
            app: './src/app.js',
            search: './src/search.js'
          },
          output: {
            filename: '[name].js',
            path: __dirname + '/dist'  // 写入到硬盘：./dist/app.js, ./dist/search.js
          }
        }
        ```

        ​

      - 高级进阶

        ```js
        output: {
          path: '/home/proj/cnd/assets/[hash]',
          publicPath: 'http://cdn.example.com/assets/[hash]/'
        }
        ```

        > 在编译时不清楚publicPath，可在入口起点设置`__webpack_public_path__ = myRuntimePublicPath`

  - `Loader`

    > `loader`用于对模块的源代码进行转换，在`import`或加载模块时预处理文件。如: 转换`typescript` 为 `javascript`、转内联图像为`data URL`、在`javascript`模块中`import` css文件。

    - 在使用`loader`之前，必须安装相应的`loader`模块包

      ```
      npm i --save-dev css-loader
      npm i --save-dev ts-loader
      ```

      - 安装完成后，再配置相应的规则，指定文件使用对应的规则。

        ```
        module.exports = {
          module: {
            rules: [
              { test: /\.css$/, use: 'css-loader' },
              { test: /\.ts$/, use: 'ts-loader' }
            ]
          }
        }
        ```

        ​

      - 可在配置中指定多个`loader`

        ```js
        module: {
          rules: [
            {
              test: /\.css$/,
              use: [
                { loader: 'style-loader' },
                {
                  loader: 'css-loader',
                  options: {
                    modules: true
                  }
                }
              ]
            }
          ]
        }
        ```

        ​

      - 也可使用`内联`或者`CLI`的方式使用`loader`

        ```
        import Styles from 'style-loader!css-loader?modules!./styles.css';
        // 可以在 `import` 语句或任何等效于 "import" 的方式中指定 loader。使用 `!` 将资源中的 loader 分开。分开的每个部分都相对于当前目录解析。

        webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
        // 这会对 .jade 文件使用 jade-loader，对 .css 文件使用 style-loader 和 css-loader。
        ```

        ​

  - 插件(Plugins)

    > 插件的目的在与解决`loader`无法实现的其他事。
    >
    > 插件可以携带参数、选项，必须在`webpack`配置中，向`plugins`属性传入`new` 实例

    ```js
    const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过npm安装
    const webpack = require('webpack'); // 访问内置的插件
    const path = require('path');

    const config = {
      entry: './path/to/my/entry/file.js',
      output: {
        filename: 'my-first-webpack.bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      module: {
        loaders: [
          {
            test: /\.(js|jsx)$/,
            use: 'babel-loader'
          }
        ]
      },
      plugins: [
        new webpack.optimize.UglifyJsPlugin(),
        new HtmlWebpackPlugin({template: './src/index.html'})
      ]
    };
    module.exports = config;
    ```

    ​

## 相关配置
  - `package.json`

    ```json

      {
        "name": "webpack-demo",
        "version": "1.0.0",
        "description": "",
        "main": "webpack.config.js",
        "dependencies": {},
        "devDependencies": {
          "babel": "^6.3.13",
          "babel-core": "^6.3.21",
          "babel-loader": "^6.2.0",
          "babel-plugin-transform-runtime": "^6.3.13",
          "babel-preset-es2015": "^6.3.13",
          "babel-runtime": "^5.8.34",
          "clean-webpack-plugin": "^0.1.10",
          "copy-webpack-plugin": "^3.0.1",
          "css-loader": "^0.23.1",
          "extract-text-webpack-plugin": "^1.0.1",
          "file-loader": "^0.8.5",
          "glob": "^7.0.5",
          "html-loader": "^0.4.3",
          "html-webpack-plugin": "^2.9.0",
          "imports-loader": "^0.6.5",
          "jquery": "^1.12.4",
          "less": "^2.7.1",
          "less-loader": "^2.2.3",
          "style-loader": "^0.13.0",
          "url-loader": "^0.5.7",
          "webpack": "^1.12.13",
          "webpack-dev-server": "^1.14.1"
        },
        "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "dev": "webpack-dev-server --progress --colors --inline",
          "build": "webpack -p"
        },
        "author": "duanliang",
        "license": "ISC"
      }
    ```


  - `webpack.config.js`

    ```js
      {
        var path = require('path');
        var glob = require('glob');
        var webpack = require('webpack');
        var ExtractTextPlugin = require('extract-text-webpack-plugin');//将你的行内样式提取到单独的css文件里，
        var HtmlWebpackPlugin = require('html-webpack-plugin'); //html模板生成器
        var CleanPlugin = require('clean-webpack-plugin'); // 文件夹清除工具
        var CopyWebpackPlugin = require('copy-webpack-plugin'); // 文件拷贝
        var config = {
          entry: { //配置入口文件，有几个写几个
            index: './src/js/index.js',
            list: './src/js/list.js',
            about: './src/js/about.js'
          },
          output: { // 出口
            path: path.join(__dirname, 'dist'), //打包后生成的目录
            publicPath: '', //模板、样式、脚本、图片等资源对应的server上的路径
            filename: 'js/[name].[hash:6].js',  //根据对应入口名称，生成对应js名称
            chunkFilename: 'js/[id].chunk.js'   //chunk生成的配置
          },
          resolve: {
            root: [],
                 //设置require或import的时候可以不需要带后缀
                extensions: ['', '.js', '.less', '.css']
            },
          module: { // 模块
            loaders: [ 
              {
                test: /\.css$/,
                loader: ExtractTextPlugin.extract('style', 'css')
              },
              {
                test: /\.less$/,
                loader: ExtractTextPlugin.extract('css!less')
              },
              {
                test: /\.js$/,
                    loader: 'babel',
                    exclude: /node_modules/,
                    query:{
                      presets: ['es2015']
                    }
                },
              {
                test: /\.(woff|woff2|ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/,
                loader: 'file-loader?name=./fonts/[name].[ext]'
              },
              {
                        test: /\.(png|jpg|gif|svg)$/,
                        loader: 'url',
                        query: {
                            limit: 30720, //30kb 图片转base64。设置图片大小，小于此数则转换。
                            name: '../images/[name].[ext]?' //输出目录以及名称
                        }
                    }
            ]
          },
          plugins: [
            new webpack.ProvidePlugin({ //全局配置加载
                   $: "jquery",
                   jQuery: "jquery",
                   "window.jQuery": "jquery"
                }),
                new CleanPlugin(['dist']),// 清空dist文件夹
            new webpack.optimize.CommonsChunkPlugin({
              name: 'common', // 将公共模块提取，生成名为`vendors`的chunk
              minChunks: 3 // 提取至少3个模块共有的部分
            }),
            new ExtractTextPlugin( "css/[name].[hash:6].css"), //提取CSS行内样式，转化为link引入
            new webpack.optimize.UglifyJsPlugin({ // js压缩
                compress: {
                  warnings: false
                }
              }),
              new CopyWebpackPlugin([
                    {from: './src/images', to: './images'} //拷贝图片
                ])
          ],
          externals: {
                $: 'jQuery'
            },
            //devtool: '#source-map',
          //使用webpack-dev-server服务器，提高开发效率
          devServer: {
            // contentBase: './',
            host: 'localhost',
            port: 8188, //端口
            inline: true,
            hot: false,
          }
        };

        module.exports = config;

        var pages = Object.keys(getEntry('./src/*.html'));
        var confTitle = [ 
          {name: 'index', title: '这是首页标题'},
          {name: 'list', title: '这是列表标题'},
          {name: 'about', title: '这是关于我标题'}
        ]
        //生成HTML模板
        pages.forEach(function(pathname) {
          var itemName  = pathname.split('src\\') //根据系统路径来取文件名，window下的做法//,其它系统另测
            var conf = {
                filename: itemName[1] + '.html', //生成的html存放路径，相对于path
                template: pathname + '.html', //html模板路径
                inject: true, //允许插件修改哪些内容，包括head与body
                hash: false, //是否添加hash值
                minify: { //压缩HTML文件
                    removeComments: true,//移除HTML中的注释
                    collapseWhitespace: false //删除空白符与换行符
                }
            };
          conf.chunks = ['common', itemName[1]]
          for (var i in confTitle) { 
            if (confTitle[i].name === itemName[1]) { 
              conf.title = confTitle[i].title
            }
          }
            config.plugins.push(new HtmlWebpackPlugin(conf));
        });


        //按文件名来获取入口文件（即需要生成的模板文件数量）
        function getEntry(globPath) {
            var files = glob.sync(globPath);
            var entries = {},
                entry, dirname, basename, pathname, extname;

            for (var i = 0; i < files.length; i++) {
                entry = files[i];
                dirname = path.dirname(entry);
                extname = path.extname(entry);
                basename = path.basename(entry, extname);
                pathname = path.join(dirname, basename);
                entries[pathname] = './' + entry;
            }
            return entries;
        }
      }
    ```

## 说明
  - webpack 功能

  > 给一个入口，根据入口解读对应的依赖关系，并将文件打包（压缩、合并、混淆等）成一个js文件（包含了其他静态资源）

  - webpack 打包形成的代码

    - webpack基于node，读取文件，并分析依赖关系，最终生成新的目标文件。
    
    - 自执行函数，将各个模块代码作为数组元素的参数传递，并执行；
    

    ```js
      (fn(modules){
        // 先执行模块2
        module[1].call(
          return '给一个对象'
          // 给对象的属性赋值
        )
      })([fn(){模块1}, fn(){模块2}])
    ```

  - webpack 属性

    - entry入口{}：默认main属性

    - output出口{}：path：产出目录（最好使用绝对路径）；filename：产出js文件

    - module模块：loaders[]：一堆loader对象{test:/\.css$/, loader:''}

    - plugins插件[]: new xxx的插件对象

    - ! 表示分隔、 ? 表示参数


