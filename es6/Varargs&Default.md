# 不定参数&默认参数

- 三个点(...)在`es6`中，有两个含义:
  - 在形参中，表示传递的参数集合，类似于`anguments`，叫不定参数；
  - 在数组中，可以把数组的值全部展开，叫展开运算符。

## 不定参数
  
  - 下面分别使用`arguments`和不定参数分别实现检查一个字符串中是否包含若干个子串。

    - `arguments`实现
      ```js
        function containsAll(paras) { 
          for(var i = 1; i < arguments.length; i++) { // 注意从1开始，arguments[0]被paras占用
            var para = arguments[i];
            if(paras.indexOf(para) === -1) {  
              return false;
            }
          }
          return true;
        }
      ```
    
    - 不定参数实现
      ```js
        function containsAll(paras, ...needles) {
          for(var needle of needles) {          // 此处用到了for of
            if(paras indexOf(needle) === -1) {
              return false;
            }
          }
          return true;
        }
      ```
      
    - 注意：
    - 有且只有最后一个参数才可以被标记为不定参数。
    - 函数被调用时，不定参数前的所有参数都正常填充，任何'额外的'参数都被放进一个数组中并赋值给不定参数。
    - 如果没有额外的参数，不定参数就是一个空数组，而不会是`undefined`。


## 展开运算符的使用
  - 函数调用中使用展开运算符
    - 使用`apply`方法将一个数组展开成多个参数：
      ```js
        function snoopy(a, b, c) {}
        var args = [0, 1, 2];
        snoopy.apply(null, args); 
      ```
    
    - 展开运算符实现：
      ```js
        function snoopy(a, b, c) {}
        var args = [0, 1, 2];
        snoopy(...args);          
    ```
  - 数组字面量中使用展开运算符
    - 合并数组
       ```js
        var arr1 = ['a', 'b', 'c'];
        var arr2 = [...arr1, 'd', 'e'];

        var arr3 =  ['d', 'e'];
        arr1.push(...arr3);
       ```
    
  - 解构赋值
    - 展开运算符在解构赋值中是将多个数组项组合成一个新数组
      ```js
        let [arg1, arg2, ...arg3] = [1, 2, 3, 4];
        arg3 // ['3', '4']
      ```

  - 类数组对象变成数组
    - 展开运算符将伪数组变成数组
      ```js
        var list = document.querySelectorAll('div');
        var arr = [...list];
      ```
  
## 默认参数
  - 用于指定任意参数的默认值
    ```js
      function test(name1 = 'snoopy', name2 = 'fifi') {
        return `${name1} love ${name2} !`;
      }

      function test2(name1 = 'snoopy', 
        name2 = (name1=='jack' ? 'rose' : 'fifi')) {
        return `${name1} love ${name2} !`;
      }
    ```
  - 注意：
    - 传递`undefined`等效于不传值，没有默认值的参数隐式默认为`undefined`。
    - 默认值表达式在函数调用时自左向右求值，默认表达式可以使用该参数之前已经填充好的其他参数值。
    