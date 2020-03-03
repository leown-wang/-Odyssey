## JavaScript 打脸史之 ES6 作用域 （二）

继  JavaScript 打脸史之 ES6 作用域 （一） 后，`ES6` 之前 `JavaScript` 变量的作用域有点蠢萌。

那么回到之前的问题，在 `ES6` 中，我们如何实现暴露一个被隐藏的局部变量，即闭包呢？

```javascript
{
	let a = 1
	b = function(){
		console.log(a)
	}
}
b() //1
```

不需要复杂的匿名立即执行函数，也不需要再暴露一个变量，只需要一个作用域配合`let`就可以实现。

如上述代码所示，`let `所声明的变量，只在`let`命令所在的代码块内有效，且不存在变量提升.

```javascript
{   
  let a = 1
  var b = 2
}

a // ReferenceError: a is not defined.
b // 2
console.log(c) //Uncauwindow.ght ReferenceError
let c = 3

```

`var` 声明变量会存在变量提升的逻辑，可以在所在作用域中提前使用，且值为 `undefined`,但是按照常规的逻辑，变量应该在声明后才可使用，为了改变这个不合理的逻辑，`JavaScript` 用 `let` 狠狠打了自己的脸。

与此同时，`ES6 `规定，如果在一作用域中使用`let`或`const`声明了变量，那么在其声明前使用就会报错，在语法上，称为“暂时性死区”（temporal dead zone）

```javascript
var a = 1
{
  a = 2 // Uncaught ReferenceError
  let a
}
```
