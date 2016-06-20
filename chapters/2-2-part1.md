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

### 2.4 组件基本概念
&emsp;&emsp;和 DOM 树类似，Angular2 的应用是一棵组件树，每个组件都是一个`类`，有自己的生命周期，组件使用`@Component`修饰符（Decorator）来修饰。

&emsp;&emsp;每个组件都应有它对应的模板，通过`template`或`templateUrl`来指定。模板决定了组件在页面上的展现方式。

&emsp;&emsp;Angular2 通过单向的数据流，将更新应用模型（Application Model）和视图状态（View State）分成两个阶段：开发者负责更新模型；Angular2 则通过变更检测（Change Detection）自动更新对应的视图。

&emsp;&emsp;事件绑定（Event Bindings），开发者可以通过`()`操作符将事件绑定到组件中，当浏览器触发了该事件，则此绑定的组件方法便会执行，这便是第一种情况：开发者通过定义方法来更新模型。

&emsp;&emsp;属性绑定（Property Bindings），开发者可以通过`[]`将组件中的属性绑定到模板上，这样当组件中的属性变化时，Angular2 的变动检测机制便会自动更新该组件的对应视图。

*（此处应有图）*
图2-2 Angular2 组件的数据流

&emsp;&emsp;相对于组件的模板来说，属性绑定是一种`数据输入`，用`@Input`定义，通过`[]`语法调用；事件绑定则是`数据输出`，使用`@Output`定义，通过`()`语法调用。

&emsp;&emsp;一般来说，每一个应用程序都有自己的根组件（一般被命名为 XxxApp 或 XxxAppComponent），当应用被启动（bootstrap）时，Angular 会从根组件开始启动，并解析组件树。

&emsp;&emsp;现在让我们通过通讯录的例子，分析组件的功能。

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/ng2-contact-demo.png)

图2-3 通讯录 Demo

##### 应用的根组件（ContactApp）

&emsp;&emsp;contact-app.ts 部分代码

```typescript
import {Component, OnInit} from '@angular/core';
...

@Component({
  selector: 'contact-app',
  templateUrl: 'app/contact-app.html',
  styleUrls: ['app/contact-app.css']
})
...
export class ContactApp implements OnInit{
  constructor() {}

  ngOnInit(){
  }
}
```
&emsp;&emsp;代码中的`import`在之前也出现了不少次，如果读者了解 NodeJS 的话，这里也很容易理解，因为 Angular2 所有的模块都是依照 NodeJS 的规范去管理的，这里的意思就是从`node_modules`的`@angular`模块中的`core`子模块，导入`Component`和`OnInit`这两个接口。

> OnInit 是组件生命周期中的初始化，后续内容将会讲述。

&emsp;&emsp;然后代码定义了一个`ContactApp`的类，并用`@Component`修饰符修饰了这个类，这是用于定义 Angular2 组件的修饰符，它使得这个类“成为” Angular2 的一个组件。这是 Angular2 提供的一种便捷的语法，除此之外 Angular2 还提供了其他很多很有用的修饰符，用于对开发者定义的类进行修饰，使得这个类可以”装配“上特定的功能。例如上面的代码，通过`selector`、`templateUrl`和`styleUrls`分别定义了组件的标签、模板以及组件的样式。

&emsp;&emsp;每个组件，更准确来说，每个类都会有一个构造方法`constructor`，在构造方法中可以用于声明一些类的属性或做一些**简单的**初始化操作。注意这里用了“简单的”词眼，像变量赋值初始化这些便是“简单的”操作。一般不建议在构造方法里做复杂的初始化操作，例如我们经常会在页面 loaded 之后获取数据，相应地类似这些操作不建议放在构造方法中，而建议放在`ngOnInit`中，保持构造方法的简洁。

&emsp;&emsp;刚才也提到了`OnInit`接口，这个组件实现了这个接口。这是 TypeScript 提供的一种语法约束，类似 Java 中的 Interface，当组件声明了要实现某个接口时，相应地就必须添加该接口的方法实现。例如`OnInit`对应的方法便是`ngOnInit`，以上代码实现了这个接口方法，方法体为空。

##### 应用的启动（Bootstrap）

&emsp;&emsp;app.ts 部分代码

```typescript
import {bootstrap} from '@angular/platform-browser-dynamic';
...
import {ContactApp} from './app/contact-app';


bootstrap(ContactApp, ...)
```

