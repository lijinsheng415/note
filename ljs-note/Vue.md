# 什么是Vue

vue是一套用于构建用户界面的渐进式JavaScript框架

#### Vue特点

- 1.采用组件化模式,提高代码复用率,且让带吗更好维护
- 2.声明式编码,让编码人员无需直接操作DOM，提高开发效率。
- 3.使用虚拟Dom+优秀的Diff算法，尽量复用Dom节点

JavaScript自身是使用命令式编码，繁琐且麻烦，无法复用Dom节点

vue是面向数据的编程,其作者设计时参考mvvm的设计模式

mvvm: m -> model数据 也就是data里面的内容 , v -> view视图 template里面的内容, vm -> viewModel 视图数据连接层,对应Vue实例对象.

#### Vue注意事项

- **所有由Vue管理的函数,最好写成普通函数,因为使用箭头函数this指向会错误,****`data`****、****`mounted`****等**
- **所有不被Vue管理的函数(定时器,ajax),最好写成箭头函数,因为箭头函数没有自己的this,会跟随外层的this指向Vue**

# Vue 2

## 创建`Vue2`实例

***在Vue2中模板的最外层不能有多个根元素标签,当有多个标签时需要用一个标签包裹***

```html
<head>
    <script src="../js/Vue.js"></script> 引入Vue源码
</head>
<body> 
    <div id="root">hello {{ name }}</div> 为Vue服务的容器
</body>
<script>
    const vm = new Vue({      创建Vue实例
        el: '#root',         绑定容器
        data() {
            return {
                 name:'张三'
            }
        }               
    })
</script>
```

- 创建一个为Vue服务的容器`root`,容器里面的代码依然符合`html`规范，只不过混入了一些Vue语法.
- 创建`Vue`实例,类似于`class`需要使用`new`的形式,创建实例时,里面的参数是一个对象,对象里面书写`Vue`的配置.
- `el`:用于绑定容器,`#`表示id,容器与`Vue`实例是一一对应了,不可一对多/多对一
- `data`:用于存放`Vue`的数据,其标准语法应该是`data`为一个函数,返回一个存放`vue`据的对象

