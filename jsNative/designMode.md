# 设计模式

## 单例模式
单例模式的定义是：保证一个类仅有一个实例，并提供一个访问它的全局访问点。
- 实现单例模式

  ```js
    var Singleton = function(name) {
      this.name = name;
      this.instance = null;
    };

    Singleton.prototype.getName = function() {
      alert(this.name);
    };

    Singleton.getInstance = function(name) {
      if(!this.instance) {
        this.instance = new Singleton(name);
      }
      return this.instance;
    };

    var a = Singleton.getInstance('snoopy');
    var b = Singleton.getInstance('fifi');

    alert(a===b);


    // or

    var Singleton = function(name) {
      this.name = name;
    };

    Single.prototype.getName = function() {
      alert(this.name);
    };

    Singleton.getInstance = (function(){
      var instance = null;
      return function(name) {
        if(!instance) {
          instance = new Singleton(name);
        }
        return instance;
      }  
    })();

    var a = Singleton.getInstance('snoopy');
    var b = Singleton.getInstance('fifi');

    alert(a===b);
  ```

- 透明的单例模式

  ```js
    var CreateDiv = (function(){
      var instance;
      var CreateDiv = function(html) {
        if(instance) {
          return instance;
        }
        this.html = html;
        this.init();
        return instance = this;
      };
      CreateDiv.prototype.init = function() {
        var div = document.createElement('div');
        div.innerHtml = this.html;
        document.body.appendChild(div);
      }

      return CreateDiv;
    })();

    var a = new CreateDiv('snoopy');
    var b = new CreateDiv('fifi');
    alert(a === b);
  ```

- 用代理实现单例模式

  ```js
    var CreateDiv = function(html) {
      this.html = html;
      this.init();
    }
    CreateDiv.prototype.init = function() {
      var div = document.createElement('div');
      div.innerHtml = this.html;
      document.body.appendChild(div);
    }
    var ProxySingletonCreateDiv = (function(){
      var instance;
      return function(html) {
        if(!instance) {
          instance = new CreateDiv(html);
        }
        return instance;
      }  
    })();

    var a = new ProxySingletonCreateDiv('snoopy');
    var b = new ProxySingletonCreateDiv('fifi');
  ```

- `Javascript`中的单例模式
  > 降低全局变量污染
  ```js
    // 使用命名空间

    var namespace1 = {
      a: function() {
        alert(1);
      },
      b: function() {
        alert(2);
      }
    }
    // 动态创建命名空间
    var MyApp = {};
    MyApp.namespace = function(name) {
      var parts = name.split('.'); // dom.style -> ['dom', 'style']
      var current = MyApp; 
      for (var i in parts) {
        if (!current[parts[i]]) {
          current[parts[i]] = {};
        }
        current = current[parts[i]];
      }
    } 

    MyApp.namespace('snoopy');
    MyApp.namespace('dom.style');
    console.dir(MyApp);



    // 使用闭包封装私有变量
    var user = (function(){
      var __name = 'snoopy', // 私有变量
          __age = 28;
      return {
        getUserInfo: function(){
          return {
            name: __name,
            age: __age
          }
        }
      }
    })();
  ```
    
- 惰性单例
```js
  var createLoginLayer = (function(){
    var div;
    return function() {
      if(!div) {
        div = document.createElement('div');
        div.innerHTML = '我是登录弹窗';
        div.style.display = 'none';
        document.body.appendChild(div);
      }
    }  
  })()

  document.getElementById('loginBtn').onclick = function() {
    var loginLayer = createLoginLayer();
    loginLayer.style.display = 'blobk';
  }
```