&emsp;&emsp;有了根组件，还需要告诉 Angular2 去启动它。因为 Angular2 的启动是平台相关的，它能实现在后端渲染以提高页面输出的速度以及优化 SEO，现在此处需要在浏览器端渲染，所以代码中从`plattorm-browser-dynamic`导入了`bootstrap`这个方法。启动应用很简单，将根组件作为第一个参数传入`bootstrap`即可。

&emsp;&emsp;最后，别忘了还需要在 index.html 中写上你的根组件要渲染的位置。

```html
<body>
  <contact-app>
    Loading...
  </contact-app>
</body>
```


*此处要看前面的内容是否已讲述过bootstrap，若无则要展开一下bootstrap的参数之类*


### 2.5 组件功能详解
&emsp;&emsp;上一小节对组件的概念已经有了基本的认识，这一节再深入学习 Component 常用的 元数据（metadata）以及字段修饰器。

#### 2.5.1 @Component 常用的元数据
&emsp;&emsp;在通讯录的例子中，基本上都是由组件组成的，组件是使用 Angular2 开发中最常用的功能，并且在每个组件，基本上都必须要用到以下元数据。

&emsp;&emsp;再看看 contact-app.ts 这个文件中的 @Component 修饰器部分：大部分组件都会使用到这些元数据——`selector`、`templateUrl/template`、`styleUrls/styles`、`directives`、`providers`。

```typescript
...
@Component({
  selector: 'contact-app',
  providers: [ContactService],
  directives: [ROUTER_DIRECTIVES],
  templateUrl: 'app/contact-app.html',
  styleUrls: ['app/contact-app.css']
})
...
```

##### selector（string）
&emsp;&emsp;用于定义组件在 HTML 代码中匹配的标签。selector 参数是必须设置的，它将成为新组件的命名标记，它的工作原理很像 querySelector，会返回文档中选择器匹配到的第一个元素。

> 事实上 selector 也可以忽略不指定，此时默认会变成 div，但绝对不要这样做，因为这样组件会无法准确定位 DOM 中的元素。
> 
> selector 的命名方式建议使用“烤肉串式”命名，即名称全小写，并以`-`分隔。例如`contact-app`、`hello-world`。

##### templateUrl（string）
&emsp;&emsp;为组件指定一个外部模版的 URL 地址

```typescript
  templateUrl: 'app/contact-app.html',
```
> 关于模板的更多内容，请参见**模板**章节。

##### template（string）
&emsp;&emsp;为组件指定一个内联模版。

> 每个组件只能指定一个模版，templateUrl 或 template。
> 
> 如果要写内联模板，建议使用ES6的``语法，能够轻松创建多行模版。
> 
> ```typescript
>   template: `
>     <div>
>       <div>Inner Div</div>
>     </div>
>   `
> ```

##### styleUrls（string[]）
&emsp;&emsp;为组件指定一系列用于该组件的样式表文件。

```typescript
  styleUrls: ['app/contact-app.css']
```

##### styles（string[]）
&emsp;&emsp;为组件指定内联样式。

> styles 和 styleUrls 允许同时指定。如果同时指定，styles 中的样式会先被解析，然后才会解析 styleUrls 中的样式。换句话说，styles 的样式会被 styleUrls 的样式覆盖。
> 
> 强烈建议，styles 或 styleUrls 只使用其中一个设置。

##### directives（Array\<Type | any[]\>）
&emsp;&emsp;指定可以在模版中使用的指令/组件列表。除了 Angular2 默认提供的指令，即 ng 开头的如 ngFor 等不需要显式指定外，自定义的指令或组件必须明确指定，否则在组件中无法正确使用它们。

&emsp;&emsp;例如在 contact-list.ts 的代码中，需要指定了`Footer`和`ListChildrenComponent`这两个组件，然后才能在模板 contact-list.html 中使用它们：

*此处的 Footer、ListChildrenComponent 等组件的名称可能要规范下*

&emsp;&emsp;contact-list.ts 部分代码:

```typescript
...
@Component({
  ...
  directives: [
    ROUTER_DIRECTIVES,
    Footer,
    ListChildrenComponent  // 引入了 Footer、ListChildrenComponent 两个组件
  ]
})
...
```
&emsp;&emsp;contact-list.html:

