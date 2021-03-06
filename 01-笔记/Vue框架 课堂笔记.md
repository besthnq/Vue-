## Git 复习

1. 本地有仓库，远程没有，怎么办？

- 一般 git 仓库都有忽略文件 .gitignore。忽略一些文件，不进行 git 的版本控制

- 进行本地仓库的版本控制

  - git init 初始化 git 仓库
  - git add . 添加到暂存区
  - git commit -m '注释' 添加到版本区

- 注释规范

  - feat 特性：新增功能

  - docs 文档：新增文档
  - fix 修复 Bug

- 创建远程仓库

- 将本地仓库和远程仓库关联起来

  > git remote add origin 仓库地址

- 本地仓库将代码推送到远程仓库去

  > git push origin master

2. 将来去公司，公司有远程仓库，拉取本地进行开发

- 第一次需要克隆代码

  > git clone git@github.com:xpromise/class191227.git

- 远程仓库更新代码

  > git pull origin master

## 库、框架和插件

1. 库：封装好特定功能代码的集合体（特定功能集合体）
2. 框架：基于自身特点提供一套较完整的解决方案
3. 插件：基于某个库/框架的库

## 渐进式

- 从底向上增量开发模式

\- 比如

\- 我只需要开发一个简单静态页面，此时只要 Vue 框架即可

\- 要开发动态页面（页面中包含与后台交互的动态数据），此时使用 axios 发送请求~

\- 将来开发更加复杂功能，引入其他库或者插件 vue-router vuex 等

## vue 使用

#### 1.引入 vue.js 文件（一旦引入，全局就有一个变量 Vue，Vue 是一个构造函数）

#### 2.创建 vue 对象 new Vue（配置对象）

- 配置对象：属性名是固定的，每个固定属性有相应的作用，不能所以更改

- 第一层属性是固定的（对象的直接属性，如 el、data）

- 第二层属性可自定义

在 new Vue 内部，会将 data 上的所有属性和 methods 上面的所有方法挂在实例对象上

#### 3.模板

##### 3.1 模板页面：

动态的 html 页面，包含一些 js 语法代码：双大括号表达式 、 指令

##### 3.2 模板语法

- 差值语法(双大括号表达式)：

  _{{JS表达式}}_

  作用：向页面输出数据（**将数据显示到标签内部**）

- <p style='background-color:pink;'>指令语法</p> 指令：v- 开头的自定义标签属性
1. v-model="JS 表达式"

- 作用：用于实现 **双向数据绑定**
  - <u>常用于表单中自动收集数据，表单中注意value设定。提交表单 form 标签绑定@submit.prevent 来接收</u>
  