在控制台中打印`Vue`实例`vm`会得到一个对象,这个对象和这个实例缔造者的原型对象上所有的$开头的方法我们都可以使用.例如 ***[vm.$data.name](http://vm.$data.name)*** 赋值后就可以修改vue的数据,从而改变显示的内容.

#### Vue绑定容器的另一种形式

```html
<script>
    const vm = new Vue({      创建Vue实例
        data() {
            return {
                 name:'张三'
            }
        }               
    })
    vm.$mount('#root')
</script>
```

#### {{插值表达式}}

在`Vue`绑定的容器中可以使用双花括号的形式`{{插值表达式}}`,在花括号中可以书写`Vue`数据、js表达式(不可以是js语句),一旦vue里面`data`中的数据发生改变,页面的显示也会随之改变.

#### template 模板

```html
<body> 
    <div id="root"></div> 为Vue服务的容器
</body>
<script>
    const vm = new Vue({      创建Vue实例
        el: '#root',         绑定容器
        data() {
            return {
                 name:'张三'
            }
        },
        template:` <div>{{name}}</div>`               
    })
</script>
```

- template:用于书写Vue中的html结构,如果不书写Vue默认会把绑定的DOM元素作为模板进行解析
- template与data同级,值为字符串,使用普通字符串时不支持换行书写,使用模板字符串可以换行
- template的书写形式与在DOM中一致，可以正常书写插值表达式,元素绑定等

#### template 标签

```html
<template>
    <div1></div1>
    <div2></div2>
</template>
```

> `template`也是`Vue`中的一个标签,这个标签只作为占位的用处,在输出时会自动删除template.

> 由于`Vue2`中模板最外层只允许存在一个标签,如果我们需要将多个标签放在最外层,可以使用`tempalte`标签包裹,在输出时标签会被删除,就相当于我们在最外层使用了多个标签

## 组件component

#### 局部组件

```javascript
const student = Vue.extend({
      data(){
         return {
              name:'张三',
              age : 18
           }
      },
      template: `
         <div>
             <h2>学生姓名:{{name}}</h2> 
             <h2>学生年龄:{{age}}</h2>
          </div>` 
})
```

#### 局部组件中使用局部组件

```js
 const school = Vue.extend({ 
     data(){
        return {
            name: '中国家里蹲大学',
            address: '中国'
         }
      },
     components:{student}
      template:`
          <div>
              <h2>学校名称:{{ name }}</h2> 
              <h2>学校地址:{{address}}</h2>
              <Student></Student>
          </div>`
 })
```

#### Vue实例使用组局组件

```html
 <body>
     <div id="box">
         <School></School>
     </div>

     <script>
        new Vue({
             el:'#box',
             components:{ 
                  School,
                  }
         })
      </script>
  </body>
```

`Vue.extend({})`:用于创建组件,对象内的配置与`new Vue()`时一致

`components`: `Vue`实例中用于引入局部组件的对象,里面输入创建局部组件名即可

#### 全局组件

```html
<body>
     <div id="box">
          <Hello></Hello>
     </div>
    <script>
       const hello = Vue.extend({
            data(){
               return {
                  str:'hello world'
                }
             },
             template:`
                    <h2>{{ str }}</h2>
                  `
         })

         注册全局组件
         Vue.component('Hello',hello); 
              //生成Vue实例
         new Vue({
             el:'#box',
           })
      </script>
</body>
```

创建全局组件:全局组件与局部组件创建的方法一致都是使用`Vue.extend`.

注册全局组件: `Vue.component('组件名',组件)`

#### 组件创建简写

```js
 const school = { 
     data(){
        return {
            name: '中国家里蹲大学',
            address: '中国'
         }
      },
     components:{student}
      template:`
          <div>
              <h2>学校名称:{{ name }}</h2> 
              <h2>学校地址:{{address}}</h2>
              <Student></Student>
          </div>`
 }
```

`const school = Vue.extend({})`可以简写为`const school = {}`

#### 局部组件与全局组件

- 局部组件与全局组件创建时都是使用 `Vue.extend({})`创建
- 注册局部组件:在Vue里面的`components`中注册使用,局部组件只能在注册的地方使用
- 注册全局组件:需要使用`Vue.component('Hello',hello);`的形式注册,全局组件注册后在任何地方都可以使用
- 子组件的使用:`<School></School>` 与`<School/>`不在脚手架中必须使用双标签的形式,否则会导致后续组件不能渲染,在脚手架中两种形式都可以使用

#### 组件命名

- 一个单词组成:
  
  - 第一种写法(首字母小写):school
  - 第二种写法(首字母大写):School

- 多个单词组成
  
  - 第一种写法(段横线分割):my-school,注册局部组件时对象中用引号包裹
  - 第二种写法(首字母大写):MySchool (需要Vue脚手架支持)
  
  1.创建的组件school的本质是一个名为VueComponent的构造函数,且不是程序员定义的,是Vue.extend生成的
  
  2.我们只需要写<school/>或<school></school>,Vue解析时会帮我们创建school组件的实例对象
  
  3.特别注意:每次调用Vue.extend,返回的都是一个全新的VueComponent
  
  4.关于this指向
  
  - (1).组件配置中
  - data函数,methods,watch,computed中的函数,他们的this均是【VueComponent实例对象】
  - (2)new Vue(option)配置中
  - data函数,methods,watch,computed中的函数,他们的this均是【Vue实例对象】
  
  5.VueComponent与Vue基本一致,以后简称vc，Vue简称vm
  
  一个重要的内置关系:VueComponent.prototype.**proto** === Vue.Prototype
  
  组件实力对象(vc)可以访问到Vue原型上的属性,方法

## 数据绑定

***使用了数据绑定后引号中为表达式,不使用引号中就是字符串***

#### v-bind单向数据绑定

`v-bind`用于绑定将`Vue`中的数据绑定到指定的标签属性上

```html
<a v-bind:href="url">点击跳转</a>  
```

`v-bind:XXX`可以简写为`:XXX`

```html
<a :href="url">点击跳转</a>  
```

#### v-model双向数据绑定

`v-model`可以进行双向数据绑定,例如`input`输入框,可以实现`data`中的数据可输入框的`value`一致

```html
<input v-model:value="inputValue" />
```

`v-model:value`可以简写为`v-model`,,因为v-model默认收集的就是value的值

```html
<input v-model="inputValue" />
```

#### v-model 收集表单数据

1. 当表单是输入框时,v-model收集的是value值,用户输入的就是value
2. 当表单是单选框时,v-model收集的是value,需要自己配置value值
3. 当表单时多选框时,配置input的value属性:
   3-1.v-model的初始值是非数组,那么收集的就是checeke
   3-2.v-model的初始值是数组,那么收集的就是value组成的数组
4. 当是下拉框时,如果存在`value`收集value,不存在`value`则收集内容
   4-1: 单选,收集value或者内容
   4-2: 多选,收集value或内容组成的数组

```html
<body>
    <div id="box">
         输入框
        <input type="text" v-model="name">
          多行文本
        <textarea v-mode="desc"></textarea>
       <!-- 不可以使用 <textarea >{{desc}}</textarea> -->
        单选框
        <input type="radio" id="man" value="Man" v-model="sex">
        <label for="man">男</label>
        <input type="radio" id="woman" value="Woman" v-model="sex">
        <label for=woman>女</label>

        <input type="checkbox"  v-model="checked">

        多个复选框
        <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
        <label for="jack">Jack</label>
        <input type="checkbox" id="john" value="John" v-model="checkedNames">
        <label for="john">John</label>
        <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
        <label for="mike">Mike</label>
        下拉列表单选
        <select v-model="selected">
            <option disabled value="">请选择</option>
            <option >A</option>
            <option >B</option>
            <option >C</option>
        </select>

        下拉列表单选
        <select v-model="selectedList" multiple>   multiple 多选
            <option disabled value="">请选择</option>
            <option >A</option>
            <option >B</option>
            <option >C</option>
        </select>

    </div>
<script>
var vm = new Vue({
    el:'#root',
    data(){
        return {
            name: 'zhangsan', //对应输入框 
            sex: 'man' ,      //对应单选框
            checked: true,    //对应单个复选框
            checkedNames: [], //对应多个复选框
            selected: '',     //对应单选下拉列表
            selectedList:[],  //对应多选下拉列表
        }
    }
})
</script>
</body>
```

### Vue中的数据代理

Vm中的data ,就是浏览器显示的vm对象中的_data

- Vue中的数据代理:    通过vm对象来代理data对象中属性的操作(读/写)
- vue中数据代理的好处:更加方便操作data中的数据
- 基本原理:
  - 通过object.defineProperty()把data对象中的所有属性添加到vm上. 为每一个添加到vm上的属性,都制定一个getter/setter. 在getter/setter内部去操作(读/写)data中对应的属性

## 事件处理

```html
<body>
<div id="box">
    <input type="button" value="按钮" v-on:click="handlebtnClick">
    <input type="button" value="按钮" @click="handlebtnClick(2.$event)">
</div>
<script>
var vm = new Vue({
    methods: {
        handlebtnClick() {
            alert('你好')
          }
    }
})
</script>
</body>
```

`v-on:`:`Vue`中绑定实践的操作符, `v-on:`可以简写为`@`,后面写`事件="操作函数"`.

- 如果不需要传参那么可以不用写函数的括号,在函数调用时可以得到一个`event`的参数
- 如果需要传参时并且需要`event`对象,需要在传递的参数后面以`$event`的形式把event对象传递过去
- 同时绑定多个操作函数时必须每个都写上括号,且用逗号分隔

#### methods

`methods`: methods是`Vue`的一个配置项,其中用于书写函数.

#### 事件修饰符

| @click.stop="函数"    | 阻止向外事件冒泡                        |
| ------------------- | ------------------------------- |
| @click.prevent="函数" | 阻止默认行为                          |
| @click.self="函数"    | 自己触发,子元素不触发                     |
| @click.capture="函数" | 把事件运营默认变成捕获模式(默认是冒泡)            |
| @click.once="函数"    | 只执行一次                           |
| @wheel.passive="函数" | 当绑定wheel事件时使用passive修饰符可以提高滚动性能 |

#### 按键修饰符

| @keydown.enter="函数"  | 当按下回车时触发                                  |
| -------------------- | ----------------------------------------- |
| @keydown.delete="函数" | 当按下删除时触发                                  |
| @keydown.esc="函数"    | 当按下退出时触发                                  |
| @keydown.space="函数"  | 当按下空格时触发                                  |
| @keydown.tab="函数"    | 当按下换行时触发(必须配合keydown才能使用)<br>配合 keyup 不好用 |
| @keydown.up="函数"     | 当按下上时触发                                   |
| @keydown.down="函数"   | 当按下下时触发                                   |
| @keydown.left="函数"   | 当按下左时触发                                   |
| @keydown.right="函数"  | 当按下右时触发                                   |
| @keydown.ctrl.y="函数" | 按下ctrl 和y时执行                              |

#### 系统修饰符

ctrl,alt,shift,meta(系统菜单)

- 配合keyup使用:按下修饰键同时,再按下其他键,随后释放其他键,事件才能被触发
- 配合keydown使用 正常触发
- 使用时还可以在@keydown后.键码 ,但是不推荐使用

#### 自定义键名

- `Vue.config.keyCodes.自定义键名 = 键码` ;
- 使用 `keydown.自定义键名` 就可以使用 不推荐

#### 鼠标修饰符

- left左键点击:`@click.left="操作函数"`
- right右键点击: `@click.right="操作函数"`
- middle滚轮点击:`@click.middle="操作函数"`

#### 精确修饰符

- `exact`: `@click.ctrl.exact="操作函数"` 当按住ctrl键点击时触发

## computed计算属性

```html
<body>
<div id="box">{{ fullname }}</div>
<script>
const vm = new Vue ({ 
       data(){
          return {
              firstname : '张',
              lastname: '三'
            }
        },
        computed:{
            fullname () {
                return this.firstname + '-' + this.lastname
              }
        }
    })
    vm.$mount('#box')
</script>
</body>
```

`computed`计算属性,值为一个对象,在其中定义原本不存在,需要计算得来的属性.

如果计算的属性不需要修改,可以写成函数的形式,返回计算后的结果即 可

如果计算的属性需要修改,需要写成对象的形式,其中包括`get()`、`set()`两个函数

```js
computed:{
    fullname : {
        get() {
            return this.firstname + '-' + this.lastname
        }
        set(value) {
            var arr = value.split('-');
            this.firstname = arr[0];
            this.lastname = arr[1];
         }
    }
}
```

- `get()`用于获取数据,在其中返回计算的结果,计算属性的函数形式就相当于只有`get()`
- `set()`用于修改,`set()`会接收到一个参数,就是我们要修改的数据,将得到的参数赋值到`data`数据中

> 原理:底层借助了`Object.defineproperty`方法提供的`getter`、`setter` `computed`属性存在缓存,`data`中的数据不修改就不会再次执行,只有数据修改才会重新计算,某些情况下`computed`比`methods`效率更高,`methods`每次都需要重复调用.

***计算属性中不可以用定时器延时器,等异步操作***

**计算属性创建时不需要在data里面弄个空的同名数据,会报错.直接在计算属性时命名即可**

## watch监听属性

`watch`用于监听`data`中的数据是否发生改变,其值是一个对象,对象内用于书写监听的逻辑

监听数据时,需要把监听的数据作为`key`值,在其对应的`value`的对象中写具体操作

#### 普通数据类型 1

```js
watch:{
    isHot:{
        immediate:true,
        handler(newvalue,oldvalue){console.log(newvalue,oldvalue)}
    }
}
```

#### 普通数据类型 2

```js
vm.$watch('isHot',{
        immediate:true,
        handler(newvalue,oldvalue){console.log(newvalue,oldvalue)}
})
```

监听属性时,在其内部有一个`handler()`函数,有两个参数分别是`newvalue(改变后)`、`oldvalue(改变前)`,复杂数据类型只有`newvalue(改变后)`,无法获取修改前的参数,每当属性发生改变,watch就可以监听到,并且执行其`handler()`函数.

`immediate`: 初始化时候就调用.

#### 监听属性简写

```js
watch:{
isHot(newValue,oldValue) {console.log('isHot 被修改了')}
}

或

vm.$watch('isHot',function(newValue,oldValue){console.log('isHot 被修改了')})
```

#### 深度监听复杂数据类型

```js
data(){
    return {
        numbers:{a:1,b:3}
        }
}
watch:{
    'numbers.a':{
        handler() {console.log('a被改变了')}
    },
    numbers:{
        deep:true,
        handler() {
            console.log('numbers改变了')
        }
    }
}
```

监听一个对象里面的属性时需要用字符串包裹起来`'对象名.key'`,要不然会报错.

- `deep`: 用来开启深度监听,不开启无法监听复杂数据类型.

**在watch中使用定时器/延时器时,内部参数要使用箭头函数,不要使用普通函数,因为本身定时器的this就是指向windows,而箭头函数没有自己的this**

#### computed和wtach的区别

- `computed`可以完成的操作`watch`都可以完成
- `watch`可以完成的`computed`不一定可以完成,例如异步操作,定时器.

## Vue中Css操作

```html
<head>
    <style>
        .red {color: red}
        .green {color: green}
    </style>
</head>
<body> 
    <div id="box">
        <div style="color:yellow">行内样式</div>  
        <div :style="styleObject">动态绑定一个写有样式的类</div>
        <div class="red">绑定类</div>
        <div :class="classString" >动态绑定类</div>
        <div :class="classObject" >对象动态绑定多个类</div>
        <div :class="classArray" > 数组形式绑定多个类</div>
        <demo class="green" />
    </div> 
</body>
<script>
const app = Vue.createApp({
    data() {
        return {
            styleObject:{
                color: 'yello',
                background: 'orange'
            },
            classString: 'red',
            classObject:{
                red:true,
                green:true,
            },
            classArray:['red','green',{brown:false}],
        }
      }
   })

app.mount('#box')
</script>
```

组件的`style`与`class`都可以使用动态的形式绑定,绑定时可以是类名、数组、对象,当绑定数组或对象时,里面所有的样式都会随之绑定.

## v-if 条件渲染

```js
data() {
    return {
        show: false,
        show1: true
        }
},
template:`
<div v-if="show">if</div>
<div v-else-if="show1">else if</div>
<div v-else>else</div>
`
```

在`Vue`中使用`v-if`指令进行判断,当值为真时加载节点,值为假时删除节点.

多重判断: `v-if`,`v-else-if`,`v-else`,使用多重判断时三个标签必须挨着

## v-show 条件隐藏

```js
data() {
    return {
        isshow: false,
        }
},
template:`
<div v-show="isshow">show</div>
`
```

`v-show`:用来显示与隐藏标签,值为真显示标签,值为假时标签的样式为 `display:none`

如果节点需要频繁的显示与隐藏,使用`v-show`比`v-if`更加节省资源

## v-for 列表循环

```html
<head>
    <script src="../js/Vue.js"></script> 引入Vue源码
</head>
<body> 
    <div id="root">

            <div v-for="(item,index) in list" :key="item"> 
                {{item}} -- {{index}}
            </div>



            <div v-for="(key,value,index) in object" :key="key"> 
                {{key}}--{{value}} -- {{index}}
            </div>

            <div v-for="item in 10" :key="item"> 
               {{item}}
            </div>

    </div>
</body>
<script>
    const vm = new Vue({      创建Vue实例
        el: '#root',         绑定容器
        data() {
            return {
               list: ['one', 'two' , 'three'],
               Object:{
                      fistName: 'zhangsan',
                      lastName: '李四',
                      job: 'mom'
                                } 
            }
        }               
    })
</script>
```

循环列表时`item`是每一项,`index`为下标.

循环对象时`key`和`value`分别对应键和值,`index`下标.

在`Vue`中使用循环时,必须要有一个属性`key`,且`key`必须是唯一的

#### 循环中key原理

- 1.虚拟DOM中key的作用
  - key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】
  - 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较
- 2.对比规则
  - 2-1旧虚拟DOM中找到了与新虚拟Dom相同的key
    - 若虚拟DOM中内容没变，就直接使用之前的真实DOM
    - 若虚拟DOM中内容变了，则生成新的真实Dom，随后替换掉之前的真实DOM
  - 2-2 旧虚拟Dom中未找到与新虚拟Dom相同的key
    - 创建新的真实DOM，随后渲染到页面
- 3.用index作为key可能会引发的问题：
  - 3-1对数据进行：逆添加、逆顺序删除等破坏顺序操作：
    - 会产生没必要的真实DOM更新，界面效果没问题，但效率低
  - 3-2如果姐狗狗还包含输入类的DOM：
    - 会产生错误DOM更新 界面会出现问题
- 4.开发中如何选择key？：
  - 1.最好是用每条数据的卫衣标识作为key，比如id、手机号、身份证号等唯一值
  - 2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key值是没有问题的

#### 数组对象修改 空

## Vue内置指令/v-

#### v-text

`v-text="str"` 会向其所在的节点中渲染文本内容.会替换节点中的内容

#### v-html

`v-html="str"`:向指定节点中渲染包含Html所有的内容

- 与差值表达式的区别
  - (1).v-html会替换掉节点中所有的内容,插值表达式不会
  - (2).v-html可以识别html结构
- **v-html有安全性问题!!**
  - (1).再网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
  - (2).一定要在可信的内容上使用v-html,永远不要用在用户提交的内容上

#### v-cloak

```html
<head>
     <style>
        [v-cloak]{
            display: none;
        }
    </style>   
<head>

<body>   
    <h2 v-cloak>{{ str }}</h2>
</body>
```

`v-clock`: 组件内被编译完毕才会进行显示,可以防止网速慢,页面展示出现问题

#### v-once

`v-once`:所在标签的内容只第一次会动态渲染,渲染后数据再发生改变,也不会随之改变

#### v-pre

`v-pre`:标签内的内容不会被编译,原样输出

### directive自定义指令

#### 局部指令

```html
<body>
    <div id="root">
        <h2>当前n值是:<span v-text="n"></span></h2>
        <h2>放大10倍后的n值是: <span v-big="n"></span></h2>
        <input type="text" v-fbind:value="n">
        <button @click="n++">n++</button>
    </div>
    <script>
        const vm = new Vue({
            el: '#root',
            data() {
                return {
                    n:9,
                }
            },
            directives: {
                fbind: {
                    bind(element, binding) {
                        element.value = binding.value
                    },
                    inserted(element, binding) {
                        element.focus();
                    },
                    update(element, binding) {
                        element.value = binding.value
                    }
                },
                 big(element, binding) {
                    console.log(element,binding);
                    element.innerText = binding.value * 10;
                },
            }
        })
    </script>
</body>
```

> 自定义指令里面的函数可以接收到两个参数,一个是元素的真实dom,另一个指令的对象,其中包括传递的`value`

- 完整写法: 指令(key):配置对象(value),对象中包含三个函数
  1. bind(){}: 指令在与元素成功绑定时调用的函数
  2. inserted(){} : 指令所在的元素呗插入页面时调用的函数
  3. update(){}: 指令所以在模板结构被重新解析时调用的函数
- 简写 : `指令(element, binding){}`, 何时会被调用
  1. 元素与指令成功绑定时
  2. 指令所在的模板被重新解析时

#### 全局指令

```js
Vue.directive('fbind',{
        bind(element, binding) {
             element.value = binding.value
        },
        inserted(element, binding) {
              element.focus();
        },
        update(element, binding) {
              element.value = binding.value
         }
}
```

注意事项

- (1).指令定义时不加v-,但使用时要加v-
- (2).指令名如果是多个单词,要使用kebab-case方式命名,不要使用驼峰,且作为key时要用引号包裹
- (3).如果需要获取父节点,获取元素的焦点需要在元素插入页面后才可以操作

### Vue 检测数据改变原理与添加数据

1. Vue会监视data中所有层次的数据

2. 如何监测对象中的数据:
   
   通过setter实现监控,且要在new Vue时就传入需要监测的数据.

3. 监测数组中的数据 ,通过包裹数组更新元素的方法实现,本质就是做两件事:
   
   - 调用原生对应的方法对数组进行更新
   - 重新解析模板,进而更新页面

#### **数据劫持**

**把普通的数据操作后便有有getter与setter的操作就叫做数据劫持,**

```js
   const vm = new Vue({
            el: '#root',
            data() {
                return {
                  nameLis:['zhangsan','lisi'],
                }
            },
           mounted(){
             this.$set(this.nameLis,2,'wangwu')
           }
        })
```

- **Vue.set()和vm.$set()不能给vm或vm的根数据对象添加属性**
- `Vue.set(target,propertyName/index,value)`
- `vm/this(Vue配置中).$set(target(目标位置),propertyName(属性名)/index,value)`

在Vue修改数组/对象,必须以数据劫持的形式添加,否则不会存在动态数据. 数组可以使用以下所有,对象只能用`set()方法`

API: push(),pop(),shift(),unshift(),splice(),sort(),reverse()

Vue.set() 或vm.$set()

**使用其他方法修改时,可以在修改后的数组赋值给原来的数组**

### filter 过滤器

```html
   <div id="box">
        <h2>现在是:{{ time | timeFormater }}</h2>
        <h2>现在是:{{ time | timeFormater("YYYY_MM_DD") | mySlice }}</h2>
    </div>
    <script>
        Vue.filter('mySlice', function (value) {
            return value.slice(0, 4);
        })
        new Vue({
            el: '#box',
            data() {
                return {
                    time: 1621561377603,
                }
            },
            filters: {
                timeFormater(value, str = 'YYYY-MM-DD HH:mm:ss') {
                    return dayjs().format(str)
                },
                mySlice(value) {
                    return value.slice(0, 4);
                }
            }
        })
    </script>
```

filter:也是`Vue`的一个属性,值为对象其中可以配置多个.

filter定义: 对要现实的数据进行特定格式化后再显示(适用于一些简单格式的处理),并没有改变原本的数据,是产生新的对应数据.

过滤器多数书写在差值表达式中 用|(管道符)分割,左边是传递的参数右侧是需要调用的函数,多个过滤器可以串联,左边的返回值自动作为右面的参数传入

- 语法:
  
  1.注册过滤器
  
  - 全局过滤器: Vue.filter(name,callback)
  - 局部过滤器: new Vue({filter:{}})
  
  2.使用过滤器: {{ xxx | 过滤器 }} 或v-bind:属性 =" xxx | 过滤器"

### 生命周期函数

生命周期函数:也叫做生命周期钩子,在Vue运行的某一时刻会自动执行的函数,配置在Vue配置对象的最外层.

| 函数            | 运行时刻     |
| ------------- | -------- |
| beforeCreate  | Vue初始化之前 |
| created       | Vue初始化完毕 |
| beforeMount   | 组件挂载之前   |
| mounted       | 组件挂载完毕   |
| beforeUpdate  | 页面更新前    |
| updated       | 页面更新完毕   |
| beforeDestory | 组件销毁前    |
| destoryed     | 组件销毁完毕   |

生命周期函数应该使用普通函数的形式,因为需要其内部的`this`指向这个Vue.

最常用的两个生命周期函数 :

1. mounted 发送ajax请求,启动定时器,绑定自定义事件,订阅消息等初始化操作
2. beforeDestoty:清除定时器,解绑自定义事件,取消订阅消息,等收尾事件

关于销毁Vue实例

1. 销毁后借助Vue开发者工具看不到任何信息
2. 销毁后自定义事件会失效,但是原生DOM事件依然有效
3. 一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了

收起静音新窗口打开
wolai-yang
wolai-yang

`$nextTick()`也是个特殊的生命周期函数,其作用是当页面渲染完毕后再更新页面

#### nexttick()

- 1.语法: this.$nextTick(回掉函数)
- 2.作用:在下一次DOM更新结果后执行其指定的回调
- 3.什么时候使用：当数据改变后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行
- $nextTick:将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。它跟全局方法Vue.nextTick一样，不同的是回调的 this 自动绑定到调用它的实例上。

   **要求改变的数据必须在当前的组件里面,否则不好用**

## Vue Cli 脚手架工具

### 脚手架安装

- 需要存在nodejs稳定版, Vue3要求nodejs至少8.0以上, nodejs中文网[Nodejs中文网](https://nodejs.org/zh-cn/)
- 切换国内下载源: `npm config set registry https://registry.npm.taobao.org`
- 删除历史版本: `npm uninstall vue-cli -g` , `yarn global remove vue-cli`
- 安装Vue Cli : `npm install -g vue-cli`,4.5.15版本可以支持浏览器自动打开
- 查看版本 : `vue -V`

### 创建Vue项目

1. 在目录下使用 `vue create name` 创建项目

2. 配置Vue,选择 Vue版本,及需要的插件等 自定义配置
   
   - 1. 选择Manually select features 自定义配置,进入列表后选择babel,linter/Formatter,然后回车在选择需要vue版本,选择 3.x
   - 3. 选择 ESLint with error prevention only
   - 4.选择Lint on save
   - 5.配置项放在哪里 In dedicated config files(放到单独的配置文件),In package.json(放到package.json里)

3. 命令:  
   
   - `npm run serve` 运行
   
   - `npm run build` 打包

### 项目目录介绍

```
App
 ├─ node_modules(文件夹):存放依赖包的文件夹
 ├─ public(文件夹):存放静态资源,
 ├─ src(文件夹):程序员代码源文件夹
 │    ├─ assets(文件夹):存放静态资源,图片,视频等
 │    ├─ componens(文件夹):存放非路由组件(全局组件)
 │    ├─ pages/views(文件夹):用于存放路由组件
 │    ├─ App.vue:管理所有组件的Vue组件
 │    ├─ main.js: 项目入口文件
 │    ├─router:存放路由的配置文件(.js)
       plugins.js     存放插件
 ├─ .gitignore: 里面的文件不会上传到git仓库
 ├─ bable.config.js:babel配置文件
 ├─ jsconfig.json:
 ├─ package-lock.json: 依赖包的具体信息
 ├─ packge.json: 项目信息,依赖包等
 ├─ README.md: 工程说明
 ├─ vue.config.js: Vue的配置文件
```

- src目录:是程序员主要操作的目录,代码都在里面

- public目录: 放在public文件夹中的静态资源,webpack进行打包的时候,会原封不动的打包到dist文件夹中

#### Vue版本介绍

- 1.vue.js与vue.runtime.xxx.js的区别
  
  - (1).vue.js是完成版的vue,包含核心功能+模板解析器
  - (2).vue.runtime.xxx.js是运行版(残缺版)的Vue,只包含核心功能,没有模板解析器

- 2.因为vue.runtime.xxx.js没有模板解析器,所以不能使用template配置项,需要使用render函数接收到的createElement函数去指定具体内容
  
  **Vue中默认引入的是运行版的Vue**

### 代码介绍

#### app.vue

```html
<template>
     <School/>
</template>
<script>
  import School from 'School.vue';
    export default {
    name:'App',
    components:{
      School
    }
}
</script>
<style>
</style>
```

#### main.js

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  el:'#app'
  render: h => h(App),  //默认引入运行版Vue,需要借助render函数
})
```

#### 单文件组件

在脚手架中,所有vue组件都是以`.vue`结尾的文件形式呈现, `.vue`文件也称之为**单文件组件**

单文件组件只有在脚手架中才可以使用.

单文件组件,一般由三个部分组成,template模板书写布局,script书写js语法,style书写样式

组件中每个组件需要使用模块语法导出,

在单文件组件中使用import 语法引入的.vue 文件可以不写后缀

#### render()函数

在引入了运行版的`Vue`后由于没有`template`模板配置项,使用组件是需要借助`render()`函数来

```js
render(createElement) {
    return createElement('h1','hello world')
}
```

`rander`函数用于帮助我们解析模板

`render(createElement)`函数会接收一个参数,这个参数也是函数,我们通常使用这个参数来创建DOM节点, 使用这个参数创建节点时需要给其传入两个参数,标签和内容.

如果传递的是组件直接把组件传递过去即可

  

## ref

```html
<template>
    <div id="app">
        <h1 ref="title">Hello World</h1>
    </div>