```html
<h3>所有联系人<i (click)="addContact()"></i></h3>
<ul class="list">
  <li *ngFor="let contact of contacts">
    <!-- 组件中指定了 ListChildrenComponent，才能使用 list-li 标签 -->
    <list-li [contact]="contact" (routerNavigate)="routerNavigate($event)"></list-li>
  </li>
</ul>
<!-- 组件中指定了 Footer，才能使用 my-footer 标签 -->
<my-footer [path]="path" (writeTitle)="writeTitle($event)"></my-footer>
```
> 关于指令的更多内容，请参阅**指令**章节。

##### providers（any[]）
&emsp;&emsp;指定级联的组件依赖注入的服务列表。

```typescript
  providers: [ContactService],
```

&emsp;&emsp;为什么说是“级联”呢？因为通常依赖注入的服务，会在应用的根组件一并设置。

&emsp;&emsp;为什么这样做？本书认为，服务是用于共享数据、实现业务逻辑的，而这些数据或者业务逻辑，一般是为应用所用，而不是为某个组件所用，并且注入的服务是单例的。在根组件设置这些服务注入，就避免了要在每个组件都设置的麻烦。

&emsp;&emsp;是否可以为组件注入特定的服务？答案是可以的，本章节后续会解释`viewProviders`的用法。或者想了解更多内容，请参阅**依赖注入**和**服务**章节。

#### 2.5.2 组件的常用功能

&emsp;&emsp;组件的模板最终是会解析到 DOM 上的，所以组件必然要和一个 DOM 元素关联，该 DOM 元素称为宿主元素。Angular2 提供了丰富的功能实现了宿主元素和组件之间的交互：

- **变量显示**，将组件的成员变量通过插值的语法显示到宿主元素上
- **事件绑定**，监听宿主元素的事件，响应用户的输入
- **属性绑定**，更改宿主元素的属性，改变组件的显示
- **依赖组件**，通过指定依赖的组件实现更丰富的组件功能
- **自定义内容**，通过使用 ng-content 来创建可复用的组件

&emsp;&emsp;其中**事件绑定**和**属性绑定**，在本章节的**组件基本概念**处也提过，现在一齐来看看具体的用法。

##### 显示组件属性

&emsp;&emsp;先看看 Demo 中的联系人详细页，从首页点击第一个联系人进去。

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/demo-contact-detail.png)
图2-4 联系人详细页

&emsp;&emsp;在该页面中，有很多显示联系人信息的字段如手机号码、邮箱等，右上方有个“编辑”按钮，头像右边有个收藏按钮。

&emsp;&emsp;contact-detail.ts 部分代码。`ContactDetail`这个类中定义了三个成员变量`contact_id`，`detail`和`contacts`。

```typescript
...
export class ContactDetail implements OnInit, OnDestroy {
  contact_id: number;
  detail:any = {};
  contacts:any = {};
  
  ...
  
  ngOnInit() {
    this.contact_id = parseInt(this._routeParams.get('id'));
    this.getById(this.contact_id);
  }
  
  ...
  
  getById(id:number) {
    let ss_contacts = sessionStorage.getItem('contacts');
    if(ss_contacts) {
      this.contacts = JSON.parse(ss_contacts);
      this.detail = this.contacts[id-1];
    }else {
      this._constactService.getContactById(id).subscribe(data => {
        this.detail = data;
      });
    }
  }
}
```

&emsp;&emsp;我们来看看`detail`，它是联系人信息的对象。`ContactDetail`实现了`OnInit`和`OnDestroy`这两个**生命周期**的方法，并且在`ngOnInit`的时候，初始化了成员变量。之后，Angular2 便会将在模板中引用到的`detail`成员变量的属性（如手机号码`detail.telNum`）显示到宿主元素上。

> 生命周期是组件的关键概念，详情请参阅本章的后续小节。

&emsp;&emsp;在对应的模板 contact-detail.html 中，需要用`{{}}`语法，来显示成员变量的值。

```html
...
    <li>
      <p>手机号码：</p>
      <p>{{ detail.telNum }}</p>
    </li>
...
```

> 这种语法`{{}}`在 Angular2 中称为**插值**，本质上**插值**和**属性绑定**都属于 Angular2 中的**数据绑定**的概念，但是属性绑定是指在元素的属性上的数据绑定，并且使用的语法并不一样，于是本书将它们分开讲解。
> 
> 关于插值、数据绑定的更多内容，请参阅**模板**章节。

