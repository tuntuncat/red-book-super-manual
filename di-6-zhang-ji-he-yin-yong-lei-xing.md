---
description: KEYWORDS：对象，数组，Map/Set
---

# 第6章 集合引用类型

## 6.1 Object

Object是JS中最一般的对象，所以也可以称为最“干净”的对象，因为Object的实例没有继承多少方法，Object的方法大多作为Object本身的静态方法，而非Object的原型方法。

如果你了解原型链，你可以看一下Object实例的原型有哪些方法。

![](<.gitbook/assets/image (3).png>)

除了getter和setter以外，一共就6个方法，1个属性。唯一的属性就是每个原型对象都有的constructor，默认指向实例对象的构造函数。

Object实例除了使用new + 构造函数Object实例化以外，还可以通过对象的字面量语法来创建。但是使用new关键字并不被推荐，因为字面量初始化的可读性更强，可以直接看到对象内部的key和value。

Object实例推荐使用点语法来读写数据，除了一些特殊场合：

1. 读写的属性key被存储在变量中，只能通过括号访问，例如用Symbol存储的key。
2. 另外如果使用了非合法标识符字符串来表示key，那么点语法也会失效。例如a.not valid, 因为"not valid"中间的空格，所以只能通过a\['not valid']来读写该属性。

这些实际上都属于老生常谈的玩意儿，但是对于集合引用类型。Object的难点其实也不在于最基础的声明和属性的存取，而是在于Object内部属性其实也有自己的“属性”，就像上图的get，set对应的属性\_proto\_，它又是怎样的属性呢？

所以其实我们这里需要介绍一种除了开始声明，或者中途动态添加属性的方法，一种更一般的添加属性的方法：`Object.defineProperty()`。

**`Object.defineProperty()`** 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。所以该方法本身也可以作为一个对象的工厂使用。

```javascript
// 参数：Object.defineProperty(obj, prop, descriptor)
// obj - 要修改的对象，prop - 属性key, descriptor - 属性的描述对象，即实现对属性的细粒度控制
// 对象工厂
const newObj = Object.defineProperty({}, name, 
{
    value:'Benjamin',
    writable:false // 是否可写，使用该函数定义的属性默认值是false，表示不可写
    configurable:false // 是否可删除，默认为false
    enumerable:false // 是否可使用for-in或者Object.keys()遍历，默认为false
    get(){} // 读取器，表示该属性被读时触发的函数，该函数的返回值即作为读取该属性的结果
    set(newVal){} // 设置器，当属性被赋值的时候触发，该函数的返回值作为属性的新值
}
)
```

以上介绍的六个字段便是对象实例属性的细粒度属性，依然是可以自己配置的。使用Object.defineProperty()方法定义的属性默认是“保守的”，即不可遍历，不可删除，不可写。而一般通过字面量定义的属性是“开放的”,即可遍历，可删除，可写的。另外其实也可以通过字面量来设置getter,setter。

```javascript
const students = {
    names: ['tuntun', 'Ben', 'YuYu'],
    get lastStudent() {
        if(this.names.length === 0) {
            return 'no students yet'
        } else {
            return this.names[this.names.length - 1]
        }   
}
// 读取students.lastStudent
console.log(students.lastStudent) // YuYu
```
