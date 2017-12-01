# 数据类型扩展

## 数组的扩展

  - 扩展运算符`...`

  > 将一个数组变为一个参数序列，主要用于函数调用
  
  ```js
    function push(array, ...items) {
      array.push(...items)
    }

    function f(v, w, x, y, z) { }  
    var args = [0, 1];  
    f(-1, ...args, 2, ...[3]);  
  ```

  - 替代数组的`apply` 方法
    
    > 由于扩展运算符可以展开数组，所以不再需要`apply`方法，将数组转为函数的参数了。
  ```js
    // es5
    Math.max.apply(null, [14, 3, 77]);
    // es6
    Math.max(...[14, 3, 77]);
    // 等价于
    Math.max(14, 3, 77);
  ```
