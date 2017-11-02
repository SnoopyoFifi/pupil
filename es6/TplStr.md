# 模板字符串

	[深入浅出ES6（四）：模板字符串](http://www.infoq.com/cn/articles/es6-in-depth-template-string)
	
  > 模板字符串是增强版的字符串，用反撇号`\``标识，

  ```js
    function authorize(user, action) {
			if(!user.hasPrivilege(action)){
				throw new Error(
					`用户 ${user.name} 未被授权执行 ${action} 操作`	
				);
			}
    }

		$("#warning").html(`
			<h1>小心！>/h1>
			<p>未经授权打冰球可能受罚
			将近${maxPenalty}分钟。</p>
		`);

		var message = TplTag`<p>${user.name} you have a message!</p>`
  ```
	- 注意：
	  - 模板字符串可以当做普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
		- `${user.name}`和`${action}`被称为模板占位符。
		- 模板占位符的代码可以是任意js表达式，所以函数调用、算术运算等都可以。
		- 如果两个值都不是字符串，可以将其转化为字符串。如：对象调用`.toString()`方法。
		- 如果需要在模板字符串中引用反撇号、`$`和`{`，则需要用反斜杠转义。
		- 可以通过一个模板嵌套另一个模板实现循环语法，叫做模板套构。
		- 另一个衍生用法就是标签模板，即反撇号之前附加额外标签即可。