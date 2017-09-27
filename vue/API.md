# API

## 简介

  > vue.js是一套构建用户界面的渐进式框架。

  - 声明式渲染

    > vue.js 的核心是，可以采用简洁的模板语法来声明式的将数据渲染为`DOM`

    - 文本插值
    
    ```html
      <div id="app">
        {{ message }}
      </div>
      
      var app = new Vue({
        el: '#app',
        data: {
          message: 'snoopy o fifi'
        }
      })
      
      <!-- app.message = 'fifi o snoopy' 可以改变其值 -->
    ```

    - `v-bind`
  
    ```html
      <div id='app-2'>
        <span v-bind:title='message'>
          鼠标悬停可看到此处绑定的 title !
        </span>
      </div>

      var app2 = new Vue({
        el: '#app-2',
        data: {
          message: '页面加载于' + new Date().toLocaleString()
        }
      })

      <!-- v-bind属性被称为指令 -->
    ```


fetch('http://some-site.com/cors-enabled/some.json', {mode: 'cors'})  
  .then(function(response) {  
    return response.text();  
  })  
  .then(function(text) {  
    console.log('Request successful', text);  
  })  
  .catch(function(error) {  
    log('Request failed', error)  
  });
