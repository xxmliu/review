# CSS父子元素定位的使用
首页展示，利用定位完成。

```html

  <div class="zt">
      <!-- 背景图 -->
      <div class="back-img">
        <img src="./img/download.jpg" alt=""/>
      </div>
      <!-- 版心 -->
      <div class="center">
        <!-- 导航栏 -->
        <div class="nav">
          <!-- logo -->
          <div class="logo">
            <img src="./img/logo.png" alt=""/>
          </div>
          <!-- 导航内容 -->
          <ul>
            <li>首页</li>
            <li>笔记</li>
            <li>关于</li>
            <li>售后</li>
            <li>登录</li>
          </ul>
        </div>
        <!-- 练习浮动/定位 -->
        <div class="fd">
          <div class="fd1"></div>
          <div class="fd1"></div>
          <div class="fd1"></div>
        </div>
      </div>
    </div>



/* 去样式 */
* {
  margin: 0;
  padding: 0;
}

li {
  list-style: none;
}

a {
  text-decoration: none;
}

.zt {
  width: 1520px;
  height: 960px;
  margin: 0 auto;
  position: relative;
}

/* 背景图 */
.back-img img{
  width: 100%;
  height: 100%;
  position: absolute;
  top:0;
}

/* 版心 */
.center {
  width: 1200px;
  margin: auto;
  position: absolute;
  z-index: 999;
  top: 0;
  right: 0;
  left: 0;
}


/* 导航栏 */
.nav {
  width: 100%;
  height: 100px;
  display: flex;
}

/* logo */
.nav .logo img {
  height: 100%;
  position: relative;
}

/* 导航标题 */
.nav ul {
  display: flex;
  line-height: 100px;
  text-align: center;
  position: absolute;
  right: 0;
}

.nav ul li {
  color: #fff;
  font-size: 30px;
  margin-left: 40px;
}

.nav ul li:hover {
  border-bottom: 1px solid #fff;
}

/* 定位练习 */
.fd {
  width: 500px;
  height: 500px;
  position: absolute;
  top:300%;
}

.fd .fd1 {
  width: 300px;
  height: 100px;
  background-color: red;
  margin-bottom: 100px;
}
```

# ***arguments函数重载***

```js
	function zhekou(money) {
      // 判断实参的个数,  3个 就是满减
      if (arguments.length == 3) {
        if (money >= arguments[1]) { //超过满减条件
          money -= arguments[2]
        }
      }

      // 两个参数
      // 判断实参的个数,  2个 就是打折
      if (arguments.length == 2) {
        // 参数2: 字符串类型 - 代表 vip
        // 参数2: 数字类型 - 折扣
        // typeof转类型判断是否为数字/字符串
        if (typeof arguments[1] == 'number') {
          money *= arguments[1]
        }
        if (typeof arguments[1] == 'string') {
          if (arguments[1] == 'vip1') {
            money *= 0.95
          }
          if (arguments[1] == 'vip2') {
            money *= 0.8
          }
        }
      }

      return money
    }

    // zhekou : 计算折扣价格的函数
    // 使用方式:
    console.log(zhekou(3000, 0.8)) // 消费3000 打八折
    console.log(zhekou(3000, 0.6)) // 6折

    console.log(zhekou(3000, 2000, 500)) // 满2000 减500
    console.log(zhekou(3000, 3000, 700)) // 满3000 减700

    console.log(zhekou(3000, 'vip1')) // 95折
    console.log(zhekou(3000, 'vip2')) // 8折
```

# instanceof: 判断对象类型

**instanceof和typeof类似**

- instanceof 判断对象是否是指定构造函数创建的

- **typeof**判断JS基本数据类型

- **instanceof**判断JS对象数据类型

```js
function calc() {
      // 判断数组长度是1位
      if(arguments.length == 1){
        if(typeof arguments[0] == 'number'){
          return arguments[0] * arguments[0]
        }
      }
      // 判断数组长度是2位
      if(arguments.length == 2){
        if(typeof arguments[0,1] == 'number'){
          return arguments[0] + arguments[1]
        }
      }
      // 判断数组长度是3位
      if(arguments.length == 3){
        if(typeof arguments[0,1,2] == 'number'){
          return arguments[0] * arguments[1] * arguments[2]
        }
      }

      // 数组类型
      // instanceof: 判断对象是否是指定构造函数创建的
      if(arguments[0] instanceof Array) {
        // let一个变量保存总和
        let total = 0
        // for循环出数组里的值
        for(let i = 0; i<arguments[0].length; i++){
          total += arguments[0][i]
        }
        // 退出循环return
        return total
      }
    }


    // 实现一个 calc 函数, 预期效果如下
    console.log(calc(10)) //算出数字的平方, 即 10 * 10
    console.log(calc(20)) //算出数字的平方, 即 20 * 20
    console.log(calc(10, 20)) //算出和值, 即 10 + 20
    console.log(calc(10, 20, 30)) //算出乘积, 即 10 * 20 * 30

    console.log(calc([11, 22, 33])) //数组类型, 则计算出数组内容的和
```