##### 事件绑定
&emsp;&emsp;Angular2 提供了非常方便的事件绑定的方式，通过`(event)`的语法，便可以轻易地响应UI事件。

&emsp;&emsp;contact-detail.html 中的点击编辑按钮的代码。

```html
...
    <a class="edit" (click)="editContact()">编辑</a>
...
```

&emsp;&emsp;就是这么简单，“编辑”按钮在用户点击时，便会触发 click 事件，从而调用到组件的`editContact()`方法，跳转到编辑联系人的页面。

```typescript
...
  editContact() {
    this._router.navigate(['Operate',{id: this.contact_id}]);
  }
...
```

&emsp;&emsp;事件绑定还支持传递事件参数`$event`，例如在刚才的“编辑”按钮里，如果加上这个参数，在组件中的方法便能得到这个参数，从而获得事件信息如点击的元素、坐标等。

```html
...
    <a class="edit" (click)="editContact($event)">编辑</a>
...
```

```typescript
...
  editContact($event) {
    this._router.navigate(['Operate',{id: this.contact_id}]);
    console.log($event.type); // 此处会打印 click
  }
...
```

&emsp;&emsp;正如本章**组件基本概念**中所描述的，事件绑定在 Angular2 中是一种单向的数据流，**事件及包含事件的数据**由 Angular2 内部处理，从宿主元素中传递到组件，使得组件能够与模板的事件进行交互。

> 关于事件绑定的更多内容，请参阅**模板**章节的相关部分。

##### 属性绑定
&emsp;&emsp;相对于事件绑定，属性绑定则是 Angular2 通过变动检测机制，及时检测到组件成员变量的变化，并将变更重新渲染到宿主元素的 DOM 上的过程。这种数据流向也是单向的，**成员变量**数据通过 Angular2 的处理，传递到宿主元素。

> 变动检测机制，也是组件的核心概念，详情请参阅本章的**变动检测机制**小节。

&emsp;&emsp;请看例子中的 contact-detail.html 的代码片段

```html
...
      <span class="contact-name">
        {{ detail.name }}
        <i [ngClass]="{collect: detail.collection == 0, collected: detail.collection == 1}" (click)="collectTheContact()"></i>
      </span>
...
```

&emsp;&emsp;当点击头像右下方的“收藏”标记时，会触发 click 事件并调用组件的`collectTheContact`方法，该方法会将成员变量`detail`的`collection`属性由0变为1，或由1变为0，即是否收藏该联系人。

```typescript
  ...
  collectTheContact() {
    this.detail.collection == 0 ? this.detail.collection = 1 : this.detail.collection = 0;
    ...
  }
  ...
```

&emsp;&emsp;回头看 html 中的代码，注意其中的`[ngClass]`中使用到了`detail.collection`这个变量的值去判断，当为0时，使用`collect`这个样式，当为1时，使用`collected`这个样式。当相应的变量值被改变时，Angular2 的变更检测便会检查到，从而根据模板中的表达式去更新 DOM。

> 以上例子使用的是`ngClass`，事实上，更准确来说这是一个**指令**，而不是 DOM 对象的属性。广义的属性绑定包括了 DOM 元素的属性、组件的属性、指令属性三种。
> 
> 组件的即自定义属性，一般用作组件间的数据交互，详见本章的**组件交互**小节。
> 
> 关于属性绑定的更多内容，请参阅**模板**章节的相关部分。

##### 依赖组件
&emsp;&emsp;在前面我们提到过 directives、providers 等属性，通过定义这些依赖，可以使得组件的逻辑更多丰富，使得开发复杂的组件变得容易。

&emsp;&emsp;组件中另一个常用的功能是管道（pipes），通过在组件的元数据中指定 pipes，便可以在模板中使用它，管道的主要作用是用来格式化数据，通常这对于国际化很有用处。

> 关于管道的更多知识，请参阅**模板**章节的相关部分。

##### 自定义内容
&emsp;&emsp;自定义内容有时被认为是一个高级的功能，使用自定义内容能很好地扩充组件的功能，特别是在需要创建团队、项目之间共享的通用的 HTML 代码片段的时候。

