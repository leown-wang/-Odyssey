# 深入理解 viewport

`viewport`是`<meta>`标签的一个属性，它提供有关视口初始大小的提示，仅供移动设备使用。也就是说只有清楚`viewport`的使用，才能更好的针对不同分辨率的设备进行移动端开发。

什么是 viewport？

> [ viewport](http://www.iciba.com/viewport)
>
> 英 [ˈvju:pɔ:t]  美 [ˈvjupɔrt] 
>
> n.视口；

相信中英互译已经很好理解了，是的，viewport简单来说就是设备显示网页的区域。

与pc端相比。移动设备的视口往往偏小，且宽小于高。为确保那些不是为移动端设备设计的网站可以正常显示，布局不至于乱掉，移动端尝试用虚拟的视口渲染页面然后缩小以适应设备视口大小。

不得不说，这种虚拟视口是一种让未做移动端优化的网站在移动设备上自动适配的有效方法。

可问题来了，对于那些用媒体查询做了优化的页面，这种机制并非友好，浪费了响应式设计。

viewport meta 标签应运而生。

苹果在 safari IOS 中第一次引入了 viewport meta 标签，可以让开发人员控制视口的大小和比例。

**一个典型的针对移动端优化的页面meta标签实例：**

```
<meta name="viewport" content="width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
```

- init-scale：设置页面的初始缩放程度
- maximum-scale：设置了页面最大缩放程度
- minimum-scale：设置了页面最小缩放程度
- user-scalable：是否允许用户对页面进行缩放操作

故上述实例含义为：浏览器视图为设备宽度，页面初始缩放比例及最大缩放比例最小缩放比例都是1，且不允许用户对页面进行缩放。