</template>
<script>
export default {
    mounted() {
        console.log(this.$refs.title);
    }
}
</script>
```

`ref`:可以用来替代id,素或子组件注册引用信息,应用在html标签上返回的是真实DOM元素，应用在组件标签上是组件实例对象（vc).

使用方式：

- 打标识： `<h1 ref="xxx">...</h1>` 或 `<School ref="xxx"/>`
- 获取:`this.$refs.xxx`

## 组件传值

#### props 父传子

```html
<template>                父组件 
    <div>
        <Student name="张三" sex="男" :age="19"/>
    </div>
</template>
<script>
import Student from './components/Student.vue';
export default {
name: 'App',
components: {Student}
}
</script>
```

```html
<template>        子组件
    <div>
        <h2>姓名:{{ name }}</h2>
        <h2>性别:{{ sex }}</h2>
        <h2>年龄:{{ age }}</h2>
    </div>
</template>
<script>
export default {
        name:'Student',
        1.props:['name','sex','age']
        2.props:{
            name: String,
            sex: String,
            age: Number
        }
        3.props:{
            name:{
                type:String,
                required:true
            },
            sex:{
                type:String,
                default: '男'
            },
            age:{
                type:Number,
                required:true
            }
        }
}
</script>
```

`props`可以用于单向数据传递,通常用于父子组件间传值.

props用法: 在父组件中使用子组件的标签上使用键值对的形式向子组件传递数据,在子组件中使用`props`配置通过`key`进行接收. 

props的三种形式

    1. 数组形式只接收数据: `props:['name']`

    2. 对象形式限制类型: `props:{name:Nmber} `

    3. 对象形式 : 

        props:{

            name:{

                type:Number, 类型

                required:true, 必须传

                default: '老王',默认值

             }

           }

**传输数据时默认是字符串的形式,使用`v-bind`指令可以动态传输,`v-bind`可以传递表达式,变量等**

**props是只读的,Vue底层会检测你对props的修改,如果进行修改,就会触发警告,若业务需求需要更改,赋值props中的内容到data中,然后修改data中的数据**

#### 回调函数  子传父

```html
<template> <div> <子组件 :f="fn" /> </div> </template>
<script>
......                        父组件
  methods: {
    function fn(x) {
        console.log(x)
     },
}
</script>
```

```html
<script>                  子组件
export defaule {
        props:['f'],
        methods:{
            function() {
                f(传递的数据)
            }
        }
}
</script>
```

**在父组件中创建一个函数,通过`props`传递给子组件,当传递数据时子组件调用函数,父组件就可以得到数据**

#### $emit 子传父

```html
父组件
<template>
  <div>
    <list
      @add="handleAdd"
      @demo.once="handleDemo"
    />
    <list ref="list" />
  </div>
