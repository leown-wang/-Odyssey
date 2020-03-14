## JavaScript 打脸史之 ES6 作用域 （二）

`javascript` 中有一个特别反智的概念，叫做变量提升，即在声明变量之前可以使用变量且值为 `undefined`，这会导致什么问题呢？

我们试想这样一个场景，使用 `for` 循环来给一组 `<li></li>` 添加 `onclick` 监听事件，实现点击标签打印是第几个 `<li></li>`。

```javascript
//错误代码
for (var i = 0; i < liItems.length; i++){
    liItems[i].onclick = function() {
      console.log(i)
    }
}
```
运行上述代码，我们会发现，无论点击哪个 `<li></li>` 标签打印出来的都是 `liItems,length`,为什么会这样呢？

是的，变量提升，上述代码经过变量提升，会先编译成如下代码；
```javascript
var i
for (i = 0; i < liItems.length; i++){
    liItems[i].onclick = function() {
      console.log(i)
    }
}
```
整个代码结构中只存在一个 `i`,且在 `for` 循环结束之后值为 `liItems,length`，再调用 `click` 事件当然打印的就是 `i` 的值了。

那么如何实现点击`<li></li>` 标签打印出是第几个标签呢？

和实现闭包如出一辙，利用 `var` 声明的变量在函数内的作用域，通过匿名立即执行函数来实现，如下述代码所示；
```javascript
var i
for (i = 0; i < liItems.length; i++){
    (function(i) {
        var j = i
        liItems[j].onclick = function() {
          console.log(j)
        }
    })(i)
}
```
复杂吧？这一切都归功于变量在声明前可以使用这个不合理的逻辑，而为了改变这个不合理的逻辑，`JavaScript` 用 `let` 狠狠打了自己的脸。

如代码所示，`let` 所声明的变量，只在 `let` 命令所在的代码块内有效，且不存在变量提升.

```javascript
{   
  let a = 1
  var b = 2
}

a // ReferenceError: a is not defined.
b // 2
console.log(c) //Uncaught ReferenceError
let c = 3
```
那么用 `let` 如何实现刚刚那个需求呢？

很简单只需要在 `for` 循环中用 `let` 声明变量 `j` 且把 `i` 的值赋值给 `j`，如下述代码；
```javascript
for (var i = 0; i < liItems.length; i++){
    let j = i
    liItems[j].onclick = function() {
      console.log(j)
    }
}
```
这样一来，整个代码结构中存在 `liItems,length` 个 `j`，自然打印出来的是不同的 `j`。

而如果这样实现呢？
```javascript
for (let i = 0; i < liItems.length; i++){
    liItems[i].onclick = function() {
      console.log(i)
    }
}
```
我们会发现也可以实现上述需求，这是因为 `JavaScript` 自动在 `for` 循环的循环体中帮我们声明了一个 `let` 变量 `i`，且其值为循环体外的 `i`,并在循环体的最后把 循环体内的 `i` 的 值赋值给循环体外的 `i`；整个代码结构中存在 `liItems,length + 1` 个 `i`。