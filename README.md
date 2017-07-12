# 互通前端技术文档
*撰写者：==小九==；时间：==2017年7月11日==*

==前言：技术盏选定将决定不再支持IE9及IE9以下版本浏览器==

- **技术路线流程图**


```
graph TD
A[WebStorm]-->B{webpack}
B --> Ba[HTML5]
B --> Bb{Sass}
B --> Bc[React-Dom]
B --> Bd[React-Router]
B --> Be[React-Redux]
B --> Bf[ECMAScript6]
B --> Bg{Images}
B --> Bh{files}

Ba--> Baa[htmlWebpackPlugin]

Bb --> Bba[sass/postcss/css/style-loader]

Bc --> Bca[bable-loader/ES2015/React]
Bd --> Bca[bable-loader/ES2015/React]
Be --> Bca[bable-loader/ES2015/React]
Bf --> Bca[bable-loader/ES2015/React]

Bg --> Bga[image-webpack/image/url-loader]

Bh --> Bha[file-loader]

Baa --> Baaa[HTML5/HTML4]

Bba --> Bbaa[bundle.js]
Bca --> Bbaa[bundle.js]
Bga --> Bgaa[Base64/min-Image]
Bha --> Bhaa[eto/ttf/svg/woff]

Baaa -->C[PTOJECT]
Bbaa -->C[PTOJECT]
Bgaa -->C[PTOJECT]
Bhaa -->C[PTOJECT]
```
## WEBSTORM
*[WebStorm](http://www.jetbrains.com/webstorm/)WebStorm 是jetbrains公司旗下一款JavaScript开发工具。目前已经被广大中国JS开发者誉为“Web前端开发神器”、“最强大的HTML5编辑器”、“最智能的JavaScript IDE”等。与IntelliJ IDEA同源，继承了IntelliJ IDEA强大的JS部分的功能。*

    优点 | 缺点
    ---|---
    对前端业界内最新技术代码支持 | 运行内存大，常驻内存300M左右
    可自定义代码格式化规则 | 启动一个项目所需的时间与项目大小相关
    自配内置服务器以及终端 | 体积偏重

==以上只提及此编辑器的部分，工具请按个人喜好搭配，顺手即可==



## WEBPACK
*[Webpack](https://webpack.js.org/) 是一个前端资源加载/打包工具。它将根据模块的依赖关系进行静态分析，然后将这些模块按照指定的规则生成对应的静态资源。在webpack的思想中，它把每一个文件都当成是一个组件。*
> 下面附上webpack的整体工作流程
![image](http://www.runoob.com/wp-content/uploads/2017/01/what-is-webpack.png)

-  webpack的优势：
   - 模块化，让我们可以把复杂的程序细化为小的文件;
   - 代码拆分（code splitting）方案;
   - 智能的静态分析;
   - 模块热替换（Hot Module Replacement）[亮点];
   - 支持commejs规范和AMD规范等;
   - 通过NPM支持很多插件和loader;
   - ...
-  webpack的劣势：
   - 开始搭建项目时候，需要配置较多的参数;
   - 随着项目复杂度的增加，编译时长也会不断增加;


## React：
*[React](https://facebook.github.io/react/) 是一个用于构建用户界面的 JavaScript 库，主要用于构建UI，属于MVC中的V层，它起源于 Facebook 的内部项目，由Facebook团队维护，项目目前在Github上已经拥有了7w+的 [star](https://github.com/facebook/react)，社区也是前端中最为活跃的，已经超过曾经的angular.js*

==~~我觉得react没什么不同嘛~~==，不然！

- **Virtual DOM 虚拟DOM**

    *传统的web应用，操作DOM一般是直接更新操作的，但是我们知道DOM更新通常是比较昂贵的。而React为了尽可能减少对DOM的操作，提供了一种不同的而又强大的方式来更新DOM，代替直接的DOM操作。就是Virtual DOM,一个轻量级的虚拟的DOM，就是React抽象出来的一个对象，描述dom应该什么样子的，应该如何呈现。通过这个Virtual DOM去更新真实的DOM，由这个Virtual DOM管理真实DOM的更新。*

    *为什么通过这多一层的VirtualDOM操作就能更快呢？这是因为React有个diff算法，更新Virtual DOM并不保证马上影响真实的DOM，React会等到事件循环结束，然后利用这个diff算法，通过当前新的dom表述与之前的作比较，计算出最小的步骤更新真实的DOM。*
```
graph LR
A-->|diff|B[Real DOM]
B-->|diff|A[Virtual DOM]
```
- **Components 组件**

    *在DOM树上的节点被称为元素，在这里则不同，Virtual DOM上称为commponent。Virtual DOM的节点就是一个完整抽象的组件，它是由commponents组成。*

    > component 的使用在 React 里极为重要, 因为 components 的存在让计算 DOM diff 更高效。

    ```
    //react创建组件
    import React, { Component } from 'react';
    class Hello extends Component {
        render() {
            return (
                <div>Hello World!</div>
            );
        }
    }
    export default Hello;
    ```

- **Virtual DOM 虚拟DOM**

    *React是如何呈现真实的DOM，如何渲染组件，什么时候渲染，怎么同步更新的，这就需要简单了解下State和Render了。state属性包含定义组件所需要的一些数据，当数据发生变化时，将会调用Render重现渲染，这里只能通过提供的setState方法更新数据。*

- **JSX语法：**

    ```
    const element = <h1>Hello, world!</h1>; //JSX语法
    ```

    *JSX是一种JavaScript语法扩展，（==如上代码==）在React中可以方便地用来描述UI，JSX是一种语法糖，粗看上去，像是在Javascript代码里直接写起了XML标签，实质上这只是一个语法糖，每一个XML标签都会被JSX转换工具转换成纯Javascript代码，当然你想直接使用纯Javascript代码写也是可以的，只是利用JSX，组件的结构和组件之间的关系看上去更加清晰。*

    ++下面附上官方提供的hello world++
    ```
    <div id="example"></div>
    <script type="text/babel">
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
    ```
    ==JSX语法可自动防范注入攻击，在默认情况下，React DOM会将所有嵌入JSX的值进行编码。这样可以有效避免xss攻击。==
- **React的生命周期**

    ![image](https://github.com/Clownzoo/htong/blob/master/mardownImg/live.png?raw=true)

    ### Mounting

    *当创建一个组件的实例并插入到DOM中时，调用这些方法：*
    - constructor()
    - componentWillMount()
    - render()
    - componentDidMount()

    ### Updating

    *更新可能是由于 props 或 state 的改变引起的。当组件重新呈现时调用这些方法：*
    - componentWillReceiveProps()
    - shouldComponentUpdate()
    - componentWillUpdate()
    - render()
    - componentDidUpdate()

    ### Unmounting

    *当从DOM中移除组件时调用此方法：*
    - componentWillUnmount()
## React-Router：
*[React-Router](https://github.com/ReactTraining/react-router) 是完整的 React 路由解决方案，保持 UI 与 URL 同步。它拥有简单的 API 与强大的功能例如代码缓冲加载、动态路由匹配、以及建立正确的位置过渡处理。*
- #### 什么是路由？

    *假如我们有一台提供 Web 服务的服务器的网络地址是：10.0.0.1，而该 Web 服务又提供了三个可供用户访问的页面，其页面 URI 分别是：*

    ```
    http://10.0.0.1/
    http://10.0.0.1/pageOne
    http://10.0.0.1/pageTwo
    ```

    *那么其路径就分别是 /，/about，/concat。*

    *当用户使用 http://10.0.0.1/about 来访问该页面时，Web 服务会接收到这个请求，然后会解析 URI 中的路径 /about，在 Web 服务的程序中，该路径对应着相应的处理逻辑，程序会把请求交给路径所对应的处理逻辑，这样就完成了一次「路由分发」，这个分发就是通过「路由」来完成的。*

- #### 什么是路由？

    *前端的路由和后端的路由在实现技术上不一样，但是原理都是一样的。在 HTML5 的 history API 出现之前，前端的路由都是通过 hash 来实现的，hash 能兼容低版本的浏览器。如果我们把上面例子中提到的 3 个页面用 hash 来实现的话，它的 URI 规则中需要带上 #。*

    ```
    http://10.0.0.1/
    http://10.0.0.1/#/about
    http://10.0.0.1/#/concat
    ```

    *Web 服务并不会解析 hash，也就是说 # 后的内容 Web 服务都会自动忽略，但是 JavaScript 是可以通过window.location.hash 读取到的，读取到路径加以解析之后就可以响应不同路径的逻辑处理。*

    *history 是 html5 才有的新 API，可以用来操作浏览器的 session history (会话历史)。基于 history 来实现的路由可以和最初的例子中提到的路径规则一样。*

    ```
    http://10.0.0.1/
    http://10.0.0.1/about
    http://10.0.0.1/concat
    ```

    *用户可能都察觉不到该访问地址是 Web 服务实现的路由还是前端实现的路由。
从性能和用户体验的层面来比较的话，后端路由每次访问一个新页面的时候都要向服务器发送请求，然后服务器再响应请求，这个过程肯定会有延迟。而前端路由在访问一个新页面的时候仅仅是变换了一下路径而已，没有了网络延迟，对于用户体验来说会有相当大的提升。*
## Redux：

*[Redux](https://github.com/reactjs/redux) 是 JavaScript 状态容器，提供可预测化的状态管理。它可以让你构建一致化的应用，运行于不同的环境（客户端、服务器、原生应用），并且易于测试。Redux 除了和 React 一起用外，还支持其它界面库。它体小精悍（只有==2kB==）且没有任何依赖。*

- #### 存在动机
    *随着 JavaScript 单页应用开发日趋复杂，JavaScript 需要管理比任何时候都要多的 state （状态）。 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等。*

    *管理不断变化的 state 非常困难。如果一个 model 的变化会引起另一个 model 变化，那么当 view 变化时，就可能引起对应 model 以及另一个 model 的变化，依次地，可能会引起另一个 view 的变化。直至你搞不清楚到底发生了什么。state 在什么时候，由于什么原因，如何变化已然不受控制。 当系统变得错综复杂的时候，想重现问题或者添加新功能就会变得举步维艰。*
- #### 核心概念
    ![image](https://github.com/Clownzoo/htong/blob/master/mardownImg/redux.png?raw=true)
    当使用普通对象来描述应用的 state 时。例如，todo 应用的 state 可能长这样：

    ```
    {
      todos: [{
        text: 'Eat food',
        completed: true
      }, {
        text: 'Exercise',
        completed: false
      }],
      visibilityFilter: 'SHOW_COMPLETED'
    }
    ```
    这个对象就像 “Model”，区别是它并没有 setter（修改器方法）。因此其它的代码不能随意修复它，造成难以复现的 bug。

    要想更新 state 中的数据，你需要发起一个 action。Action 就是一个普通 JavaScript 对象（注意到没，这儿没有任何魔法？）用来描述发生了什么。下面是一些 action 的示例：

    ```
    { type: 'ADD_TODO', text: 'Go to swimming pool' }
    { type: 'TOGGLE_TODO', index: 1 }
    { type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }
    ```
    强制使用 action 来描述所有变化带来的好处是可以清晰地知道应用中到底发生了什么。如果一些东西改变了，就可以知道为什么变。action 就像是描述发生了什么的面包屑。最终，为了把 action 和 state 串起来，开发一些函数，这就是 reducer。再次地，没有任何魔法，reducer 只是一个接收 state 和 action，并返回新的 state 的函数。 对于大的应用来说，可能很难开发这样的函数，所以我们编写很多小函数来分别管理 state 的一部分：

    ```
    function visibilityFilter(state = 'SHOW_ALL', action) {
      if (action.type === 'SET_VISIBILITY_FILTER') {
        return action.filter;
      } else {
        return state;
      }
    }

    function todos(state = [], action) {
      switch (action.type) {
      case 'ADD_TODO':
        return state.concat([{ text: action.text, completed: false }]);
      case 'TOGGLE_TODO':
        return state.map((todo, index) =>
          action.index === index ?
            { text: todo.text, completed: !todo.completed } :
            todo
       )
      default:
        return state;
      }
    }
    ```
    再开发一个 reducer 调用这两个 reducer，进而来管理整个应用的 state：

    ```
    function todoApp(state = {}, action) {
      return {
        todos: todos(state.todos, action),
        visibilityFilter: visibilityFilter(state.visibilityFilter, action)
      };
    }
    ```
- #### 三大原则
    - **单一数据源**：*整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。*
    - **State 是只读的**：*唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。*
    - **使用纯函数来执行修改**：*为了描述 action 如何改变 state tree ，你需要编写 reducers。*