</template>
<script>
import List from "./components/List.vue";
export default {
components: {List},
    methods: {
        handleAdd(e) {
            console.log('App接收到了name:',e);
        },
        handleDemo() {
            console.log('demo被触发了');
        }
    },
mounted() {
    setTimeout(()=>{ 
        this.$refs.list.$on('add',this.handleAdd);  //绑定自定义事件 
        this.$refs.list.$once('add',this.handleAdd); //绑定自定义事件(一次) 
    },3000)
},
}
</script>
```

```html
<template>     子组件
    <div>    
        <h2>list</h2>    
         <input type="button" value="触发自定义事件" @click="handleClick">          
         <input type="button" value="解绑自定义事件" @click="unbind">
     </div>
</template>
<script>
export default {
name:'TodoList',
    data() {return {name : 'lisi'}},
    methods: {
        handleClick() {
            this.$emit('add',this.name)
            this.$emit('demo')
        },
        unbind() {
            this.$off('add');
            this.$off(['add','demo'])
            this.$off()
         }
    },
}
</script>
```

`$emit`:可以用于子组件与父组件的通信,在父组件中创建自定义事件,在子组件中使用`$emit`就可以触发父组件的自定义事件,同时可以传递数据.

- 创建自定义事件
  
  - 在父组件中 `<Demo @add="test"/>`或`<Demo v-on:add="test">`     
  
  - ```html
    <Demo ref ="demo" />
    ...
    mounted(){ 
    获取到元素的节点,然后添加自定义事件
    this.$emit.xxx.$on( 'add' , this.test)
    }
    ```

- 触发自定义事件: `this.$emit('add',数据)`,可以触发父组件的事件

- 解绑自定义事件:
  
  -  `this.$off('add')`解绑一个
  
  - `this.$off(['add','demo'])`解绑多个
  
  - `this.$off()`解绑所有

#### 全局事件总线`$bus`

全局事件总线:是一种组件间的通信方式,适用于任意组件间的通信.

```js
new Vue({
....        
beforeCreate() {
    Vue.prototype.$bus = this; //安装全局事件总线,$bus就是当前应用的vm
}
})
```

- 监听事件 `this.$bus.$on('xxx',this.fn)`

- 触发事件 `this.$bus.$emit('xxx',data)`

- 解绑事件 `this.$bus.$off('xxx')`

全局事件总线原理:

   **由于`$emit``$on`可以实现组件组件的通信,同时他们又是Vue原型上的方法,因为原型链的机制,项目中所有的组件都属于`Vue`实例的子组件. 此时我们就可以在Vue实例创建但还未创建之前在`beforeCreate()`函数中,在Vue的原型链上添加一个`$bus`属性,且把我们当前的`vue`也就是当前的`this`赋值给他.从此往后无论在任何组件中,我们都可以使用`this.$bus`的形式得到我们实例化后的`vue`,此时就可以的调用`$emit`和`$on`就实现了任意组件间的通信.**

#### pubsub 消息订阅与发布

- 安装pubsub: `npm i pubsub-js`

- 引入: `import pubsub from 'pubsub-js'` 

- 监听/创建: `this.pid = pubsub.subscribe('xxx',this.demo)`

- 触发/传递: `pubsub.publish('xxx',数据)`

- 删除: `pubsub.unsubscribe(this.pid)`

- 接受消息时:在mounted中使用回调需要使用箭头函数,methods中使用普通函数.

- 因为消息订阅会接受到两个参数,第一个参数时消息名,第二个往后是传递的数据,不需要第一个参数是可以使用_(下划线)占位,不用不会报错.

## mixin 混入

`mixin`:把多个组件共用的配置,提取到一起.在用的地方进行导入

- 创建mixin:就是在文件中导出一个对象,这个对象内部的配置与`Vue`的配置语法一致
  
  - ```js
    export const mixin = {
            methods : {
                showName() {
                    alert(this.name)
                  }
            }
    }
    ```

- 局部混入:vue的配置中书写`mixins`配置项,将引入的mixin配置到`minubs`值的数组中 
  
  - ```js
    import {mixin} from '../../mixin';
    export default {
     name:'App',
     data() {return {name:'张三'}}
     mixins:[mixin],
    }```
    ```

