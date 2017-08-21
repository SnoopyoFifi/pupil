# Traceur

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
