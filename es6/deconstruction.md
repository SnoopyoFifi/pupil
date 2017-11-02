# 变量的解构赋值

  > 解构赋值语法是一个js表达式，可以将值从数组或属性从对象提取到不同的变量中。

## 数组的解构赋值
  - 模式匹配：只要等号两边的模式相同，左边的变量就会被赋予对应的值。
    - 注意： 如果等号右边不是数组，或者说不是可遍历的结构(不具备`Iterator`接口)，那么就会报错。        
    ```js
      // 嵌套解构
      let [foo, [[bar], baz]] = [1, [[2], 3]];
      let [a, b, c] = [1, 2, 3];
      let [ , , third] = ['snoopy', 'fifi', 'rose'];
      let [head, ...tail] = [1, 2, 3, 4];
      let [x, y, ...z] = ['a'];

      // 不完全解构
      let [x, y] = [1, 2, 3]; 
      let [a, [b], c] = [1, [2, 3], 4];

      // 解构失败 undefined
      let [foo] = [];
      let [bar, foo] = [1];

      // 右边不是数组，报错
      let [foo] = 1;
      let [foo] = false;
      let [foo] = NaN;
      let [foo] = undefined;
      let [foo] = null;
      let [foo] = {};

      // Set结构
      let [x, y, z] = new Set(['a', 'b', 'c']);

      // Generator 函数
      function* fibs(){
        let a = 0;
        let b = 0;
        while (true) {
          yield a;
          [a, b] = [b, a + b];
        }
      }
    ```
  - 解构赋值允许指定默认值。
    ```js
      let [foo = true] = [];
      let [x, y = 'b'] = ['a'];
      let [x, y = 'b'] = ['a', undefined];

      // 右边数组成员不严格等于`undefined`
      let [x = 1] = [undefined];
      let [x = 1] = [null];

      //默认值是惰性求值 
      function f() {
        console.log('aaa');
      }
      let [x = f()] = [1];

      // 默认值可以引用解构赋值的其他变量
      let [x = 1, y = x] = [];
      let [x = 1, y = x] = [2];
      let [x = 1, y = x] = [1, 2];
      let [x = y , y = 1] = []; 
    ``` 
    - 注意：
      - `ES6`内部使用严格相等运算符(===)，判断一个位置是否有值。
      - 默认值是一个表达式时，表达式只有在用到的时候才会求值，上述`f()`没有执行。
      - 默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

## 对象的解构赋值
  - 对象解构与数组解构有个重要的不同，对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
    ```js
      let { foo, bar } = { foo: 'snoopy', bar: 'fifi' };
      let { bar, foo } = { foo: 'snoopy', bar: 'fifi' };
      let { baz } = { foo: 'snoopy', bar: 'fifi' };

    
      let { foo: baz } = { foo: 'snoopy', bar: 'fifi' };
      
      let obj = { first: 'hello', last: 'world' };
      let { first: f, last: l } = obj;

      // 嵌套结构
      let obj = {
        p: [
          'Hello',
          { y: 'World' }
        ]
      };
      let { p: [x, { y }] } = obj;

      // 指定默认值
      var {x = 3} = {};
      var {x, y = 5} = {x: 1};
      var {x: y = 3} = {};
      var {x: y = 3} = {x: 5};
      var { message: msg = 'what's wrong with you' } = {};
      var {x = 3} = { x: undefined };
      var {x = 3} = { x: null };

      // 解构失败
      let {foo} = {bar: 'baz'};

      // 内部机制
      let { foo: baz } = { foo: "aaa", bar: "bbb" };

      // 报错
      let {foo: {bar}} = {baz: 'baz'};

      // 已声明的变量
      let x;
      {x} = {x:1}; // 报错
      ({x} = {x:1}); // 正确写法

      // 诡异写法
      ({} = [true, false]);
      ({} = 'abc');
      ({} = []);

      // 赋值现有对象中的方法 
      let { log, sin, cos } = Math;

      // 数组赋值
      let arr = [1, 2, 3];
      let { 0: first, [arr.length -1] : last } = arr;

    ```

    - 注意：
      - 实际上，对象的解构就是下面形式的简写`let { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };`。
      - 对象解构赋值的内部机制是先找到同名属性，然后再赋值给对应的变量。
      - js引擎对赋值