- 全局混入 :通过引入的构造函数`Vue`,`Vue.mixin(mixin)`
  
  - ```js
    import Vue from 'vue'
    
    import mixin from '../mixin'
    
    Vue.mixin(mixin)
    ```

##### 优先级

- 组件中的data,methods 优先级高于mixin data,methods的优先级
- 生命周期函数: 先执行mixin里面的在执行,再vue中的
- 自定义属性,组件中的属性优先级高于mixin

##### 修改优先级

```js
app.config.optionMergeStrategies.count = (mixinVal,appValue) => {
return mixinVla || appValue  //先返回mixin在返回vue
}
```

## plugin 插件

创建插件导出

```js
export default {
     install(Vue,options) {
        1.添加全局过滤器
         Vue.filter(...)
         2.添加全局指令
         Vue.directive(...)
         3.配置全局混入
         Vue.mixin(...)
         4.添加实例方法
         Vue.prototype.$myMethod= function(){...}
         Vue.prototype.$myMethod= xxx
    }
}
```

入口中使用插件

```js
...
import plugin from '../plugin'  //引入插件

Vue.use(plugin)

new Vue({
render: h => h(App),
}).$mount('#app')
```

插件本质:包含install方法的一个对象,我们可以通过`install()`方法给vue增加功能更呢个,install的第一个参数是Vue构造函数本身,第二个以后的参数是插件使用者传递的数据.