> 接触过 Angular1 的读者，相信对这个自定义内容的知识不会陌生，它和 Angular1 中指令的 `transclude`属性非常类似。

&emsp;&emsp;自定义内容通用用来创建可复用的组件，典型的例子是模态对话框或导航栏。想像一下，在开发 Web 应用的时候，模态对话框和导航栏是使用得非常频繁的功能，自定义内容的特性正是提供了一种复用的方式，使得复用的组件具有样式完全一致的，但内容可自定义的组件。

*demo中需要补充自定义内容的例子*


#### 2.5.3 @Component 的其他元数据

##### inputs（string[]）
&emsp;&emsp;相当于定义属性绑定，指定哪些属性可以设置组件，通过 inputs 将数据流绑定到组件中。详情请参考本章节的**组件交互**小节关于`@Input`的内容。

##### outputs（string[]）
&emsp;&emsp;相当于事件绑定，标识组件可以通过 outputs 发送信息到父组件的事件。详情请参考本章节的**组件交互**小节关于`@Output`的内容。

##### properties（string[]）
&emsp;&emsp;这是旧版本的属性，可忽略，相当于 inputs。

##### events（string[]）
&emsp;&emsp;这是旧版本的属性，可忽略，相当于 outputs。

##### host（{[key: string]: string}）
&emsp;&emsp;host 是个非常强大的元数据，它主要用在指令中，通过 host 可以指定此指令/组件的事件、动作和属性等。因为 @Component 继承自 @Directive，所以 @Directive 中的配置也同样适用于组件。更多内容请参阅**指令**章节。

##### exportAs（any[]）
&emsp;&emsp;此属性主要在指令中使用，作用是将指令分配给一个变量，使用这个名称就可以在模版中调用指令。因为 @Component 继承自 @Directive， 所以 @Directive 中的配置也同样适用于组件。更多内容请参阅**指令**章节。

##### moduleId（any[]）
&emsp;&emsp;包含该组件模块的 id，它被用于解析模版和样式的相对路径。在 Dart 中，它可以被自动确定，并不需要去设置。在 CommonJS 中，它总是被设置为 module.id。 

##### queries（{[key: string]: any;}）
*todo待搞明白*

&emsp;&emsp;配置需要被注入到组件的查询，内容查询在ngAfterContentInit回调函数被调用之前设置，视图查询ngAfterViewInit回调被调用前设置

```typescript
@Component({
  selector: 'someDir',
  queries: {
    contentChildren: new ContentChildren(ChildDirective),
    viewChildren: new ViewChildren(ChildDirective)
  },
  template: '<child-directive></child-directive>',
  directives: [ChildDirective]
})
class SomeDir {
  contentChildren: QueryList<ChildDirective>,
  viewChildren: QueryList<ChildDirective>
  ngAfterContentInit() {
    // contentChildren is set
  }
  ngAfterViewInit() {
    // viewChildren is set
  }
}
```

##### viewProviders（any[]）
*todo例子待完善，需要配合ng-content*

&emsp;&emsp;定义一组在子节点的视图可见的依赖注入对象，下面例子中的 viewProviders 声明了 Greeter 类可以被注入：

```typescript
class Greeter {
   greet(name:string) {
     return 'Hello ' + name + '!';
   }
}
@Directive({
  selector: 'needs-greeter'
})
class NeedsGreeter {
  greeter:Greeter;
  constructor(greeter:Greeter) {
    this.greeter = greeter;
  }
}
@Component({
  selector: 'greet',
  viewProviders: [
    Greeter
  ],
  template: `<needs-greeter></needs-greeter>`,
  directives: [NeedsGreeter]
})
class HelloWorld {
}
```

##### changeDetection（ChangeDetectionStrategy）
&emsp;&emsp;定义使用的变动检测策略。

&emsp;&emsp;当组件被实例化，Angular2 创建一个变动监测器，它负责传播组件的绑定。通过修改此属性，来为组件选择是每次变动检测都会被检查还是只有组件告诉它的时候才触发。不同的策略包括：

- Default：CheckAlways
- OnPush
- Detached
- CheckAways
- Checked
- CheckOnce

&emsp;&emsp;可以设定具体的检查策略减少检查的次数，来提高程序的性能。

> 更详细的内容，请参阅本章节的**变动检测机制**小节。

