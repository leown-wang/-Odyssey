## JavaScript 打脸史之 ES6 作用域 （一）

在先前的 ES 标准中，如果未声明过 `a` ，在任何位置声明  `a = 1`  即声明了一个 `window` 下的全局变量  `a`;

```javascript
{
    a = 1
}
for(b=1;b<2;b++){
	c = 3
}
function x(){
	d = 4
}
x()
console.log(window.a)	//1
console.log(window.b)	//2
console.log(window.c)	//3
console.log(window.d)	//4
```

而在函数内声明 `var a = 1`,`a` 的作用域在当前函数中，否则 `a` 的作用域即 `window` ，并且两者都会变量提升;

```javascript
console.log(a)	//undefined
console.log(b)	//undefined
console.log(c)	//undefined
{
	var a = 1
}
for(var b=1;b<2;b++){
	var c = 3
}
function x(){
	var d = 4
}
x()
console.log(window.a)	//1
console.log(window.b)	//2
console.log(window.c)	//3
console.log(window.d)	//d is not defined
```

根据 `var` 的函数作用域的特性，我们很容易实现一个隐藏的局部变量；而当我们需要使用闭包，即实现暴露一个被隐藏的局部变量的时候，我们可以这样来写;

```javascript
function x(){
	var a = 1
	b = function(){
		console.log(a)
	}
}
x()
b()	//1
```

我们为了使用 `b` 暴露一个隐藏的局部变量 a，又额外暴露了全局变量 `x` 。

继续改进,我们可以声明一个匿名立即执行函数;

```javascript
(function(){
    var a = 1
    b = function(){
        console.log(a)
    }
}())
b() //1

```

为了实现闭包，我们竟需如此大费周折。

故，`ES6` 中的 `let` 应运而生。