插件可以让我们增加vue的功能,使用时用`Vue.use(xxx)`即可绑定插件,插件绑定时会自动调用`install()`函数,使用插件必须要`vue`实例创建前使用

## 单文件组件中的style标签

##### scoped属性

`<style scoped> </style>`

scoped属性:给style标签加上此属性后,标签内部的所有样式只对当前组件生效,让样式在局部生效防止冲突.

##### lang属性

lang:可以设置用什么语言书写样式,默认值css

使用less书写时需要安装依赖文件 `npm i less-loader@7`

##### 引入第三方css

- 第一种方式
  
  - 1.在src中创建assets(静态资源)文件夹,然后把第三方css文件推进去
  
  - 2.在用到的组件中使用impotr 'xxx.css' 引入.也可以在main.js中引入,不推荐
    
    在Vue中通过impotr形式引入样式,那么脚手架会做一个非常严格的检查,这个样式所依赖的文件一个都不能少,即便我们没有使用

- 第二种方式
  
  - 1.在public中创建一个文件夹,然后把第三方的包拖进去
  - 2.在html文件中,使用link标签引入
  - 在html文件中引入public中的文件,引入时的路径可以使用 href="<%= BASE_URL %> xxx">
  - 文件路径中的 <%= BASE_URL %> 表示的就是public的跟路径,后面跟下级路径就可以

## Vue过度与动画

### 过度

作用:在插入,更新或移除DOM元素时，在合适的时候给元素添加样式类名。

- 元素进入时样式的类名
  
  | （1.v-venter       | 进入的起点  | name-venter       |
  | ----------------- | ------ | ----------------- |
  | （2.v-enter-active | 进入的过程中 | name-enter-active |
  | （3.v-enter-to     | 进入的终点  | name-enter-to     |

- 元素离开时样式的类名
  
  | （1.v-leave        | 进入的起点  | name-leave        |
  | ----------------- | ------ | ----------------- |
  | （2.v-leave-active | 进入的过程中 | name-leave-active |
  | （3.v-leave-to     | 进入的终点  | name-leave-to     |

- 没有指定name属性,就是用`v-xxx`作为类名,指定了就是用`name-xxx`

使用 `<transition>`包裹需要过渡的元素,并配置name属性

```html
<transition name="hello" appear >
     <h1 v-show="isShow">你好啊</h1>
</transition>
```

多个元素时使用 `<transition-group>`且每个元素都要指定`key`值

```html
<transition-group name="hello" appear >
     <h1 v-show="isShow" :key="key1">你好啊</h1>
     <h1 v-show="!isShow" :key="key2">hello world</h1>
</transition-group>
```

`appear` 属性:加载时是否需要入场动画,值为布尔值,单独书写属性名也能被当做true

- transition中的name属性就是用来替换V的
- transition的enter-active-class用来绑定入场动画的类名
- transition的leave-active-class用来绑定出场动画的类名
- 入场:元素从隐藏到显示 ,出场:元素从显示到隐藏

### animation css 使用

```html
<template>
<div>
<button @click="sum = !sum">点击</button>
<transition
   name="animate__animated animate__bounce"
   enter-active-class="animate__fadeInDownBig"
   leave-active-class="animate__bounceOutLeft"
   appear>
<h1 v-show="sum">List</h1>
</transition>
</div>
</template>
<script>
import 'animate.css';
export default {
data() {
return {
sum :true
}
}
}
</script>
```

- 

