## 2 组件

> *此处可能要先回顾一下之前的hello world例子*

&emsp;&emsp;组件（Component）是构成 Angular2 应用的基础和核心，了解它是如何工作是非常重要的，因此本书也将组件介绍在最前面。

### 2.1 什么是组件

&emsp;&emsp;组件是编写应用的基本单元，通俗地说，一个组件包装了一个特定的功能，并且组件之间协同工作以组装成一个完整的应用程序。

&emsp;&emsp;举个现实中的例子，一辆汽车中包含各种各样的部件、零件，比如发动机、变速箱、轮胎等等，那么这些便可以理解为组成汽车的`组件`，当然这还不是最小粒度的组件，例如发动机本身也会由众多小零件组合而成。

&emsp;&emsp;那么作为 Web 应用开发者，怎么去理解组件呢？相信读者都应该用过或者知道jQueryUI、Bootstrap、YUI等一些经典的UI库，即使不知道也没关系，你肯定写过 html、css 和js。在 Web 开发中，组件一般是指有着独立的UI界面，并且提供相应的方法，以完成一系列的界面渲染和特定功能交互的代码集合。

&emsp;&emsp;以使用 jQueryUI 实现一个 Dialog 组件为例：

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/jquery-dialog-hello-world.png)

&emsp;&emsp;图 2-1 jquery 对话框组件

&emsp;&emsp;jQueryUI 的 Dialog 组件代码（部分）：

```javascript
var dialog = $.widget( "ui.dialog", {
    options: {},
    open: function () {},
    close: function () {},
    isOpen: function () {},
    widget: { return this.uiDialog; },
    moveToTop: function () {}
}
```

&emsp;&emsp;使用 jQueryUI 实现的一个 HelloWorld 对话框组件代码：

```html
<!doctype html>
<html lang="en">
<head>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.11.4/jquery-ui.js"></script>
  <script>
  // 组件代码 javascript 部分 start
  $(function() {
    $( "#dialog-" ).dialog({
      height:140,
      buttons: {
        OK: function() {
          $( this ).dialog( "close" );
        },
        Cancel: function() {
          $( this ).dialog( "close" );
        }
      }
    });
  });
  // 组件代码 javascript 部分 end
  </script>
</head>
<body>
<!-- 组件代码 html 部分 start -->
<div id="dialog" title="Dialog">
  <p>Hello World!</p>
</div>
<!-- 组件代码 html 部分 end -->
</body>
</html>
```

&emsp;&emsp;以上代码可以这样理解：

- 首先`$.widget( "ui.dialog" ...`这段代码，表示的是，ui.dialog 是一个基础的对话框组件，它是属于 jQueryUI 库的组件。这个组件提供了对话框的配置、打开、关闭等属性和方法。
- 接下来的 html 中的代码段，便是使用 jQueryUI 的开发者，实现了一个“hello world 对话框应用。而这个应用中（仅）包含了一个 hello world 对话框的组件（见上面注释中的`组件代码`部分）。它渲染了一个 id 为 dialog 的 div，显示了标题、内容，并提供了“OK”和“Cancel”两个按钮给用户操作。

### 2.2 组件化的发展

&emsp;&emsp;前面的内容已经对组件有了初步的了解，下面来了解组件的概念是如何产生的，组件化又是如何发展的。

#### 2.2.1 模块化
&emsp;&emsp;谈到组件化，先要了解`模块化`。在 node.js 中，模块就是一个文件，引入一个文件就是简单地`require('xxx')`。在前端的领域，也衍生出不少模块化的规范，比如 AMD、CMD，不过前端领域发展得很快，因为还未形成一种统一的规范，目前（本书写作的时候）无论是AMD还是CMD都已经过时了，新兴的 ES6、TypeScript 均采用了类似 node 的 import module 的方式，配合 browserify、webpack 等构建工具将所有模块转换、打包成一个可用于浏览器运行的 js 文件。

