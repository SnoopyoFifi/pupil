# 装饰器
- 什么是装饰器
  - 装饰器是一个表达式
  - 该表达式被执行后，会返回一个函数
  - 函数传入的参数为: `targe`、`name`和`descriptor`
  - 执行该函数后，可能返回`descriptor`对象，用于配置`target`对象

- 装饰器的分类
  - 类装饰器(Class decorators)
  - 属性装饰器(Property decorators)
  - 方法装饰器(Method decorators)
  - 参数装饰器(Parameter decorators)

- 类中不同声明上的装饰器将按以下规定的顺序应用：
  - 参数装饰器，然后依次是方法装饰器，访问符装饰器，或属性装饰器应用到每个实例成员。
  - 参数装饰器，然后依次是方法装饰器，访问符装饰器，或属性装饰器应用到每个静态成员。
  - 参数装饰器应用到构造函数。
  - 类装饰器应用到类。

- 类装饰器
  > 首先定义了 `Yaffer` 类装饰器，同时我们使用了 `@Yaffer` 语法，来使用装饰器。
  ```typescript
    function Yaffer(target: Function): void {
      target.prototype.yaff = function():void{
        console.log("旺旺，旺旺，，，");
      }
    }

    @Yaffer

    class Yaffing {
      constructor(){}
    }

    let dogYaffing = new Yaffing();
    dogYaffing.yaff(); // "旺旺，旺旺，，，"
  ```
  