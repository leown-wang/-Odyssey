# 深入理解 HTML 语义化

什么是语义化？科学上网第一步，我们先问问维基百科。

> **语义化 **是前端开发里面的一个专用术语，其优点在於标签语义化有助于构架良好的 html 结构，有利于搜索引擎的建立索引、抓取；另外，亦有利于页面在不同的设备上显示尽可能相同；此外，亦有利于构建清晰的结构，有利于团队的开发、维护。

维基百科其实已经说的很明确了。

`HTML` 作为构建网页的基石，作为开发者与浏览器的中间件，是有必要让两者都可以读懂 `HTML` 本身的。

###	让开发者读懂 HTML 内容

这要从前端开发的历史说起。

早期的网页开发是后端主导的，只会用简单的标签，甚至全盘用`table`进行布局；后来大家审美上有要求了，一批美工程序员上线了，用无数个`<div></div>` 构建整个页面，属实让人头大；再后来，也就是当下，为了构建清晰的`HTML` 结构、有利于团队的开发和维护，前端程序员需要用合适的标签表达对应的内容，`HTML` 语义化应运而生。

`HTML` 规范也以制赞往语义化的方向上不断努力，`HTML5` 更是在之前规范的基础上，对一些标签进一步做了修改、删除和增加。

[这里列出了所有标准的`HTML5`元素。](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)

`语义化HTML `原则是现代专业前端开发的基础之一，尽可能用语义化的标签来表示页面内容是前端行业的基本素养。

```html
 <body>
     
  <header>
    <nav>
      <ul>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </nav>
  </header>
     
  <main>
    <section>
      <h3></h3>
      <article></article>
    </section>
  </main>
     
  <aside></aside>
     
  <footer></footer>
     
</body>
```

* HTML5 中的区块和段落元素
  HTML5 中新的区块和段落元素一览: `<section>`, `<article>`, `<nav>`, `<header>`, `<footer>`, `<aside>` 和 `<hgroup>`.

*  使用 HTML5 的音频和视频

  `<audio>` 和 `<video>` 元素嵌入和允许操作新的多媒体内容。

* 表单的改进
  看一下 HTML5 中对 web 表单的改进：强制校验API，一些新的属性，一些新的`<input>` 元素type 属性值 ，新的 `<output>` 元素。

* 新的语义元素
  除了节段，媒体和表单元素之外，还有众多的新元素，例如 `<mark>`， `<figure>`， `<figcaption>`， `<data>`， `<time>`， `<output>`， `<progress>`， 或者 `<meter>`和`<main>`，这增加了有效的 HTML5 元素的数量。

* `<iframe>` 的改进
  使用 sandbox， seamless， 和 srcdoc 属性，作者们现在可以精确控制 `<iframe>` 元素的安全级别以及期望的渲染。

  

### 让浏览器读懂 HTML 内容

`HTML`语义化便于浏览器、搜索引擎解析。 利于爬虫标记、利于SEO。

