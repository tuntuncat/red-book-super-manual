---
description: 'keywords: 原始值, 引用值, 深拷贝和浅拷贝'
---

# 第4章 变量、作用域与内存

## **4.1 原始值和引用值**

因为JS属于弱类型语言，所以JS的变量类型是不定的。

这是一把双刃剑，增加了便利性，消减了可维护性。或者换句话说，"前期编程爽，维护XX场"。所以当代大型前端项目都要实现TS(TypeScript)化，因为没有类型约束的项目终究走不长远。

JS里的数据只有两个大类型：**原始值**和**引用值**。

* 原始值：Number,String,Symbol,Undefined,Null,Boolean这6大类型都是原始值。
* 引用值：所有的对象，因为JS不允许直接操作对象所在的内存空间，所以引用值实际上是这些对象在内存的地址而非这些对象本身。

而在JS中，变量之间的数据传递书上说的不按“引用传递”，都是“按值传递”。实际上可能是翻译的问题，这里的“引用”指的就是对象本身，但是我们通常理解的“引用”是指的对象的地址（其实我们把JS里对象的值理解为对象的地址就好了，那么所有传递都是按值传递没有问题）。所以我们把书里的“值”实际上分为两种情况：

* 第一种情况是：如果某变量是原始类型，那么它就直接传递该值给其他变量。传递过后两个变量没有任何关系，可以独立操作。
* 第二种情况是：如果变量是引用类型，那么它就直接传递该对象的地址给其他变量（因为本身该变量的值就是对象的地址，所以这也是该变量的值）。所以单纯的传递地址会让多个变量指向同一个对象。

```javascript
const a = 1 // 值是一个原始类型
const b = a // a将值传递给b，所以b的值是1
const c = {} // 值是一个引用类型
const d = c // c将值传递给d，该值是一个地址，所以d是对象的地址
d.name = 'tuntun'
c.name // 'tuntun' 
```

第一种情况比较好理解，主要是第二种情况有时候不注意的话会出意料之外的情况，特别是在某些函数以引用值为参数时。

```javascript
function setName(obj){
// 这个obj实际上是函数内部作用域的局部变量
  obj.name = "Nicholas";
  // obj被指向了一个新对象 
  obj = new Object(); 
  obj.name = "Greg";
  return obj // 此时返回的是name为Greg的对象的引用，而非你传进来的引用了   
}
// 这是书中的例子，其实我们最关键的就是要理解obj实际上是我们在函数内部声明的一个新变量。
// 该变量指向外部传进的对象的地址，并且该指向在函数内部被修改了。
```

所以我们只需记住一句话：<mark style="color:red;">JS里的对象我们只能通过引用来操作(因为没有引用的对象都被销毁了。。。)</mark>。所以任何关于对象的读写，我们只需<mark style="color:red;">把对象本身和该对象的引用分开理解</mark>，就不会造成意外情况。

以上问题也引申出了一个大问题，**我们怎么复制对象而不是复制对象的引用**？

在任何面向对象的语言中，都会有一个经典问题：**怎么实现深拷贝和浅拷贝**？

* 浅拷贝：被拷贝对象内部含有引用类型，此时就不再拷贝引用类型的内容，而是拷贝引用就OK了
* 深拷贝：将被拷贝对象内部嵌套的引用类型完全拷贝下来。

```javascript
const a = [1,[2,3,[4,5]]
// 我们怎么深拷贝这个数组?
// 方法1
function copy(a){
 const b = []
 for(let i = 0; i < a.length; i++){
    b[i] = a[i]
 }
 return b   
}
b = copy(a) // [1,[2,3,[4,5]] , 虽然看起来一样，但是只完成了浅拷贝,里面的嵌套数组指向了同一个数组
// 方法2
function deepCopy(a){
   const newArray = []
   for(let i = 0; i < a.length; i++){
      if(typeof a[i] === 'object') { // 如果想精确一点，可以使用第3章里的Object.prototype.toString()
         // 此时我们需要递归地获取该二级数组
         newArray[i] = deepCopy(a[i])
      } else {
         newArray[i] = a[i]
      }
   }
   return newArray
}

// 另外，我们怎么深拷贝一个对象呢。涉及到两个问题：1 如何遍历一个对象的key 2 如何在key指向一个
// 嵌套对象的情况下继续深入拷贝
function deepCopyObj(obj) {
   const newObj = {}
   // 使用for-in 遍历, 这样的可以拷贝obj的可遍历属性
   // 还可以使用Object.entries(obj)来获取obj的key,value
   for(let key in obj){
         newObj[key] = typeof obj[key] !== ('object' || 'function') ? deepCopyObj(obj[key]) : obj[key] 
   }
   return newObj
}
// 测试一下
const a = {a:1 ,b:{c:1,d:{e:5}}}
const b = deepCopyObj(a)
console.log(b.b === a.b) // false，证明深拷贝成功了

// 我们可以发现两个方法实际上结构都类似，我们可以合并一下，是参数既可以是数组也可以是对象
function deepCopy(obj) {
    // 先判断obj的类型,使用instanceof 来判断会更精准一点
    const a = obj instanceof Array ? [] : {}
    // 使用ES2017新API Object.entries()遍历obj
    // [key,value]是ES6引入的解构赋值
    for([key,value] of Object.entries(obj)) {
       a[key] = typeof value === ('object' || 'function') ? deepCopyObj(value) : value
    }
    return a
}
// 测试一下
const a = [1,2,3,[4,5,6,{a:1,b:2}]]
const b = deepCopyObj(a)
console.log(b) // [1,2,3,[4,5,6,{a:1,b:2}]]
console.log(b[3][3] === a[3][3])  // false 这两个嵌套引用不指向同一个对象了
```

## _本章需要你掌握的问题：_

1. 解释一下JS里的按值传递？
2. 解释一下深拷贝和浅拷贝？
3. 进阶：手写一个深拷贝函数，可以返回数组或者对象的深拷贝?