> node.js 采用的是 CommonJS 规范。AMD 全称是 Asynchromous Module Definition，CMD 全称是 Common Module Definition，著名的 RequireJS、SeasJS 分别是 AMD、CMD 规范的实现之一。


&emsp;&emsp;不过在早期的模块化，只是针对 js 部分做了处理，比如 AMD、CMD 的其中一个实现RequireJS、SeasJS 也只是管理 js 模块。后来的火起来的 Angular1.x，vue.js 都建议将同属一个功能的 js、css、html 放到一个目录下去管理，当这些具有关联功能的文件组织在一起后，便形成了“组件”的雏形。

#### 2.2.2 组件化
&emsp;&emsp;读者可以非常粗暴地理解，前端中的`组件`就是一堆为了实现共同目标的代码文件的组合。比如说一个 hello-world 的组件，它的文件结构很可能是这样的：

```
├── hello-world
│   ├── hello-world.component.js
│   ├── hello-world.html
│   ├── hello-world.css
```

&emsp;&emsp;随意前端的发展，组件的定义也逐渐清晰，一个典型的出自名门的例子便是 React，React 是 Facebook 出品的前端框架，它不但“重新”定义了 html，开发了一套 jsx 的语法，将同一个组件的 html 模板写在同一个文件中，甚至将样式表也封装到了 jsx 里，例如用 React 写的 HelloWorld 代码如下：

```javascript
// hello-world.component.jsx
var {React} = require('react')
var HelloWorld = React.createClass({
  render: function() {
    return (
      <div className="hello-world">
        Hello, world!
      </div>
    );
  }
});
module.exports = HelloWorld;

// index.jsx
var HelloWorld = require('./hello-world');
ReactDOM.render(
  <HelloWorld />,
  document.body
);
```

##### 组件化的好处
&emsp;&emsp;在大型的软件开发中，离不开组件化。通过高度的抽象，组件化提高了开发效率、代码复用率，降低开发维护成本。但是在 Web 前端并没有通用的组件标准，并不像 Java 或者 C# 那样提供了标准的UI组件，Web 前端领域正是缺少标准的的实现方式，所以每个框架/库都有一套自己的组件化方式，包括本书讲解的 Angular2 也有自己的组件化方式。

#### 2.2.3 组件化的标准
&emsp;&emsp;W3C 对 Web 组件提出了`WebComponent`的标准，通过标准化的非侵入方式封装组件，每个组件包含自己的 html、css、js 代码，并且不会对页面上其他代码产生影响。它包含以下几种重要的概念：

##### HTML导入
&emsp;&emsp;HTML 导入，是在一种在 HTML 文档中引入其他 HTML 文档的方法。在这个“其他” HTML 文档中，还能够和平常一样引入 CSS，JavaScript 等这些能在 .html 文件中能包含的任何内容。举个例子，有一个 bootstrap.html 包含了 Bootstrap 所需的各种文件：

```html
<link rel="stylesheet" href="bootstrap.css">
<script src="jquery.js"></script>
<script src="bootstrap.js"></script>
...

<!-- 还能定义一些模板 -->
<template>
  ...
</template>
```

&emsp;&emsp;然后在应用的 index.html 引入：

```html
<head>
  <link rel="import" href="bootstrap.html">
</head>
```

&emsp;&emsp;HTML 导入的功能使得开发者能够将开发好的一个模块写到一个 .html 文件去给他人使用，换句话说，仅用一个 URL，就可以将多个文件封装成一个文件提供给他人使用。

##### 模板
&emsp;&emsp;模板允许开发者预先写好一些 html 标记，用于后续使用或复用。如果你使用过 angular1.x 或者 handlebars 之类的东西，你应该熟悉模板是什么。例如：

```html
<template>
  <h1>Hello!</h1>
  <p>You can't see this script in the page.</p>
</template>
```

