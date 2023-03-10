# React

## react 介绍

用于动态构建用户界面的javascript库(只关注于视图)



## react的特点

1. 声明式编码

2. 组件化编码

3. React Native编写原生应用

4. 高效(优秀的Diffing算法),使用虚拟DOM,不总是直接操作页面真实DOM,DOM Diffing算法,最小化页面重绘



## react初使用

```html
<body>
    <div id="root"></div>

    <script src="../js/react.development.js"></script>
    <script src="../js/react-dom.development.js"></script>
    <script src="../js/babel.min.js"></script>

    <script type="text/babel">
       const VDOM = <h1>Hello World </h1>
   
       ReactDOM.render(VDOM, document.getElementById('root'))
    </script>
</body>
```

1. 准备好React依赖包
   
   1. `react.development.js`  React的核心库 第一个引入,引入增加`React`全局对象
   
   2. `react-dom.development.js`ReactDOM核心库后引入,引入增加`ReactDOM`全局对象
   
   3.  `babel.min.js`                babel包,用于将React中的`JSX`转换成`JS`

2. 在html文件中 创建一个容器 ,并将React需要的js依次引入.

3. 创建一个`script`标签,并将其type属性设置为`type="text/babel"`.

4. 使用`JSX`语法创建虚拟`DOM`

5. 使用`ReactDOM`的`render()`函数将虚拟DOM绑定到 html的容器上.

render()函数式覆盖模式,多个render()函数同时存在,后面的覆盖前面的



## 虚拟DOM的两种创建方式

### 使用JSX创建虚拟DOM(常用)

  上面的示例就是使用JSX创建的虚拟DOM,使用JSX创建的虚拟DOM,经过babel转换后,就是使用createElement()的方式创建的节点




### 使用JS创建虚拟DOM(不常用)

```html
<body>
    <div id="root">

    </div>
    <script src="../js/react.development.js"></script>
    <script src="../js/react-dom.development.js"></script>

    <script type="text/javascript">
       const VDOM = React.createElement('h1',{id:'count'},'hello world')
    
       ReactDOM.render(VDOM, document.getElementById('root'))
       
    </script>
</body>
```

`React.createElement(标签名,标签属性对象,标签内容)`

React具有一个`createElement`方法,与document的一样可以进行创建DOM节点,如果使用createElement方法进行创建节点,则不需要用到babel编译,script标签对的type也需要修改成正常的javascript.

`createElement()`方法也有缺点,就是无法进行多层标签的嵌套



## 虚拟DOM与真实DOM

1. 虚拟DOM本质是一个Object类型的对象(一般对象)

2. 虚拟DOM比较小,真实DOM比较大,因为虚拟DOM是React内部在用,无需真实DOM那么多的属性

3. 虚拟DOM最终会被React转化为真实DOM呈现在页面上



## JSX

1. 全称: javascript XML

2. react定义的一种类似 XML的JS扩展语法: JS + XML
   
   - XMl 早期用于存储和传输数据,后来使用json格式
     
     ```xml
     <student>
         <name>Tom</name>
         <age>18</age>
     </student>
     ```

3. 本质是`React.createElement()`的语法糖

4. 作用: 用来简化创建虚拟DOM
   
   1)      写法：`var ele = <h1>Hello JSX!</h1>`
   
   2)      注意1：它不是字符串, 也不是HTML/XML标签
   
   3)      注意2：它最终产生的就是一个JS对象

5. 标签名任意: HTML标签或其它标签

6. 标签属性任意: HTML标签属性或其它

7. 基本语法规则
   
   - 遇到 <开头的代码, 以标签的语法解析: html同名标签转换为html同名元素, 其它标签需要特别解析
   
   - 遇到以 { 开头的代码，以JS语法解析: 标签中的js表达式必须用{ }包含  

8. babel.js的作用
   
   1. 浏览器不能直接解析JSX代码, 需要babel转译为纯JS的代码才能运行
   
   2. 只要用了JSX，都要加上type="text/babel", 声明需要babel来处理



### JSX语法规则

```html
   <script type="text/babel">
        const data = 'hello world'
       const VDOM = (
        <div>
            <h1 style={{color:'red',fontSize: '50px'}}> {data}</h1>
            <label htmlFor="text">清输入</label> 
            <input className="class" id="text"/>
        </div>
       )
       ReactDOM.render(VDOM, document.getElementById('root'))
    </script>
```

1. 定义虚拟DOM时不要加引号

2. 标签中混入js表达式时需要用{},花括号中只能写js表达式,不能写js语句

3. 样式的类名不使用class而是使用`classname`

4. label标签中的for属性 改变为 `htmlfor`

5. 内联样式要使用:`style={{key:value}}`的形式书写,多个单词时使用驼峰命名的方式

6. 只允许有一个根标签

7. 标签必须闭合

8. 标签首字母
   
   1. 若小写字母开头,则将标签转化为html中同名元素,若html中无改标签对应的同名元素,则报错
   
   2. 若大写字母开头,react就会去渲染对应的组件,若组件没有定义则报错



### 遍历

```jsx

```



react中无法直接遍历 需要借助js中的方法才可以,而且在jsx语法中无法使用 js语句形似的for循环,需要使用遍历的方法: map()等,每次循环的标签必须具有一个key的属性,且值需要时唯一的.




