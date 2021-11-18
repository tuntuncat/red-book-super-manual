---
description: 'KEYWORDS: JS的诞生，TC39，ES，DOM，BOM'
cover: .gitbook/assets/javascript-736400-1.png
coverY: 0
---

# 第1章 什么是JS

虽然第1章的名字叫做“什么是JS”，但是红宝书里却没有从正面给出JS的定义。有一种挂羊头卖狗肉的感觉。

有人会问这个问题有什么意义？但是这个问题是很重要的，好多人学了一些东西。到最后都不知道自己学的啥，问题就出在这里。

除了一句“JS是一种高级编程语言”以外，你还能给JS贴上什么标签？脚本？前端? 动态类型？每个人的角度都不太一样，我们摘取Wiki上的解释作为JS的定义吧：

> **JavaScript**（通常缩写为**JS**）是一种[高级](https://zh.wikipedia.org/wiki/%E9%AB%98%E7%BA%A7%E8%AF%AD%E8%A8%80)的、[解释型](https://zh.wikipedia.org/wiki/%E7%9B%B4%E8%AD%AF%E8%AA%9E%E8%A8%80)的[编程语言](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)[\[8\]](https://zh.wikipedia.org/wiki/JavaScript#cite\_note-:0-8)。JavaScript是一门[基于原型](https://zh.wikipedia.org/wiki/%E5%9F%BA%E4%BA%8E%E5%8E%9F%E5%9E%8B%E7%BC%96%E7%A8%8B)、[头等函数](https://zh.wikipedia.org/wiki/%E5%A4%B4%E7%AD%89%E5%87%BD%E6%95%B0)的语言[\[9\]](https://zh.wikipedia.org/wiki/JavaScript#cite\_note-:1-9)，是一门多范式的语言，它支持[面向对象](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)程序设计，[指令式编程](https://zh.wikipedia.org/wiki/%E6%8C%87%E4%BB%A4%E5%BC%8F%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)，以及[函数式编程](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)。它提供语法来操控文本、[数组](https://zh.wikipedia.org/wiki/%E6%95%B0%E7%BB%84)、日期以及[正则表达式](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)等，不支持[I/O](https://zh.wikipedia.org/wiki/I/O)，比如网络、存储和图形等，但这些都可以由它的宿主环境提供支持。它已经由ECMA（欧洲电脑制造商协会）通过[ECMAScript](https://zh.wikipedia.org/wiki/ECMAScript)实现语言的标准化[\[8\]](https://zh.wikipedia.org/wiki/JavaScript#cite\_note-:0-8)。它被世界上的绝大多数网站所使用，也被世界主流[浏览器](https://zh.wikipedia.org/wiki/%E6%B5%8F%E8%A7%88%E5%99%A8)（[Chrome](https://zh.wikipedia.org/wiki/Google\_Chrome)、[IE](https://zh.wikipedia.org/wiki/Internet\_Explorer)、[Firefox](https://zh.wikipedia.org/wiki/Firefox)、[Safari](https://zh.wikipedia.org/wiki/Safari)、[Opera](https://zh.wikipedia.org/wiki/Opera%E9%9B%BB%E8%85%A6%E7%80%8F%E8%A6%BD%E5%99%A8)）支持。

里面提到了解释型，基于**原型(prototype)，头等函数(first-class function)，支持面向对象，函数式，指令式编程**。由ECMA制定了标准，被主流浏览器支持。

这些点才是我们在正式学习JS之前所需要知道的精髓：**JS的面向对象特性实现于原型链，JS受益于头等函数特性，对函数式编程的支持极好(回调函数，闭包，高阶函数如Array.prototype.map()都是函数式编程的应用)**。而且是一门主要运行在浏览器的语言。

我们下次再介绍JS的时候，除了告诉别人JS是一门脚本语言以外，再说一说它自己的特点呢\~

## 1.1 JS的诞生(1)

​ 一句话概括——95年，JS之父为了避免龟速的服务器验证流程，干脆让浏览器直接处理验证算了，于是JS诞生了。

## 1.2 JS和JAVA的关系(1)

​ JS的作者为了让JS（刚开始叫liveScript）蹭java热度，搞了个相似的名字。约等于“卡巴斯基”和“巴基斯坦”的关系。

## 1.3 ES和JS什么关系(3)

​ Netscape和Microsoft公司分别实现了两种不同的js，为了最后统一成一个标准，成立了一个技术委员会专门做这事儿——**TC39**。这群人集思广益花了几个月搞出了ECMA-262，作为JS的规范，后面统称其为ECMAScript。

​ 所以得出结论，ES是JS的规范。

​ 再推一步：ES只负责告诉大家js应该怎么样，但是具体怎么实现就看各家浏览器八仙过海了。其实现在ES标准早已经不再只是浏览器需要关注的了，实际上Node.js的出现让JS不再依赖浏览器就可以运行。

​ [这是ecma262的github仓库，里面有最新的ES提案，每个前端都必须star以示尊重](https://github.com/tc39/ecma262)

​ 而且当代JS也包含了DOM,BOM等对象的实现。

​ 书中也简述了对DOM,BOM功能的基本描述：

> DOM:提供与网页内容交互的API的对象
>
> BOM:提供与浏览器交互的API的对象

## _本章需要你掌握的问题_

1. _一句话阐释 JS和 ES的关系_
2. _DOM,BOM和ES，JS分别是什么关系？_
3. _JS是浏览器的专属语言吗？_

***