##### pipes（Array\<Type | any[]\>）
&emsp;&emsp;用于指定组件对应的模板中使用的属性过滤、格式化处理的类，更多的内容请参阅**模板**章节的相关内容。

##### encapsulation（ViewEncapsulation）
&emsp;&emsp;在本章的开头部分，提到了**视图包装**这个特性，它的主要目的是让组件的样式之间更加“独立”而互不影响，使得组件间的复用变得更简单。ViewEncapsulation 有三个可选的值：

ViewEncapsulation.None - 无 Shadow DOM，并且也无样式包装。
ViewEncapsulation.Emulated - 无 Shadow DOM，但是通过 Angular2 提供的样式包装机制来模拟组件的独立性，使得组件的样式不受外部影响。
ViewEncapsulation.Native - 使用原生的 Shadow DOM 特性。

*todo补充更多内容*

### 2.6 组件的生命周期

> 关于组件的生命周期，可继续阅读“指令”的生命周期章节。
> 组件继承自指令，因此它们具有相同的生命周期实现。

&emsp;&emsp;使用过 Angular1 的读者应该知道，Angualr1 中有构造函数，$watch 方法和 $destroy 事件可以尝试挂接控制器中生命周期的各个时间点。在 Angular2 中，生命周期的含义被定义得更加明确，包括但不限于 ngOninit、ngOnDestroy、ngOnchanges。当组件实现一些生命周期钩子的回调，那么在变动检测的时候就会在特定的时间点被触发。

&emsp;&emsp;当组件被创建的时候构造函数被调用，获取到组件的初始状态，如果组件依赖子组件中的属性或数据，我们需要等它初始化完毕。要做到这一点，我们可以处理 ngOnInit 生命周期事件，或者可以在构造函数里调用 setTimeout 能达到同样效果。就像 ngOnInit，我们可以追踪一个组件生命周期中很多事件的足迹。

#### 2.6.1 生命周期勾子

##### OnInit
&emsp;&emsp;使用 ngOnInit 有两个重要的原因：

1. 构造后不久就要进行复杂的初始化
2. 在 Angular 设置输入属性之后就要设置组件

&emsp;&emsp;在 Angular2 的组件中，经常会使用 ngOnInit 获取数据，那为什么不在组件构造函数中获取数据呢？因为构造函数做的事，应该是尽可能简单的，例如初始化局部变量这种简单的事情。这对于有经验的开发人员来说，已经是一种共识。另外，这对于 Angular2 的自动化测试也有非常重要的作用，因为编写测试代码的开发人员，不需要担心一个新的组件在测试或者创建之前会尝试连接远程服务器获取数据。

##### OnDestroy
&emsp;&emsp;组件在被销毁之前会触发这个勾子，ngOnDestroy 会被调用。建议把组件成员变量等东西的清理逻辑放到 ngOnDestroy 中，它是在指令/组件销毁之前必定运行的逻辑。在这个时候可以通知另一部分关心的程序，这个组将将要被销毁。

&emsp;&emsp;不会被垃圾处理自动收集的资源应当在这个地方去释放，例如订阅了的观察者事件，绑定过的 DOM 事件，通过 setTimeout 或 setInterval 设置过的计时器等，都应当在 ngOnDestroy 中去注销、删除所有与该组件相关的回调。如果忽略这些的话，会导致一些意想不到的后果，并有可能导致内存泄漏。

*todo以下待修改*

**OnChanges**
&emsp;&emsp;我们监测这个例子中OnChanges钩子。只要检测到组件的输入属性部分发生变化，angular就调用其ngOnChanges方法。
下面是我们钩子的实现：

```typescript
ngOnChanges(changes: {[propertyName: string]: SimpleChange}) {
  for (let propName in changes) {
    let prop = changes[propName];
    let cur  = JSON.stringify(prop.currentValue)
    let prev = JSON.stringify(prop.previousValue);
    this.changeLog.push(`${propName}: currentValue = ${cur}, previousValue = ${prev}`);
  }
}
```
&emsp;&emsp;该ngOnChanges方法接受一个对象映射每个更改的属性名称与当前和以前的属性值的 SimpleChange 对象，我们遍历更改的属性并记录下它们。
在我们的例子OnChangesComponent输入属性是heros和power。

```typescript
@Input() hero: Hero;
@Input() power: string;
```
&emsp;&emsp;父组件像这样绑定它们：