- 官网: [https://animate.style/](https://animate.style/)**官网下滑有使用教程**

- 1.通过npm安装: npm install animate.css --save

- 2.导入:在下载成功后 使用 import 'animate.css';导入

- 3-1在普通标签中使用
  
  - <h1 class="animate__animated animate__bounce">An animated element</h1>
  - class里面的animate__animated是Animate依赖的类名,animate__bounce是动画样式的类名
  - 依赖类名和样式类名中间以空格分割

- 3-2.在Vue中使用
  
  - 在transiton标签的name属性:
    - 书写依赖的类名:animate__animated空格后面要带上空格
    - 或依赖和动画都写上:animate__animated animate__bounce因为后面的出场和入场会覆盖掉动画名
    - 动画名的位置可以随意书写,出场入场时都可以被覆盖掉
  - 在transition标签的 enter-active-class 中书写入场的样式的类名 animate__xxx
  - 在transition标签的 leave-active-class 中书写出场的样式的类名 animate__xxx

## Vue中的Ajax

### 常用发送ajax方式

1. xhr: js默认的方式,使用`new XMLHttpRequest()`,原生操作比较麻烦.

2. jQuery: 基于xhr封装的DOM操作ajax的库，在Vue中不适用.

3. axios:基于xhr封装且具有promise风格的第三方库,不用操作DOM，Vue作者推荐的在vue用使用ajax的方式.

4. fetch:fetch在window的内置对象上，他与xhr平级,当我们无法使用xhr或者基于xhr的库时，可以使用fetch.

5. Vue-resource: Vue-resource是一个vue1.0时常用的Vue插件库,与axios同样具有promise风格，操作方式页几乎一致.

### 在Vue中跨域

在Vue中解决跨域,通常使用`Vue-cli`配置代理服务器的方式来实现跨域.

**代理:**

- 使用代理:不使用本地文件,优先发送请求

- 不使用代理:如果根路径下有同名文件优先使用本地
1. 在`vue.config.js`中进行配置,如果没有则创建该文件,与`package.json`是同级的,这个文件应该导出一个包含了选项的对象. [vue.config.js](https://cli.vuejs.org/zh/config/#vue-config-js)

2. 通过`devServer.prox`配置项配置代理服务器
   
   1. 配置单个代理服务器
      
      ```js
      module.exports = {
        devServer: {
          proxy: 'http://localhost:4000'
        }
      }
      ```
      
      proxy:的值用于指定在哪个服务器获取数据
      
      简写形式缺点:无法配置多个代理,无法灵活控制是否走代理,
      
      工作方式:按照上述配置代理,当请求了前端不存在的资源时,那么该请求会转发给服务器(优先匹配前端资源,也就是本地)  
   
   2. 完整配置代理服务器
      
      ```js
      module.exports = {
        devServer: {
          proxy: {
             '/api': { //匹配所有以'/api'开头的请求路径
                  target: 'http://localhost:5000', //代理目标的基础路径
                  pathRewrite:{'^/api':''}, //删除请求中的前缀
                  ws: true,
                  changeOrigin: true
               },
               '/demo': { //匹配所有以'/demo'开头的请求路径
                   target: 'http://localhost:5001',
                   pathRewrite:{'^/demo':''},
                   ws: true,
                   changeOrigin: true
               },
               '/foo': {
                   target: '<other_url>'
               }'
            }
          }
         }
      }
      ```
      
      proxy里面的`'/api'`:是请求的前缀,本次请求有前缀,那么就是走代理反之不走,请求的前缀可以任意命名.
      
      target:需要代理的服务器地址
      
      pathRewrite用于删除使用代理时的前缀,值为一个对象,然后匹配正则表达式,将前缀设置为空
      
      ws(websocket):用于支持websocket true默认值
      
      changeOrigin: 用于控制请求头中host的值,false:默认的端口号, true(默认值):与目标(也就是给发送请求的服务器)的端口号一致,防止目标服务器对跨域做了限制,从而得不到数据

    

配置代理服务器后,代理服务器所在的端口就是我们项目所运行的端口,如果需要在目标服务器请求数据,需要向我们当前所在的端口进行请求,请求的路径不变,就是请求的端口由目标服务器的端口号变成了本地代理的端口号

### Axios

- axios:是一款对xhr封装的promise风格的第三方ajax库,可以使用promise的方法

- axios支持请求拦截器,和响应拦截器,

- 在Vue中因为vue本身不是操作DOM，所以推荐使用具有promise风格的axios
1. 下载`axios`: `npm install axios --save`.

2. 引入`axios`: `import axios from 'axios'`.

3. 使用 
   
   1. get: `axios.get('URL').then(response=>{},error=>{})`.
   
   2. post: 

```html
<template>
     <button @click="getStudents">获取学生信息</button>
</template>
<script>
     import axios from 'axios'
     export default {
         name: 'App',
         methods:{
             getStudents() {
                 axios.get('http://localhost:8080/students').then(
                 response => {
                     console.log('请求成功',response.data);
                 },
                 error => {
                     console.log('请求失败',error.message);
                   })
              }
         }
     }
</script>
```

使用了代理服务器后,只需要向当前项目所在端口发送请求,代理服务器就会自动识别并且向数据所在服务器,请求数据.请求的路径不变

### Vue-resource

- Vue-resource:也是一个用于ajax请求的vue的一个插件库,使用时使用Vue.use(xxx)给vm绑定插件
- Vue-resource与axios几乎一致,也是promise风格,但是只是在vue1.0的时候用的多,如今不推荐使用

安装:`npm i vue-resource`

引入

```
import vueResource from 'vue-resource'
Vue.use(vueResource)
```

使用: `this.$html.get(url).then(response=>{},error=>{})`

## slot 插槽

作用:让父组件可以向子组件指定位置插入html结构,也是一种组件间通信的方式,适用于父组件==>子组件

##### 默认插槽

```html
父组件

                 <Category>
                   <div>html结构1</div>
                 </Category>


子组件

                 <template>
                     <div>
                       <slot>Category组件插槽默认值</slot>
                     </div>
                 </template>
```

##### 具名插槽

```html
父组件
          <Category>
            <template slot="header">
                <div>html结构1</div>
            </template>

            <template v-slot="footer">
                <div">html结构2-1</div>
                <div">html结构2-2</div>
            </template>
          </Category>

          <Category>
                <div slot="header>html结构1</div>
                <div slot="footer>html结构2-1</div>
                <div slot="footer>html结构2-2</div>
          </Category>
子组件

    <template>
        <div>
          <slot name="header">Category组件header默认值</slot>
          <div>Category组件body</div>
          <slot name="footer">Category组件footer默认值</slot>
        </div>
    </template>
```

##### 作用域插槽

- 1.理解:数据在组件自身,但根据数据生成的结构需要组件的使用者(父级)来决定

```html
父组件

    <template>
        <div class="container">
          <Category>
            <template scope="data">
              <div>{{data.name}}</div>
              <div>{{data.title}}</div>
            </template>
          </Category>

          <Category>
             <template scope="{name,title}">
              <div>{{name}}</div>
              <div>{{title}}</div>
            </template>
          </Category>

          <Category>
             <template slot-scope="{name,title}">
              <div>{{name}}</div>
              <div>{{title}}</div>
            </template>
          </Category>
        </div>
    </template>

子组件

    <template>
      <div>
        <slot name="lijinsheng" title="hello">Category组件footer默认值</slot>
      </div>
    </template>
```

## Vuex

vuex是什么:专门在Vue中实现集中式状态(数据管理的一个Vue插件,对vue应用中多个组件的共享状态进行集中式的管理(读/写),也是一种组件间通信的方式,且适用于任意组件间的通信.

在2022年2月7日,vue3成为了默认版本,vuex也就更新到了4版本,`npm i vuex`会是最新版

在Vue中,Vue2要用Vuex的第三版本,Vue3使用Vuex的第四版本,安装版本只需要在命令后加上`@版本号`即可

1. 安装vuex: `npm i vuex@3`

2. 在`src`目录下创建一个`store`目录用于配置Vuex,在目录下创建 js文件

```js
//该文件用于创建Vuex中最为核心的store
import Vue from "vue";
import Vuex from "vuex"

Vue.use(Vuex)

export default new Vuex.Store({
    state: { //  准备state用于存储数据
    },

    mutations: { // 准备mutations用于操作数据(state)
    },

    actions: { // 准备actions,用于响应组建里面的动作
    },
})      
```

创建`store`前需要将`Vuex`引入并通过插件的形式绑定到Vue上,然后通过`new Vuex.Store({})`的形式创建仓库并导出,仓库中包含`state`,`mutations`,`actions`等配置项.

引入

```js
.....
import store from './store/index' // 引入store
.....

new Vue({
  render: h => h(App),
  store,
}).$mount('#app')
```

##### vuex基本使用

当Vuex与Vue实例vm绑定后,Vue实例就可以使用store配置项了与data平级,在控制台中打印vm或vc时都会多出来一个`$store`,我们通过这个`$store`就可以进行`Vuex`的操作.

Vuex中常用的三个配置对象

- `state`:用于存放数据

- mutations: 用于直接操作`state`中的数据,但是不能存在异步操作.以触发的响应名大写为函数,函数第一个参数是`state`对象,

- `actions`: 可以用于异步操作,发送请求等,主要是书写各种逻辑,逻辑过于复杂还可以在action的方法中继续调用dispatch,然后通过`mutations`进行操作数据.

若没有复杂的业务需求,如延时,ajax请求等,可以跳过 `dispatch`,直接在组件中`commit`,使用mutations修改state的数据

```js
export default new Vuex.Store({

     state : { //  准备state用于存储数据
       sum: 0,
    }

     mutations : { // 准备mutations用于操作数据(state)
        ADD(state,value) {
            state.sum += val sum: 0,
    }

     actions : { // 准备actions,用于响应组建里面的动作
        add(context,value) {
            context.commit('ADD',value)
        }
    },
})
```

组件中读取Vuex数据:`this.$store.state.sum`/`$store.state.sum`.

触发事件

`this.$store.dispatch('action中的方法名',数据)` dispatch可以对接action对象.

`this.$store.commit('mutations中的方法名',数据)`commit可以对接mutations对象.

action中以dispatch触发的事件为函数名,mutations中以commit触发的事件为函数名,mutations中函数名建议以action中函数名的大写的形式.

actions中函数的第一个参数可以接收一个与store实例具有相同方法的属性context,后面的参数是用户传递的.

context:{
        state,   等同于`store.$state`，若在模块中则为局部状态
       `rootState`,等同于`store.$state`,只存在模块中
        commit,   等同于`store.$commit`
        dispatch, 等同于`store.$dispatch`
        getters   等同于`store.$getters`
}

mutations中函数的第一个参数是`state`,后面的参数是`action`传递过来的

    

#### gettrs配置项

gettrs:当state中的数据需要加工后在使用时,可以使用getters加工,state与gettres 就类似组件中的data与computed,geters就是一个所有组件都可以访问的计算属性

```js
export default new Vuex.Store({

     state : { //  准备state用于存储数据
       sum: 0,
    }
    ....
    gettrs:{
        bigSum(state) {
            return state.sum * 10
        }
    }
})
```

gettrs中的函数的参数就是state对象,可以直接获取到state中的数据.

在组件中读取gettrs:`this.$store.getters.bigSum`

#### map方法

##### mapState

```js
....
import {mapState} from 'vuex'
....
computed:{
    //借助mapState生成计算属性:sum、name、subJect(对象写法)
    ...mapState({sum:'sum',name:'name',subJect:'subJect'})

    //借助mapstate生成计算属性:sum、name、subJect(数组写法)
    ...mapState(['sum','name','subJect'])
},
```

 mapState可以帮助我们映射`state`中的数据为计算属性.

- 对象形式key是计算属性的name,value是在state中的属性,value需要使用引号包裹.
- 数组形式,计算属性名和state中的一致,直接用引号包裹写在数组中

##### mapGetters

```js
  ....
    import {mapGetters} from 'vuex'
    ....
    computed{   
        //借助mapGetters生成计算属性:bigSum(对象写法)
        ...mapGetters({bigSum:'bigSum'}),

        //借助mapGetters生成计算属性:bigSum(数组写法)
        ...mapGetters(['bigSum']),

    },
```

`mapGetters`用于帮助我们映射 `getters`中的数据为计算属性,语法与`mapState`一致.

##### mapActions

```js
   ...
    import {mapActions} from 'vuex'
    ...

    methods:{
        //靠mapActions生成:incrementOdd、incrementWait(对象形式)
        ...mapActions({incrementOdd:'jiaOdd',decrementWtait:'jiaWait'}),

        //靠mapActions生成:incrementOdd、incrementWait(对象形式)
        ...mapActions(['jiaOdd','jiaWait']),

    }
```

用于帮助我们生成 `actions`对话的方法,即:包含`$store.dispatch('xxx')的函数`

##### mapMutations

```js
    ...
    import {mapMutations} from 'vuex'
    ...

    methods:{
        //靠mapMutations生成:increment、decrement(对象形式)
        ...mapMutations({increment:'JIA',decrement:'JIAN'}),

        //靠mapMutations生成:increment、decrement(数组形式)
        ...mapMutations({['JIA','JIAN']),
    }
```

- 用于帮助我们生成 `mutations`对话的方法,即:包含`$store.commit('xxx')的函数`

- **mapActions与mapMutations使用时,若需要传递参数,需要在模板中绑定事件时传递好参数,否则参数是事件对象**

#### 命名空间+Vuex模块化

```js
const countAbout = {
        namespaced:true,  //开启命名空间
        state:{x:1},
        mutations:{...},
        actions:{...},
        getters:{
            bigSum(state){
                return state.sum * 10
            }
        }
    }

    const personAbout = {
        namespaced:true,  //开启命名空间
        state:{...},
        mutations:{...},
        actions:{...},
    }

    const store = new Vuex.Store({
        modules:{
            countAbout,
            personAbout
        }
    })
```

开启命名空间和模块化后,可以让代码更好管理,让多种数据分类更加明确.

new仓库时直接传递一个modules配置对象,然后再modules配置对象中传入开启了命名空间`namespaced:true`的store配置对象.

开启命名空间后读取state

```js
    //方式一: 自己直接读取
    this.$store.state.countAbout.sum
    //方式二: 借助mapState读取
    ...mapState('countAbout',['sum','school','list'])
```

普通形式需要加上名再打点

使用map需要把命名空间名先配置进去

开启命名空间后读取getters

```js
 //方式一: 自己直接读取
    this.$store.getters['countAbout/bigSum']
    //方式二: 借助mapState读取
    ...mapGetters('countAbout',['bigSum'])
```

开启命名空间后,组件中调用`dispatch`

```js
  //方式一: 自己直接dispatch
    this.$store..dispatch('personAbout/addPersonWang',data)
    //方式二: 借助mapActions
    ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrmentWait:'jiaWait'})
```

开启命名空间后,组件中调用`commit`

```js
    //方式一: 自己直接comit
    this.$store.commit('personAbout/ADD_PEREON',data)
    //方式二: 借助mapActions
    ...mapActions('personAbout',{increment:'JIA',decrment:'JIAN'})
```

## Vue-router路由

vue-router:是Vue的一个插件库,专门用来实现spa单页面应用.

- #### SPA应用
  
  - 1.单页Web应用（single page web application，SPA）
  - 2.整个应用只有一个完整的界面
  - 3.点击页面中的导航链接不会刷新页面，只会做页面的局部更新。
  - 4.数据需要通过ajax请求获取
  
  #### 什么是路由
  
  - 1一个路由就是一组映射关系(key- value)
  - 2.key为路径,value可能是function或component

- #### 路由分类
  
  - 1.后端路由
    - (1).理解:value是function,用于处理客户端提交的请求
    - (2).工作过程:服务器接收到一个请求时,根据请求路径找到匹配的函数来处理请求,返回响应数据
  - 2.前端路由:
    - (1) 理解:value是component,用于展示页面内容
    - (2).工作过程:当浏览器的路径改变时,对应的组件就会显示

### 路由使用

- 2022年2月7日后,vue-router的默认版本,为4版本,vue-router4只能在Vue3中使用,vue-router3 才能在Vue2中使用
1. 安装vue-router: `npm i vue-router`,`npm i vue-router@3`

2. 编写路由配置项: src目录下创建router目录 ,router目录中创建js文件配置
   
   ```js
   src/router/index.js
   
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   // 创建router实例对象,去管理一组一组的路由规则
   const router =  new VueRouter({
       routes:[
           {
               path:'/about',
               component:About
           },
           {
               path:'/home',
               component:Home
           }
       ]
   })
   //导出router
   export default router
   ```

3. 应用
   
   ```js
   main.js
   ....
   // 引入Vue-router
   import VueRouter from 'vue-router'
   // 引入路由配置
   import router from './router/index.js'
   ....
   //绑定路由
   Vue.use(VueRouter)
   
   new Vue({
     el:'#app',
     render: h => h(App),
     router,  //导入router配置项
   })
   ```

4. 路由切换:

    `<router-link class="list-group-item" active-class="active" to="/about">About</router-link>`

5. 路由展示  `<router-view></router-view>`