&emsp;&emsp;所有在`template`中的脚本都被浏览器看作“静态”的东西，换句话说所有写在`template`里面的像\<img\>、\<video\>这些标签引用的资源都不会被加载，\<script\>标签也不会被执行，里面所有的标签也都不会被渲染到页面中。直到我们使用 javascript 去控制它。

##### Shadow DOM
&emsp;&emsp;通过 Shadow DOM 可以在文档流中创建一些完全独立于其他元素的 DOM 子树，这个特性可以可以让开发者开发一个独立的组件，并且不会干扰到其它 DOM 元素（非侵入的方式）。Shadow DOM 和标准的 DOM 行为一样，可以通过 html、css、js 去定义。居于这个特性，使得组件的复用变得简单。

##### 自定义元素
&emsp;&emsp;WebComponent 规范允许开发者声明一个语义化的自定义元素来引用组件：

```html
<template id="hello-template">
  <h1>Hello!</h1>
</template>

<script>
  // 获得上面的模板
  var tmpl = document.querySelector('#hello-template');

  // 创建一个新元素的原型，继承自 HTMLElement
  var HelloProto = Object.create(HTMLElement.prototype);

  // 设置 Shadow DOM 并将模板的内容 clone 进去
  HelloProto.createdCallback = function() {
    var root = this.createShadowRoot();
    root.appendChild(document.importNode(tmpl.content, true));
  };

  // 注册新元素
  var Hello = document.registerElement('hello', {
    prototype: HelloProto
  });
</script>
```

&emsp;&emsp;目前的浏览器只有 Chrome 和 Opera 对 WebComponent 的支持度比较高，其他浏览器不能运行使用 WebComponent 标准写的哪怕是很简单的 hello-world 代码。Google 官方出口的 Polymer 框架则比较接近 WebComponent 的写法，它简直就是面向未来的框架。同样也是出自 Google 之手的 Angular2 ——也就是本书的内容——的概念也有几分相似，虽然 Angular1 也能写模板和自定义元素，但 Angular2 的组件化比 Angular1 更加彻底。

### 2.3 Angular2的组件
&emsp;&emsp;前面的章节已经介绍了 Angular2 是什么，以及为什么要使用它。本章的开头也介绍了组件及组件化的概念，在 Angular2 中，组件是非常重要的组成部分，一种更面向对象的方法来开发Web 应用。

&emsp;&emsp;如果读者写过 Java 或者 C#，或者其他强面向对象的语言，你会很容易理解“组件”，它实际上是一个类，一个有着自己特定的成员数据，并根据成员数据的特性将自己渲染到屏幕上的类。Angular2 也不外乎这些，先看看 Hello World：

```typescript
import {Component, OnInit, ViewEncapsulation} from '@angular/core';
import {bootstrap} from '@angular/platform-browser-dynamic';

@Component({
  selector: 'hello-world',
  template: '<div>Hello World, {{name}}</div>',
  encapsulation: ViewEncapsulation.None
})
export class HelloWorldComponent implements OnInit {
  constructor() {
    this.name = 'Super Man';
  }
  ngOnInit() {
    console.log('HelloWorldComponent inited');
  }
}

bootstrap(HelloWorldComponent, [])
```

&emsp;&emsp;然后在 index.html 的 body 中，用上 hello-world 组件：

```html
<body>
  <hello-world>Loading...</hello-world>
</body>
```

&emsp;&emsp;上面的代码大概的意思是创建了一个叫 HelloWorldComponent 的组件，这个组件有一个`name`的成员数据，它将 template 里指定的 div 渲染到了页面上，并且在组件初始化时输出`HelloWorldComponent inited`。所有的 Angular2 应用都需要通过 bootstrap 去启动。

&emsp;&emsp;以上代码，也展示了 Angular2 及组件的一些核心概念：

> - 自定义标签（selector）
> - 模板（template）
> - 视图包装（view encapsulation）