```typescript
<on-changes [hero]="hero" [power]="power"></on-changes>
```
&emsp;&emsp;运行实例时能看到 power 属性变化的字符串值，但 ngOnChanges 没有捕捉到 hero.name 的变化，这看起来很奇怪。
angular 仅调用挂接的输入属性值的更改，hero 属性值是参照 hero对象，hero 对象的引用并没有变化，angular不关心 hero 自身名字属性的变化。因此，从 angular 的角度来说这是没有变化的。

> 我们第一个访问这些属性的机会在ngOnInit前是 angular 调用  ngOnChanges 方法之前。angular 会多次调用ngOnChanges但只调用ngOnInit一次。

**DoCheck**
&emsp;&emsp;我们可以使用DoCheck钩子来检测并在angular没有捕捉到自身变化的时候采取行动。通过这个方法我们可以检测到 angular 忽略的这一变化，使用这些信息刷新显示就是另外一回事了。
&emsp;&emsp;ngDoCheck钩子的调用有巨大的频率－每一个变化检测周期后，不管发生变化的地方。大多数这些初步检查是由angular在网页其他地方不相关的数据第一次渲染的时候触发，单纯的将鼠标移到另一个输入框就会触发调用，相对较少的调用才有相关数据的实际变化。很明显，我们的实现必须很轻否则用户体验就会受到影响。

**AfterView**
&emsp;&emsp;AfterViewChecked和AfterViewInit钩子根据子视图中值的变化采取行动，我们只能通过查询子视图的属性描述 @ViewChild 延伸。

&emsp;&emsp;我们必须遵循angular的单项数据流原则，当它组成后我们可能不会更新视图。当组件的视图已经渲染完毕后这两个钩子会被触发。
&emsp;&emsp;如果我们立即更新组件的数据绑定 comment 属性，angular会抛出一个错误。setTimeout推迟了浏览器的javascript循环更新一周，这个时间已经足够长了。

&emsp;&emsp;注意，angular经常调用AfterViewChecked，往往没有有意义的变化。写单一的钩子方法能避免性能问题。

**AfterContent**
&emsp;&emsp;AfterContent例子是探索angular何时调用AfterContentInit和AfterContentChecked挂钩以angular项目外部的内容到组件。
内容投影是一种从外面向组件导入HTML内容和将该内容插入组件模版指定点的方法。

&emsp;&emsp;当指令的数据绑定属性已经初始化并且子组件未被检查的时候，通过这个接口来执行自定义的初始化逻辑，只有该指令第一次被实例化它才会被调用。


&emsp;&emsp;最后，这些事件处理程序必须在控制器的原型上定义，否则 angular 无法在适当的时候调用它们。

```typescript
//...
function ProtoController() {
	this.bindType = "Defined on constructor prototype.";
}
ProtoController.prototype = {
	ngOnInit: function() {
		console.log( "ngOnInit:", this.bindType );
	},
	ngOnDestroy: function() {
		console.log( "ngOnDestroy", this.bindType )
	}
};

function InstanceController() {
	var bindType = "Defined on instance.";
	this.ngOnInit = function() {
	    console.log( "ngOnInit:", bindType );
	};
	this.ngOnDestroy = function() {
	    console.log( "ngOnDestroy:", bindType );
	};
}
```
&emsp;&emsp;我们会发现，这些事件处理器只有定义在控制器的原型（如ProtoComponent组件的ProtoController.prototype）上才会被调用，InstanceController中声明的并没有起作用。

&emsp;&emsp;使用属性装饰所有生命周期钩子，而不使用接口
&emsp;&emsp;目前组件和路由组件的生命周期都是通过接口定义的（例如Oninit），这存在一些问题，因为这些接口在Javascript中没有运行时的表现。所以在运行时如果我们调用了它，我们只是检查接口中是否定义了这些方法，它们在组件实例中是否存在。如果组件中有一个 onInit方法，这并不意味着它会成为一个生命周期钩子，但我们仍然会调用它。
&emsp;&emsp;这些命名冲突可能会导致意想不到的结果，如果我们增加新的生命周期钩子，可能破坏现有的组件。基于这些原因，建议大家使用属性描述来取代接口的定义。

#### 2.6.2 路由勾子

canActivate
onActivate
canDeactivate