2. v-bind:xxx="yyy"

  - 简写： _:xxx='yyy'_
    - 作用：指定变化的属性值。**强制数据绑定** (**将数据显示在标签属性上**）
  3. v-on:click='yyy'\_

    - 简写： _@click='yyy'_
    - 作用：绑定指定事件名的回调函数。 **绑定事件监听**
    - 4种传参情况：
      - 如果函数不需要其他参数，或者只需要event参数    >>  *@click='method'*
      - 如果函数不需要event参数，只需要其他参数    >>  *@click="method('a','b')"*
      - 如果函数既需要event参数，也需要其他参数    >>  *@click="method('c',$event)"*
      - 如果事件回调函数只有一条语句,（默认去this中找xxx属性，此处不能写this）    >>  *@click="xxx=yyy"*
    - 事件修饰符：
      - 阻止事件默认行为：event.preventDefault()    >>  *@click.prevent="method"*
      - 阻止事件冒泡：event.stopPropagation()    >>  *@click.stop="method"*
    - 按键修饰符：
      - *@keyup.13="method"*   适用于所有键
    - *@keyup.enter="xxx"*   只有少部分键可以使用

  4. **条件渲染指令** *v-if  v-else  v-show*
   - v-if和v-else是配合使用的：
      - 当v-if是true时，就会显示，而v-else就隐藏；
      - 当v-if是false时，就会隐藏，而v-else就显示；
      - 当属性值是true时，往往可以省略不写
  - v-if 和 v-show 的区别
    - 相同：能实现DOM元素切换显示
    - 不同：v-if 在内存中删除标签对象来实现隐藏，重新显示时会重新创建。DOM树中只有要显示的DOM元素，没有隐藏的；  v-show 通过样式display来控制显示和隐藏的，显示标签没有样式，隐藏标签会加上 display: none。DOM树中所有DOM元素都有，只是隐藏的DOM元素有一个隐藏样式而已
    如果要频繁切换样式显示，选择 v-show。
    因为v-if要进行更多DOM操作：删除DOM元素，重新创建新的DOM元素，而v-show只要切换style样式即可
  5. **列表渲染指令**   *v-for*
   - v-for 遍历数组
     - `<li v-for="(person, index) in persons" :key="person.id">{{xxx}}</li>`
   - v-for 遍历对象
     - `<li v-for="(value, key) in person" :key="key">{{xxx}}</li>`
   - **注意：遍历的每一项元素需要有一个唯一的key属性：值有id用id，没有id考虑使用index**

  6. *v-once*
      只渲染一次，后面更新都不会再重新渲染（性能优化~）
  7.  *v-text*
      v-text 内部找到元素，调用 元素.textContent，会当做纯文本解析
  8.  *v-html*    
      v-html 内部找到元素，调用 元素.innerHTML，会当做HTML解析


9. 自定义指令
   * 注册全局指令
      ```vue
      Vue.directive('my-directive', function(el, binding){
        el.innerHTML = binding.value.toupperCase()
      })
      ```
   * 注册局部指令
      ```vue
      directives : {
        'my-directive' : {
          bind (el, binding) {
            el.innerHTML = binding.value.toupperCase()
         }  //el 就是绑定指令的DOM元素;binding 是一个对象，包含指令的所有信息
      }
      }
      ```
    ```
   
    ```
  * 使用指令
    *v-my-directive='xxx'*

  常用属性：ref
  ref : 为某个元素注册一个唯一标识, vue对象通过$refs属性访问这个元素对象
  作用：能获取DOM元素
  注意：一般能不用就不用，vue不建议直接操作DOM, 性能优化




**双向数据绑定**

1. 改变页面的输入，vue 会自动将页面最新的数据保存在代码 data 对应的属性上 （视图层 —> 数据层），数据由视图层（页面）流向数据层（代码---data）

2. 当 data 数据发生变化，vue 会自动将最新的数据更新到页面对应的位置上 （数据层 —> 视图层），数据由数据层流向视图层

   React 只有数据层流向视图层，叫做数据的单项绑定（单向数据流）

**表达式和语句**

- 表达式

  - 没有分号结尾
  - 有一个结果值（返回值，可以是 undefined）

- 语句
  - 有分号结尾，如果没有分号 编译时会自动添加分号
  - 对内部数据进行操作，没有结果值

#### 4.理解 MVVM

##### MVC

M ——> model 数据层，存放数据

V ——> view 视图层 ，展示页面

C ——> controller 控制层 ，复杂操作数据显示到页面上

##### MVVM

M ——> model 数据层，存放数据

V ——> view 视图层 ，展示页面

VM ——> viewmodel 通过数据绑定和 DOM 事件监听实现 model 和 view 的双向数据绑定

数据绑定： model ——> view

DOM 事件监听：view ——> model

#### 5.this 指向

1. 函数直接调用 fn() this 指向 window

   _特殊：在 ES5 严格模式下 this 指向 undefined_

2. 函数隐式调用 obj.fn() this 指向 obj

3. 函数显示调用 fn.call/apply(obj) this 指向 obj

4. 函数 new 调用 new Fn() this 指向实例对象

5. ES6 箭头函数 this 指向离他最近一层包裹它的函数的 this（外部函数的 this）

6. 定时器回调函数 this 默认指向 window

   _特殊：在 ES5 严格模式下 this 指向 undefined_

7. DOM 事件回调函数 this 指向被绑定事件的 DOM 元素

   _特殊：在 Vue 框架中，DOM 事件回调函数的 this 指向 Vue 的实例对象 vm_

#### 6.计算属性和监视属性详解

1.  计算属性 ---> _当属性不能直接显示，需要通过相关属性计算后才能显示时，使用计算属性_

    - 在 computed 属性对象中定义计算属性的方法
- 在页面中使用{{方法名}}来显示计算的结果
    - 通过 getter/setter 实现对属性数据的显示和监视，属性不需要在 data 中定义
- 计算属性存在缓存, 多次读取只执行一次 getter 计算
    - 计算属性：一上来会触发一次，得到结果显示到页面上；当内部依赖的值（参与计算data的值）发生变化，也会继续触发；否则使用缓存（如果内部的值没有变化，此时读取会使用上一次的缓存结果，不会重新计算）。

2.  监视属性 ---> _监视某个属性的变化，在属性发生变化需要发送 ajax 请求时才使用_

    - 通过通过 vm 对象的\$watch()或 watch 配置来监视指定的属性，属性需要在 data 中定义

    - 当属性变化时, 回调函数自动调用, 在函数内部进行计算

    **一般使用计算属性，只有需要发送请求时使用监视属性**
    
    

```html
<div id="app">
  姓:<input type="text" placeholder="First Name" v-model="firstName" /><br />
  名: <input type="text" placeholder="Last Name" v-model="lastName" /><br />
  姓名1:<input type="text" placeholder="Full Name1" v-model="fullName1" /><br />
  姓名2:<input type="text" placeholder="Full Name2" v-model="fullName2" /><br />
</div>
<script type="text/javascript" src="../js/vue.js"></script>
<!-- //1.原生js
<script>
    const person = {
        firstName: "xiaofei",
        lastName: "zhang",
      };
     // 定义单个属性
      Object.defineProperty(person, "fullName", {
        // 属性描述符 / 元属性（描述属性的属性）
        // writable: false, // 决定属性是否可以被修改
        // configurable: false, // 决定属性是否可以重新配置/删除
        // enumerable: false, // 决定属性是否被遍历for in
        // value: "123", // 属性的值

        // 访问描述符
        // 重新属性的读取/设置的方法
        get() {// 读取属性调用的方法
          return this.firstName + "-" + this.lastName; // this指向person对象
        },
        set(value) {// 设置属性调用的方法
          const [firstName, lastName] = value.split("-");
          this.firstName = firstName;
          this.lastName = lastName;
        },
      });   
</script>
-->

<script>
  const vm = new Vue({
    data: {
      firstName: "xiaofei",
      lastName: "zhang",
      fullName2: "xiaofei-zhange", //定义监视属性监控变量
    },
    computed: {
      // 计算属性:
      fullName1: {
        get() {
          return this.firstName + "-" + this.lastName;
        },
        set(value) {
          const [firstName, lastName] = value.split("-");
          this.firstName = firstName;
          this.lastName = lastName;
        },
      },
    },
    watch: {
      // 监视属性: 这个属性必须存在data中
      firstName(newValue, oldValue) {
        // 监视data中firstName属性的变化，一旦变化就会触发当前函数
        this.fullName2 = newValue + "-" + this.lastName;
      },
      lastName(value) {
        // 监视data中lastName属性的变化，一旦变化就会触发当前函数
        this.fullName2 = this.firstName + "-" + value;
      },
      fullName2(value) {
        const [firstName, lastName] = value.split("-");
        this.firstName = firstName;
        this.lastName = lastName;
      },
    },
  }).$mount("#app");

  // 用的很少
  // vm.$watch("fullName2", function (value) {
  // const [firstName, lastName] = value.split("-");
  // this.firstName = firstName;
  // this.lastName = lastName;
  // });
</script>
```
### Vue 基本语法

```vue
const vm = new Vue(配置对象)

el 值：元素选择器 作用：获取vm要挂载的DOM元素。$mount() 可以取代~
data 值：对象
作用：保存要渲染到模板页面的动态数据（一般数据/非函数数据）

methods 值：对象
作用：保存要渲染到模板页面的方法（函数数据）

computed 值：对象
作用：保存计算属性（定义属性getter和setter）

什么时候使用计算属性？当需要使用属性要通过计算才能使用（data中不用定义这个属性）
理解：计算属性是一种特殊的data，每次取值需要先计算才能得到~

watch 值：对象
作用：监视某个data属性的变化
什么时候使用watch属性？当data属性变化时需要发送AJAX请求，才需要使用（data中必须定义这个属性）
$watch 可以取代

filters 值：对象
作用：对要显示的数据进行特定格式化后再显示。详见11.

directives 值：对象
作用：自定义指令

template 值：字符串
作用：定义组件要渲染的模板页面

components 
作用：定义组件

特点：data和methods上的属性和方法，最终都会直接挂载到vm/this/Vue实例对象上~
```



#### 7.class和style绑定

作用：class/style绑定就是专门用来实现动态样式效果的

默认情况下使用 class，当样式的值是动态确定，用 style

**class绑定: :class='xxx'**

* xxx是字符串 ：一般用于类名不确定的单个样式 

  *`<p :class="className">xxx</p>`*

* xxx是对象：一般用于类名确定的单个样式

  *`<p :class="{red: isRed, green: !isRed}">xxx</p>`*

* xxx是数组：一般用于多个确定的动态类名

  *`<p :class="['red', 'green']">xxx</p>`*

**style绑定：**  *:style="{ color: activeColor, fontSize: fontSize + 'px' }"*

* Vue的style语法: 是一个对象形式，里面所有属性名都采用小驼峰命名法
* 其中activeColor/fontSize是data属性
  
#### 8.数组方法比较 filter、map、reduce
* filter  长度变值不变
  * 返回一个新数组，不会对原数组产生任何影响（不会修改原数组）
  * 特点：新数组长度往往比原数组更少，但里面的值和原来的一定一样
* map 长度不变值变
  * 返回一个新数组，不会对原数组产生任何影响（不会修改原数组）
  * 特点：新数组长度和原数组一定一样，但里面的值往往会发生变化
* reduce 长度和值都变
  * 语法：arr.reduce((previousValue, currentValue) => {}, initValue)
  * 如果希望reduce方法返回值是number类型，initValue往往初始化为 0
  * 如果希望reduce方法返回值是object类型，initValue往往初始化为 {}
  * 如果希望reduce方法返回值是array类型，initValue往往初始化为 []
  * 如果希望reduce方法返回值是string类型，initValue往往初始化为 ''
* find方法
  * 回调函数返回值true就找到了并返回找到的元素，返回值false就没找到就会继续找


#### 9.Vue实例对象的生命周期函数
Vue的实例从创建到更新到死亡经历的回调函数，由vue内部自己调用。
**Vue对象的生命周期分3个阶段：**
* 初始化渲染阶段（new Vue()产生，只会执行1次）
  * beforeCreate
    * 此时已经创建了vm，是在实现数据代理和监听之前调用
    * 不能访问data/methods数据
  * created
    * 在实现数据代理和监听之后调用
    * 可以访问所有数据
  * beforeMount
    * 在页面挂载（渲染）之前触发
  * mounted
    * 在页面挂载（渲染）之后触发
* 更新阶段（当data数据发生变化，就会自动更新, 触发n次）
  * beforeUpdate
    * 在更新之前触发
    * 此时data数据已经更新完毕，但是页面没有更新
  * updated
    * 在更新之后触发
    * data数据更新完毕，页面也更新完毕
* 销毁/死亡阶段 (this/vm.$destroy()触发，触发1次 )
  * beforeDestroy
    * 在销毁之前调用
  * destroyed
    * 在销毁之后调用
  注：当调用this.$destroy()时，会自动解绑事件，所以没有DOM事件的内存泄漏。定时器需要手动清除。
  
  **开发中常用的重要生命周期函数**
  * created / mounted （created速度更快一点）
    * 发送AJAX请求、设置定时器等一次性任务
  * beforeDestroy
    * 做一些收尾工作：取消AJAX请求，清除定时器等
  


  内存泄漏：数据占用内容，但无实际用途。DOM事件、定时器、意外全局变量等
  内存溢出：预期使用的内存，超出实际内存


#### 10.过渡和动画
1. vue提供组件transition，专门用来做过度效果 。会给目标元素添加/移除特定的class
2. 基本过渡动画的编码
   * 在目标元素外包裹`<transition name="xxx">`
   * 定义class样式
     * 指定过渡样式: transition
     * 指定隐藏时的样式: opacity/其它
3. 过渡的类名
   * xxx-enter-active: 指定显示的transition
   * xxx-leave-active: 指定隐藏的transition
   * xxx-enter: 指定隐藏时的样式
   * 默认类名：v-enter v-enter-to v-enter-active v-leave v-leave-to v-leave-active

#### 11.过滤器

功能: 对要显示的数据进行特定格式化后再显示
<u>并没有改变原本的数据, 可是产生新的对应的数据</u>
全局过滤器：对所有vm生效
局部过滤器: 只对当前vm生效
过滤器使用：

* 定义过滤器
  
  * `Vue.filter(filterName, function(value[,arg1,arg2,...]{return newValue})`

* 使用过滤器

  * `<div>{{myData | filterName}}</div>`
  * `<div>{{myData | filterName(arg)}}</div>`
  

使用dateFormat过滤器对nowTime处理，最终显示的是过滤器的返回值
时间格式化处理，往往使用工具函数库：moment、dayjs（常用）、date-fns

```html
 <div id="test">
      <h2>显示格式化的日期时间</h2>
      <p>{{nowTime | dateFormat}}</p>
      <p>{{nowTime | dateFormat('YYYY年MM月DD日')}}</p>
      <p>{{nowTime | dateFormat('HH:mm:ss')}}</p>
      <p>{{nowTime | dateFormat2}}</p>
    </div>
    <script type="text/javascript" src="../js/vue.js"></script>
    <script src="https://cdn.bootcss.com/dayjs/1.8.24/dayjs.min.js"></script>
    <script>
      // 全局过滤器：对所有vm生效
      Vue.filter("dateFormat2", function (value) {
        return dayjs(value).format("HH:mm");
      });

      new Vue({
        data: {
          nowTime: Date.now(), 
        },
        filters: {     //局部过滤器    
          dateFormat(value, formatStr = "YYYY-MM-DD HH:mm:ss") {
            return dayjs(value).format(formatStr);
          },
        },
      }).$mount("#test");
```

#### 12.数据代理

当定义实例化对象 `new Vue({ data: { isShow: true } })` 时， Vue 内部解析时会对 data 中的数据进行数据代理。Vue 会自动给 vm（this/实例对象）添加一个直接属性 isShow ，并且设置该属性的 getter 和 setter `类似于~ Object.defineProperty(vm, 'isShow', { get() {}, set() {} })`
所以这些数据具备一些特点，本身是没有值的
当读取 isShow 属性的值时，内部会自动调用 getter 方法并返回值出去（实际得到的是 getter 方法的返回值）
当设置 isShow 属性的值时，内部会自动调用 setter 方法，更新值并更新模板页面


#### 13.响应式数据

1. 什么是响应式数据？
   数据一旦发生变化，会自动更新页面/数据
   （页面输入数据发生变化，会自动更新 JS 中 data 数据 / data 数据发生变化，会自动更新页面）

2. 哪些数据是响应式数据？
   Vue 中 data 中所有数据都是响应式数据
   data中数据分为两种情况探讨：
   数组数据：内部也会 setter 监视，但是会有例外：
      this.persons[0] = { id: 7, name: "jack" };
      解决： this.persons.splice(0, 1, { id: 7, name: "jack" });   变异方法
   对象数据/其他类型数据：内部都会给属性添加 setter 进行监视，值一旦发生变化，即会更新值也会触发页面的更新

3. 响应式和非响应式
   响应式数据
      data 中的所有数据（data 对象，data 函数返回的对象）
      通过 vm.$set() / Vue.set() 设置的属性数据
   非响应式数据   
      手动给vm添加属性  
        this.msg2 = xxx
      手动通过 . 方式给data数据添加额外的属性（得使用vm.$set()解决）
        this.person.age = 18

#### 14.组件


- 模块
  - 具有特定功能效果 js 文件
- 模块化
  - 当 js 文件采用一个一个模块编写的就是一个模块化应用
- 组件
  - 具有特定功能效果的集合体（HTML/CSS/JS...）
- 组件化

  - 当应用程序采用 一个一个组件编写的就是一个组件化应用



1. 面试题：为什么组件中的data必须是函数形式？
   Vue解析组件标签时，会找到组件的构造函数，创建组件实例对象，根据实例对象的内容进行显示。
   如果data使用的是对象形式，那么创建组件实例对象，进行数据代理时，组件实例对象代理的data数据是同一个对象。那么只要有一个变化，全都变。
   每个组件应该要单独使用自己的数据。所以data要使用函数。那么创建组件实例对象，进行数据代理，会调用data函数得到新data对象从而进行数据代理，每一个组件实例对象得到的是新的对象，互不影响

2. 总结
    定义组件 组件构造函数 Vue.extend(options/配置对象)
    注册组件 Vue.component(组件名称, 组件构造函数)
    定义并注册组件（全局组件） Vue.component(组件名称, options/配置对象)
    options/配置对象: data、methods、computed、watch、filters、directives、template
    使用组件 以标签组件使用 <xxx></xxx>
    当你使用组件标签时，内部会找到组件的构造函数，创建组件实例对象
   ```vue
    // 定义组件
    const Component = Vue.extend(options); 
    new Vue({
      components: { // 注册局部组件 
        'component': Component
      }
    })
    ```

## Vue 脚手架

### webpack

一个现代 JavaScript 应用程序的静态模块打包工具

1. 5 个核心概念

- 入口 entry
  - 指示以哪个文件开始打包
  - 注意：以入口文件为起点，构建依赖关系图，将所有依赖的文件全部打包进来
- 输出 output
  - 打包后资源输出到哪里去
- 加载器 loader
  - webpack 工具本身只能打包 js、json 资源，其他资源打包不了
  - 需要借助 loader 解析其他资源，webpack 才能打包这些其他资源
- 插件 plugins
  - 执行更加强大的任务（相对 loader 来讲）
- 模式 mode
  - 开发模式 development
  - 生产模式 production
    - 相同点：都能解析 ES6 模块化
    - 不同点：production 多一个压缩 JS 代码

2. 基本使用

- 初始化 package.json 文件

  - npm init
  - npm init -y

  ```json
  {
    "name": "vue-cli", // 包名
    "version": "1.0.0", // 包的版本号
    "scripts": {
      // 启动指令
      "start": "xxx", // npm start
      "dev": "xxx", // npm run dev
      "build": "xxx" // npm run build
    },
    /*
      如果你把开发依赖的包下载到生产依赖会不会有问题？反之会不会有问题？
        不会影响任何功能。
      生产依赖：项目运行时需要使用的依赖（vue，jquery）
      开发依赖：webpack构建打包需要使用的依赖（webpack，babel）
        解决：直接重下（注意依赖）
    */
    "dependencies": {}, // 生产依赖
    "devDependencies": {} // 开发依赖
  }
  ```

- 下载依赖包

  - npm i webpack webpack-cli -D

- 定义 webpack 配置文件

  - webpack.config.js

- 项目根目录
  - 配置文件就在项目根目录
  - 下载包也在项目根目录下
  - 启动 webpack 指令也是在项目根目录
  - 哪个目录是项目根目录？
    - 02.定义 vue 脚手架
    - 包含整个项目的最近的目录（package.json 文件所在的目录）

### webpack的配置文件
所有JS构建工具都是基于NODEJS工作的，所以模块化默认使用commonjs。使用commonjs模块化语法向外暴露一个配置对象（属性名固定的对象）。里面配置不能写错，一旦写错单词就会报错（代码写完检查一遍~）
  开发环境：让代码在内存中编译运行即可，没有输出文件到本地
  生产环境：输出打包后的资源文件到本地

1. 处理js资源
    babel  一个 JavaScript 编译器，可以将ES6以上语法编译成ES5以下语法~，作用用来做JS兼容性处理

    - 下载依赖包（loader只需要下载不需要引入）
      npm i babel-loader @babel/core @babel/preset-env -D 
    - 配置loader  
    ```js
    module: {
    rules: [
      
      {
        test: /\.js$/, // 规则对哪些文件生效
        // exclude: /node_modules/, // 排除node_modules文件，其他文件都检查
        include: [resolve("src")], // 包含src下面的文件，只检查包含的文件，而其他文件不检查
        // use: {}, 如果只要使用一个loader 用{}
        // use: []  如果要使用多个loader 用[]
        use: {
          // 需要下载
          loader: "babel-loader",
          options: {
            // 配置对象
            presets: ["@babel/preset-env"], // 预设，babel要干什么活
            plugins: [], // 插件
          },
        },
      },
    ],
    }
    ```

2. 处理css资源
    - 下载依赖包（loader只需要下载不需要引入）
        npm i style-loader css-loader -D
    - 配置loader  
    ```js
    module: {
    rules: [
      
      {
        test: /\.css$/,
        include: [resolve("src")],
        use: [
          // 执行顺序：从下到上 / 从右到左
          // 动态创建style标签，将js中css字符串添加，插入head中显示
          "style-loader",
          // 将css编译成js字符串，以commonjs规则插入到js文件中
          "css-loader",
        ],
      },
    ],
    }
    ```

3. 处理图片资源
    - 下载依赖包（loader只需要下载不需要引入）
        npm i url-loader file-loader -D
    - 配置loader  
    ```js
    module: {
    rules: [
      
      {
        test: /\.(png|gif|jpe?g|webp)$/,
        include: [resolve("src")],
        use: {
          loader: "url-loader",
          options: {
            /*
              大小小于10kb以下的图片会被base64处理
              base64:
                1. 一种图片的优化手段（只针对小图片做优化）
                2. 将图片编译成base64编码的字符串
                  优点：随着html文件加载一起加载，不需要额外发送请求（减少请求数量，降低服务器压力）
                  缺点：体积会变得更大
            */
            limit: 10 * 1024,
            /*
              对输出文件进行重命名
              [hash:10] hash（根据文件生成唯一id值）取10位
              [ext] 使用原来文件扩展名
            */
            name: "static/media/[hash:10].[ext]",
            /*
              默认情况下 url-loader 对图片解析是ES6模块化
              ES6模块化识别不了 [object module]
              关闭ES6模块化，使用commonjs模块化就能识别了~
            */
            esModule: false,
          },
        },
      },
    ],
    }
    ```

4. 处理html资源
   - 下载依赖包(plugins既需要下载也需要引入)
      `npm i html-webpack-plugin -D`
      `const HtmlWebpackPlugin = require('html-webpack-plugin');`
   - 配置plugin
  ```js
  plugins: [
    new HtmlWebpackPlugin({
      // 配置对象
      // 以 public/index.html 文件为模板，创建基于这个文件的新HTML文件
      // 新HTML文件会自动引入webpack打包生成JS/CSS
      template: resolve("public/index.html"),
    }),]
  ```


5. 处理其他资源（字体图标~）
   - 下载依赖包
        `npm i file-loader -D` (之前处理图片资源时，已经下载过了，所以不需要重新下载)

    - 配置loader
  ```js
  module: {
    rules: [
      
      {
        // test: //,  // 不写test，代表匹配所有文件
        exclude: [/\.js$/, /\.css$/, /\.html$/, /\.(png|gif|jpe?g|webp)$/, /\.vue$/],
        use: {
          // 作用：将文件加载，原封不动输出出去(只修改名称)
          // 能处理所有类型文件
          loader: "file-loader",
          options: {
            name: "static/media/[hash:10].[ext]",
          },
        },
      },
    ],
  }
  ```

6. 自动化

   一旦修改源代码，会自动编译，接着自动刷新浏览器，从而看到最新的效果;第一次使用时，自动打开浏览器访问。（自动编译、自动刷新、自动打开浏览器等自动化任务）
   如果没有自动化，每次写完代码，都需要重新编译打包刷新
   有了自动化，自动编译打包刷新，我们开发者只需要看浏览器最新的结果,提升开发效率

  - 下载依赖包 
        `npm i webpack-dev-server -D`

  - 配置
  ```js
  devServer: {
    // contentBase: resolve('build'), // 开发服务器将哪个目录的资源暴露出去
    contentBase: resolve("dist"), // 开发服务器将哪个目录的资源暴露出去
    port: 9527, // 服务器端口号
    host: "localhost", // 服务器域名,
    // 启动gzip压缩
    // 这种压缩格式浏览器可以识别，所以可以自动解压（反观zip文件浏览器是不识别，也不能解压的）
    // 资源会在服务器先进行gzip压缩，文件体积就更小，传输速度就更快。性能更好
    compress: true,
    open: true, // 自动打开浏览器
    // 热模块替换（Hot Module Replacement）
    // 正常没有HMR功能，一旦有一个文件发生变化，整个页面会全部重新渲染。假设我有10000个文件，因为其中一个文件变化，导致所有文件全部重新编译加载更新，性能很差。
    // HMR功能：一旦有一个文件发生变化，只会更新这变化的文件，其他文件默认使用之前缓存，速度快，性能好
    // html文件在将来开发时只有一个，所以不需要HMR功能
    // css文件，因为使用style-loader处理，默认使用HMR功能
    // js文件，默认是没有使用HMR（即使开启了HMR，也需要手动写其他代码才可以使用）
    hot: true,
    quiet: true, // 启用静默模式，在终端不打印多余信息
    clientLogLevel: "none", // 在浏览器控制台不打印多余内容
  },
  ```
  - 启动指令
    webpack 一定会有输出资源（输出到配置文件output.path去），不能启用devServer配置
    webpack-dev-server 只在内存中编译打包，不会有任何输出，同时能启用devServer配置

  - 配置启动指令
    在package.json中配置启动指令
  ```js
    "scripts": {
          "dev": "webpack-dev-server", // 代表启动开发环境指令
          "start": "npm run dev" // 指令简写为npm start
        }
  ```

7. devtool 开发调试工具

  所有代码（HTML/CSS/JS）经过webpack编译打包处理，默认会将所有js以eval方式汇总在一个js文件（built.js）中，后面实际运行就是这个文件built.js。代码报错提示的是built.js代码中的错误，开发者不知道到底出了什么错误，不利于调试BUG

  source-map：提供构建后代码与源码映射关系文件
  浏览器支持 source-map 技术，在webpack打包时会生成一个built.js.map文件，这个文件就会将构建后代码和源码的关系记录起来（源代码在哪个文件第一行 对应 构建后代码第几行）
  如果构建后built.js代码出错了，浏览器会找到built.js.map文件，根据构建后错误位置，通过built.js.map文件， 就能追踪到源码的错误，从而浏览器提示源码的错误，方便调试

  - 配置
  ```js
  devtool: "cheap-module-source-map", // 开发环境
  devtool: "source-map", // 生产环境
  ```
  source-map 提供完整代码映射（包括行和列）
  cheap-source-map 提供简版代码映射（只包含行，没有列）
  module-source-map 提供node_modules中代码映射
  cheap-module-source-map 

8. 进行vue配置（让webpack能够解析vue资源）
  - 下载

  `npm install -D vue-loader vue-template-compiler`

  vue-loader  处理vue文件
  vue-template-compiler  编译vue组件模板代码

  - 配置
  ```js
  const VueLoaderPlugin = require('vue-loader/lib/plugin');

  module.exports = {
            module: {
              rules: [
                // ... 其它规则
                {
                  test: /\.vue$/,
                  loader: 'vue-loader'
                },
                {
                  test: /\.css$/,
                  use: [
                    'vue-style-loader', //修改后 可以应用到 .css文件 及 .vue文件的<style>中
                    'css-loader'
                  ]
                }
              ]
            },
            plugins: [
              new VueLoaderPlugin(),  // 请确保引入这个插件！
              // 它的职责是将你定义过的其它规则复制并应用到 .vue 文件里相应语言的块。
              // 例如，如果你有一条匹配 /\.js$/ 的规则，那么它会应用到 .vue 文件里的 <script> 块。
            ]
          }

  ```


9.  打包public下面的静态资源

  - 下载
    `npm install copy-webpack-plugin --save-dev`
    
  - 配置

```js
const CopyPlugin = require('copy-webpack-plugin');//引入

plugins:[
  new CopyPlugin([
    {
      from: resolve("public"), // 将public下面的所有文件复制
      to: resolve("dist"), // 复制到dist目录下去
      ignore: ["index.html"], // 复制时忽略index.html文件（这个文件已经被HtmlWebpackPlugin处理了）
    },
  ]),
]
```

10. 配置路径别名
    
    ```js
  resolve: {    // 帮助webpack解析模块（打包的资源）
    alias: {
      // 配置文件路径别名
      // 当你路径写 vue 实际上代表的路径 vue/dist/vue.esm.js
      // xxx$ 真正写路径时 $ 可以省略不写~
      // 'vue$': "vue/dist/vue.esm.js",
      "@": resolve("src"),
      "@comps": resolve("src/components"),
    },
  },
    ```
11. 自动补全文件扩展名   

    ```js
  resolve: {
    // 解析模块路径时，如果没有文件扩展名，会按照数组顺序自动补全文件扩展名
    extensions: [".js", ".vue", ".json"],
  },
    ```





### Vue组件化使用

vue项目默认有一个App.vue组件（应用主组件/根组件）
  组件里面有三个标签：
      template 模板页面：里面写模板代码
        注意：必须有且只有一个根标签
      script 组件配置对象：里面写js代码
      style 模板样式（组件样式）：里面写css代码
            scoped：让样式只在当前组件生效（类似于作用域），实现方法：给当前组件标签中添加特定的字符串

  App.vue组件使用：
    - 引入其他组件，使用ES6模块化语法，向外暴露一个组件配置对象: data\methods\watch\computed...，
    - 注册组件  组件名: 组件构造函数，用ES6对象简写形式
    - 使用组件：通过组件标签使用
      <HelloWorld />  <!--单标签（常用）-->
      <HelloWorld></HelloWorld>  <!--双标签-->
      <hello-world></hello-world> <!--写代码不太方便-->

  index.js使用：
  index.js是webpack打包的入口文件
  开发前端/客户端代码，使用都是ES6模块化

  - 引入组件
    `import Vue from "vue";`   // npm i vue 安装
    `import App from "./App";`   //webpack中配置路径别名+自动补全扩展名
    `import Hello from "@comps/HelloWorld";`

  - 注册组件
    Vue.component("Hello", Hello);  // 全局注册一个组件

    ```js
    // 方法1：内部会创建App组件实例对象，并渲染到 "#app" 元素上
      new Vue({
        render: (h) => h(App),
      }).$mount("#app");   // 去public/index.html中找

    //方法2：
      new Vue({
        components: {
           App, // 注册App组件
        },
        template: "<App />", // 内部渲染App组件内容
      }).$mount("#app");

    ```
    方法1是方法2的简写，但方法2直接使用会报错。
    原因：默认使用Vue的版本是运行时版本（vue.runtime.esm.js）, 这个版本没有编译器，没有编译器就不能解析template，所以报错
    解决：
    * 使用render方法去对 template 进行预解析（内部使用 vue-template-compiler 去编译template） --推荐使用，体积更小
    * 使用带编译器的vue版本  --体积更大
  


### 组件化编码流程（开发代码套路）

1. 拆分组件

- 根据用户页面功能或者变化来拆分组件

  - 用户页面功能：JS 交互功能
  - 用户页面变化：用户界面更新变化


2. 实现静态组件

- 实现前面拆分组件的静态结构和样式，JS 功能先不写

- 结构样式

3. 实现动态组件

- 初始化 data 数据的问题

  - 要不要定义 data 数据？页面有没有变化/更新
  - 数据类型：[{id: 1, name: 'xx', content: 'xxx'}]
  - 数据名称：comments / commentList
  - 数据保存在哪个组件? App
    - 如果数据只有一个组件使用，就定义在这个组件内容
    - 如果数据由多个组件使用，就定义在多个组件的公共父组件中

- 完成功能
  - 实现初始化数据显示
  - 实现 JS 交互功能（添加数据/更新数据/删除数据...）

- 父组件如何向子组件传递数据
  - props（标签属性）：通过标签属性方式传递数据
    - 特点：props是父组件传递数据给子组件，子组件只能读取使用，不应该直接修改  通过计算属性更新数据
  - 父组件定义data数据 `{comments: [{}, {}]}`
  - 父组件给子组件指定标签属性：`<CommentList :comments="comments" />`
  - 子组件声明接受标签属性（声明接受之后，子组件实例对象就直接拥有这个属性）
  - 子组件声明接受标签属性方式：
    - 数组形式
      props: ['prop1', 'prop2']
    - 对象形式
      props: {
        prop1: Object,
        prop2: Array,
      }

      props: {
        prop1: {
          type: Number,  // 类型是Number
          default: 0, // 默认值为 0
          required: true, // 必须要传的属性（必要的）
          validator: function (value) { // 校验函数
            return value >= 0 // 值必须大于0
          }
        }
      }

- 组件关于数据的2个重要问题
  - 数据定义在哪个组件
    - 如果数据只有一个组件使用，就定义在这个组件内容
    - 如果数据由多个组件使用，就定义在多个组件的公共父组件中
  - 更新数据的方法定义在哪个组件？
    - 数据源在哪里，更新数据方法就定义在哪

- 父组件给子组件传递数据
  - 函数
    - 例子：addComment/Function delComment/Function
    - 作用：子组件调用函数修改父组件数据（子组件传递数据给父组件  子 --> 父）
  - 非函数
    - 例子：comments/Array comment/Object
    - 作用：父组件传递子组件直接显示使用（父组件传递数据给子组件 父 --> 子）
    - 注意：子组件不应该直接修改数据，应该通过调用父组件的方法来修改



Web Strorage 浏览器本地离线存储方案：用来存储大量数据（4mb）

localStorage 持久化存储（一直都有）
sessionStorage 会话存储（打开浏览器访问网页：开始会话，关闭浏览器: 结束会话）。当浏览器没有关闭，存储不会消失，但是一旦关闭浏览器，存储会自动销毁

xxxStorage.setItem(key, value) 存储数据(注意：value必须是字符串类型，不是的话会调用toString方法强制转化)
xxxStorage.getItem(key) 读取数据
xxxStorage.removeItem(key) 删除单个数据
xxxStorage.clear() 删除全部数据

配合 JSON.stringfy  和 JSON.parse 方法

```js
watch: {
    // 浅度监视，只能监视todos的第一层属性的变化，todos里面对象监视不到
    // todos(val) {
    //   // 监视todos的变化，一旦变化就存储起来
    //   window.localStorage.setItem("todos", JSON.stringify(val));
    // },

    // 深度监视：监视todos所有值的变化
    todos: {
      deep: true,
      handler(val) {
        window.localStorage.setItem("todos", JSON.stringify(val));
      },
    },
  },

```















零碎知识点：
1. 表达式：

!!xxx 为了将xxx数据强制转换成布尔值
!xxx 为了xxx数据强制转换成布尔值并取反
2.  mouseenter/mouseleave （通常用法）：进入元素触发mouseover ，离开元素触发mouseout ，和子元素无关；

mouseover/mouseout ：
进入元素触发mouseover 离开元素触发mouseout 。 如果进入子元素，会触发父元素mouseout / 子元素mouseover
      问题：导致事件触发n次



3.  

4. 
    