##### 自定义元素
&emsp;&emsp;Angular2 允许开发者自定义元素名称，在刚才的示例代码中，`selector: hello-world`就给 HelloWorldComponent 定义了一个新的元素名称`hello-world`，在相应的 index.html 里，就可以这样去使用了`<hello-world>Loading...</hello-world>`。

> 为什么要在`hello-world`之间加上一句`Loading...`？这是因为在 Angular2 还没解析好组件并渲染到页面上时，可以看到一个加载的提示。当然也可以不加上。

##### 模板
&emsp;&emsp;和很多框架一样，Angular2 也提供模板机制，允许开发者预先定义好一系列 DOM 结构，以用于填充数据。例子中的`template: '<div>Hello World, {{name}}</div>'`便为 HelloWorldComponent 指定了模板内容。关于模板的更多内容，请参考**模板**章节。本节也会作简单的介绍。

##### 视图包装
&emsp;&emsp;相比 Angular1，这是一个新的特性，并且可以配置使用原生的 Shadow DOM，它的主要目的是让组件的样式之间更加“独立”而互不影响，使得组件间的复用变得更简单。ViewEncapsulation 有三个可选的值：

- ViewEncapsulation.None - 无 Shadow DOM，并且也无样式包装。
- ViewEncapsulation.Emulated - 无 Shadow DOM，但是通过 Angular2 提供的样式包装机制来模拟组件的独立性，使得组件的样式不受外部影响。
- ViewEncapsulation.Native - 使用原生的 Shadow DOM 特性。

&emsp;&emsp;接下来的内容通过详细的例子来深入认识组件，以及理解以上的核心概念。

#### 2.3.1 组件基本概念
&emsp;&emsp;和 DOM 树类似，Angular2 的应用是一棵组件树，每个组件都是一个`类`，有自己的生命周期，组件使用`@Component`标注来修饰。

&emsp;&emsp;每个组件都应有它对应的模板，通过`template`或`templateUrl`来指定。模板决定了组件在页面上的展现方式。

&emsp;&emsp;Angular2 通过单向的数据流，将更新应用模型（Application Model）和视图状态（View State）分成两个阶段：开发者负责更新模型；Angular2 则通过变更检测（Change Detection）自动更新对应的视图。

&emsp;&emsp;事件绑定（Event Bindings），开发者可以通过`()`操作符将事件绑定到组件中，当浏览器触发了该事件，则此绑定的组件方法便会执行，这便是第一种情况：开发者通过定义方法来更新模型。

&emsp;&emsp;属性绑定（Property Bindings），开发者可以通过`[]`将组件中的属性绑定到模板上，这样当组件中的属性变化时，Angular2 的变更检测机制便会自动更新该组件的对应视图。

**（此处应有图）**

&emsp;&emsp;对组件来说，属性绑定是一种`数据输入`，用`@Input`定义，通过`[]`语法调用；事件绑定则是`数据输出`，使用`@Output`定义，通过`()`语法调用。

&emsp;&emsp;一般来说，每一个应用程序都有自己的根组件（一般被命名为 XxxApp 或 XxxAppComponent），当应用被启动（bootstrap）时，Angular 会从根组件开始启动，并解析组件树。

&emsp;&emsp;现在让我们来看看一个通讯录的例子。

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/ng2-contact-demo.png)

图2-2 通讯录 Demo

##### 应用的启动（Bootstrap）

```typescript
import {bootstrap} from '@angular/platform-browser-dynamic';
import {ContactApp} from './app/contact-app';

bootstrap(ContactApp, [])
.catch(err => console.error(err));
```


#### 2.3.2 组件功能详解

@Component的MetaData成员大家族总览（通过Demo层层深入）
首先从上面的例子，我们已经知道了下面这些组件功能（继续扩展讲述）
selector
匹配HTML中的自定义标签
继续讲解selector的一些注意事项
省略后变成"div"
驼峰命名还是烤肉串命名
template
如何引用成员类的变量及函数
如果想将模板外链，可通过templateUrl指定路径
详情引导至第三章