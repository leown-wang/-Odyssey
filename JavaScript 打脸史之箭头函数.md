## JavaScript 打脸史之箭头函数

谈起 `JavaScript` 打脸史，就不得不提提 `ES6` 的箭头函数，谈起函数，就不得不提提 `this`，

自 `ES3`， `JavaScript` 便支持 `this`,那 `this` 到底是什么呢？

我们在控制台试图打出 `this`，

```javascript
this  //Window
this === window //true

let x = function() {
  console.log(this)  
}
x() //Window
let name = "windowName"
let block = {
    name: "block",
    fn : function () {
        console.log(this.name)     
    }
}
block.fn() //block
```
用面向对象的逻辑来理解，`this` 应当是对象本身，与其类似，在这里的 `this` 看起来是函数调用者本身。

`x()` 其实为 `window.x()`, 故其 `this` 应当为 `window`，`block.fn()` 中函数 'fn()' 中的 `this` 应当为 `block` 本身。

再看一个有趣的例子；
```javascript
let name = "windowName"
let block = {
    name: "block",
    fn : function () {
        console.log(this.name)    
    }
}

let b = block.fn
b()  //windowName
```
按照上述逻辑，`this` 为函数调用者本身，在这个例子里，把 `block.fn` 赋值给 `b`,再调用 `b()`，那么 `b()` 的函数调用者是 `window` 啊，故打印出 `windowName`
没问题啊，多好的一个 `this`，代表函数调用者本身。

```javascript
let name = 'windowName'
let block = {
    name: 'block',
    fn : function () {
       setTimeout( function() {
         console.log(this)
         console.log(this.name)
       }, 500) 
    }
}
block.fn()  //Window  //windowName
```

而上述代码中，我们发现定时器中的函数调用者竟然是 `window`,而非 `block`，那我们要想在定时器的函数中打印出 `block` 只能曲线救国——转移 `this`。
```javascript
let name = 'windowName'
let block = {
    name: 'block',
    fn : function () {
       let that = this
       setTimeout( function() {
         console.log(that.name)
       }, 500) 
    }
}
block.fn()  //block
```
虽然麻烦点，不过还好，算是严谨的 `this`,可坏就坏在，其实 `this` 本身可以被人为改变。
```javascript
let name = 'windowName'
let block = {
    name: 'block',
    fn : function () {
       setTimeout( function() {
         console.log(this.name)
       }.call(block), 500) 
    }
}
block.fn()  //block
```
什么，那个让我们觉得神圣不可侵犯而又严谨的 `this` 变了？!

是的，变了，它变了，而这会有什么影响呢？

让我们试想一下，当我们调用一个 `API` 的函数时，我们不确定其 `this` 是否为函数调用者本身，这是一件多么糟糕的事情。

那么到底 `this` 是什么呢？

一句话来概括：`this` 是 `call` 的第一个参数。如下；
```javascript
let name = 'windowName'
let block = {
    name: 'block',
    fn : function () {
         console.log(this.name)
    }
}
block.fn() //block
block.fn.call(window)  //windowName
```
继而，`this` 也是 `bind`、`apply` 的第一个参数。

至此我们搞懂什么是 `this` 了；

而至于为什么说箭头函数是 `JavaScript` 的打脸史之一，原因有二：
其一为当意图传递的 `this` 为外部的 `this` 但却非函数调用者时，我们需要花费的成本太高，例如使用 `that` 传递，例如使用 `bind`修改；
其二为当函数不需要 `this` 的时候，具名函数或匿名函数的声明太繁琐。

```javascript
let name = 'windowName'
let block = {
    name: 'block',
    fn : function () {
       setTimeout( () => {
         console.log(this.name)
       }, 500) 
    }
}
block.fn()  //block
```
是的，不需要 `bind` 也不需要 使用 `that`，只需要简化声明函数的方式，就可以实现在定时器中使用外部 `this`。

箭头函数还有简化函数声明的优点，例如我们实现数组的次方的次方计算。
```javascript
[1,2,3,4].map(array => array * array).map(array => array * array) //[1, 16, 81, 256]
```
而改用声明匿名函数的方法呢？
```javascript
[1,2,3,4].map(function(array) {
  return array * array
}).map(function(array) {
  return array * array
})  //[1, 16, 81, 256]
```

完。