# this的用法

- 是函数中自带的一个变量, 指向函数`运行时`所在的对象 -- **非常灵活**

使用场景?

- 为函数提供了另一种执行方式
  - 传统方案: 通过传递参数的方式  把对象传入
  - 当前方案: 把函数作为参数传递到对象里执行 -- 反过来

```js
    // 矩形对象:
    var r1 = { length: 10, width: 20 }
    var r2 = { length: 100, width: 120 }

    // area函数: 用于计算 矩形的面积  长 * 宽

    // 传统做法:
    function area(rect) {
      return rect.length * rect.width
    }

    console.log(
      area(r1), area(r2)
    );


    // this模式的函数
    function area1() {
      // this: 运行时服务的对象, 所在的
      return this.length * this.width
    }

    // 1. 把 area1 存储到对象中 :  上门服务
    r1.area1 = area1
    console.log(r1)
    // 2. 执行 r1 中的 area1 函数
    console.log(
      r1.area1()
    )
    // 3. 执行完毕后, 从对象中删除.
    delete r1.area1

    // 练习: 把 area1 放到 r2 执行
    // 1. 上门服务:  函数存入r2中
    r2.area1 = area1
    // 2. 在 r2 中执行
    console.log(r2.area1())
    // 3. 删除
    delete r2.area1
```

```js
    // 立方体 长*宽*高
    var c1 = { length:10, width:20, height:30 }

    // 创建一个volume函数
    function volume() {
      // 传入之后调用c1，这里this指c1本身
      return this.length * this.width * this.height
    }

    // 将volume传入到c1对象中
    c1.volume = volume
    // 调用c1对象中的volume
    console.log(c1.volume())

    // 结束后删除
    delete c1.volume
```

# call的用法

```js
	// call: 短暂拜访
    // 函数 具有一个短暂拜访对象的方法 -- call
    function area() {
      return this.length * this.width
    }

    var r1 = { length: 10, width: 20 }

    // 任务: 把 area 函数临时放到 r1 对象中执行
    console.log(
      area.call(r1) // area函数短暂拜访 r1 对象
    )

    console.dir(area) // dir: 直接输出函数对象

    // 练习: 立方体
    var c1 = { length: 10, width: 20, height: 30 }

    // 1. 制作 volume 函数, 计算 体积=长*宽*高
    // 把此函数放到 c1 中执行, 获取其体积
    function volume() {
      return this.length * this.width * this.height
    }
    console.log(volume.call(c1))

    // 2. 制作 area 函数, 计算 面积=(长x宽 + 长x高 + 宽x高)*2
    // 把此函数放到 c1 中执行, 获取其面积
    function area1() {
      return (this.width * this.length + this.length * this.height + this.width * this.height) * 2
    }

    console.log(area1.call(c1))
```

```js
	var emp1 = { name: "亮亮", salary: 30000 } //月薪
    var emp2 = { name: "凯凯", salary: 10000 }
    var emp3 = { name: "泡泡", salary: 20000 }

    // 所得税汇算函数  shui
    // 年薪 10~ 15w   扣税 5%
    // 年薪 >15 ~ 20  扣税 10%
    // 年薪 >20 ~ 30  扣税 15%
    // 年薪 >30 ~ 40  扣税 20%
    // >40  扣税40%;   <10  不扣税
    function shui() {
      // 算年薪
      let total = this.salary * 12
      // 小于10w
      if( total<100000 ) return 0
      // 年薪10~15w
      if( total>=100000 && total<150000 ) return total * 0.05
      // 年薪15~20w
      if( total>=150000 && total<200000 ) return total * 0.1
      // 年薪20~30
      if( total>=200000 && total<300000 ) return total * 0.15
      // 年薪30~40
      if( total>=300000 && total<400000 ) return total * 0.2
      // 大于40
      if( total>=400000 ) return total * 0.4
    }

    // call短暂访问emp对象，结束后离开
    console.log(shui.call(emp1));
    console.log(shui.call(emp2));
    console.log(shui.call(emp3));
```

- call传参

​		参数1: 指定函数执行时所在的对象, 即 this 的指向

​		参数2 之后 : 传递给函数的实参列表

```js
	var emp = { ename: '亮亮', salary: 20000 }

    // 制作一个函数, 用于获取员工  n 个月的总薪资
    function total(n) {
      return this.salary * n
    }

    console.log(
      // 6个月
      // 参数1: 指定函数执行时所在的对象, 即 this 的指向
      // 参数2 之后 : 传递给函数的实参列表
      total.call(emp, 6)
    )

    ///////////////////////
    var x = { a: 10 }

    function show(b, c, d) {
      return this.a + b + c + d
    }

    console.log(
      show.call(x, 20, 30, 40)
    );
```

