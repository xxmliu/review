# CSS画出0.5px的线

# CSS父子元素定位的使用

首页展示，利用定位完成。

# ***arguments函数重载***

# instanceof: 判断对象类型

**instanceof和typeof类似**

- instanceof 判断对象是否是指定构造函数创建的

- **typeof**判断JS基本数据类型

- **instanceof**判断JS对象数据类型

# this的用法

- 是函数中自带的一个变量, 指向函数`运行时`所在的对象 -- **非常灵活**

使用场景?

- 为函数提供了另一种执行方式
  - 传统方案: 通过传递参数的方式  把对象传入
  - 当前方案: 把函数作为参数传递到对象里执行 -- 反过来

# call的用法

- call传参

​		参数1: 指定函数执行时所在的对象, 即 this 的指向

​		参数2 之后 : 传递给函数的实参列表

# apply用法

函数的一个属性, 作用和 call 方法极其相似:

- 相同点：

  函数.apply(对象): 把函数临时放到对象里执行, 修改函数中的this指向

- 不同点:

​		实参通过 数组类型 进行传递:  **函数.apply(对象, [实参, 实参, ...])**  

- 用途:

​		如果函数接收的是实参列表, 但是我们只有数组类型, 则利用此函数实现数组转实参列表的效果

# bind的用法

提前绑定 函数和运行时的资源, 简化后续调用时的格式  

作用: 把函数和其运行时需要的资源捆绑在一起, 返回新的函数  

# call、apply、bind的区别

**函数触发的三种方案**  

- call: 临时把函数放在对象中执行, 用于设定this的指向
- apply: 临时把函数放对象中执行, 可以把数组 转为 参数列表
- bind: 提前绑定 函数和运行时的资源, 简化后续调用时的格式

# 构造函数

构造函数: 功能是用于构建创造对象的函数, 称为构造函数，函数名大驼峰

# new运算符

- new运算符: 搭配构造函数使用时, 可以自动完成一些代码
- 函数前存在 new 运算符, 则认为此函数为构造函数

# 三目运算符

# 原型和原型链

- 构造函数构造出来的对象，都有一个`__proto__`属性 ，这个`__proto__`指向构造函数的prototype

- 总结:为什么要设计原型模式?

  ​	节省内存

- 如何节省的?

  ​	把公共的方法存储在 共享的对象 : 构造函数.prototype 中

- new 运算符生成对象时, 自动为对象关联 `__proto__`到 共享对象 prototype 上

- JS引擎的原型链设计, 全自动

  ​	如果 对象.属性 对象自身没有, 则自动到`__proto__` 中查找!

# 数组的元素

# 数组的高阶函数

**高阶函数: 函数中使用了其他函数, 就叫高阶函数**  ----不属于ES6的新特性

- every：和逻辑与&&相似，全都满足条件
- some：和逻辑或||相似，至少有一个满足
- filter：把满足条件的过滤出来
- map：映射，把数组每个元素处理返回值后，返回新的数组

# AJAX用法和封装AJAX

封装AJAX：

```js
// 需求:
// get(地址, 回调函数)
// callback:回调; 简写: cb
function get(url, cb) {
  let xhr = new XMLHttpRequest();
  xhr.open('get', url);
  xhr.onload = function () { 
    let data = JSON.parse(xhr.response);

    cb(data)    // 传到回调函数中
  }
  xhr.send();
}
```

使用封装的AJAX：

# forEach的用法

***数组的遍历操作: 4种方案***

- **for循环遍历**

- **for..in** 

  用于遍历对象类型, key是属性名, 字符串类型

  由于数组属于对象类型的一种, 所以可以用for..in遍历. 但是并不合适

- **for..of** 

  来自 ES6

  **特色:** 直接遍历值;

  **区别：****for..in**先拿属性名 再通过属性名拿值，**for..of** 更加直接

- **forEach** 

  来自 ES6

  没有返回值, 只是存粹的遍历数组

- 取舍问题:

  通常对数组采用 forEach 方案

  对 伪数组 / 类(似)数组 采用 for..of 方案

  伪数组/类数组: 内容与数组的结构相同, 但是原型不是数组的，无法使用forEach，如arguments。

# reduce的用法

**reduce:** 减少, 合并

把数组中的元素 经过处理之后, 合并成 1个值

把数组的元素 累加到一起, 得到总和

- 参数1: 每个元素都被此函数处理, 其中 box 形参, 接收的是 当前的总和
- 参数2: 初始时的 总和

# 数组数据转HTML代码

- map 搭配 join 使用

​		缺点: 用map和join 两个函数完成任务

- forEach 搭配 外部的变量

​		缺点: 需要额外的外部变量

- reduce

​		缺点: 理解上有难度, 使用少

# dom初体验

**DOM: Document Object Model 文档 对象 模型**

- 文档: html代码
- 对象: js对象
- 模型: html代码 转换成 js对象 的这套流程

**浏览器中真正显示的是 全局中的document 对象**

- 可以通过JS来修改document中的值, 进而影响到页面上的内容展示

# 元素的事件

**事件:** 在元素上触发的一些事情, 能够触发的事件都被系统提前规定好 

- 所有 **on** 开头的属性, 都是事件相关的

https://www.runoob.com/jsref/dom-obj-event.html 

# style操作

# querySelectorAll

- query:查询 selector:选择器 all:所有
- 通过选择器查找所有符合的元素
- 此方式查询的结果, 是类数组类型, 但是其原型 NodeList中存在forEach方法可以实现遍历操作
