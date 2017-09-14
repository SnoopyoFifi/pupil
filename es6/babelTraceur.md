# Babel&Traceur

## babel

- 安装

> 全局安装


```
$ npm i -g babel
```

> 本地安装

```
$ npm i --save-dev babel-cli babel-preset-env
```



1. 安装好nodejs和npm。

2. 安装Babel:

**注意**:考虑在单独项目里进行安装，没有全局安装，因为在项目里安装了，打包给别人，别人只要有node环境就可以直接运行，不需要再安装Babel,当然要视情况而定。

- 在命令行工具进入项目根目录
- 执行命令 `npm init -f ` ，然后会在项目根目录里生成一个基础的package.json文件
- 执行命令 `npm install --save-dev babel-cli babel-preset-env `即可安装babel
- npm list可以查看安装的依赖：babel-preset-env 这个插件包含了babel-preset-es2015、babel-preset-es2016、<em>babel-preset-stag</em>等，不包括babel-polyfill、babel-react

3. 配置Babel

在package.json里面添加两项：

```json
  "scripts": {
      "build": "babel js/main.js --out-file js/es5.js"
  },
  "babel": {
      "presets": ["env"]
  }
```

> `"build": "babel js/main.js --out-file js/es5.js" `这段意思是用babel编译js/main.js这个文件 并将编译后的文件输出到js/es5.js这个文件，在项目中就可以引入es5.js这个文件。


## Traceur

- 直接在页面中使用

  ```
  <!-- 加载Traceur编译器 -->
  <script src="http://google.github.io/traceur-compiler/bin/traceur.js" type="text/javascript"></script>

  <!-- 打开实验选项，否则有些特性可能编译不成功 -->
  <script>
    traceur.options.experimental = true;
  </script>
  ```

  > 编译es6代码:

  ```
  <script type="module">
    // es6代码
  </script>
  ```

  **注意**：`script` 标签 `type` 属性必须为 `module` 用于 Traceur 编译器识别es6代码的标识。

  ​

- Traceur 的在线编辑器

  [点击进入在线编辑]([http://google.github.io/traceur-compiler/demo/repl.html](http://google.github.io/traceur-compiler/demo/repl.html))

- 使用 `node.js` 工具


> 安装

````
$ npm i -g traceur
````

> 运行es6代码

```
$ traceur calc.js
```

> 将es6输出为es5脚本

```
$ traceur --script calc.es6.js --out calc.es5.js --experimental
```

**注意**：为了防止有些特性编译不成功，最好加上 `--experimental` 选项
