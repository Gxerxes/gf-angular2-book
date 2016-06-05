## 2 组件

> *此处可能要先回顾一下之前的hello world例子*

&emsp;&emsp;组件（Component）是构成Angular2应用的基础和核心，了解它是如何工作是非常重要的，因此本书也将组件介绍在最前面。

### 2.1 什么是组件

&emsp;&emsp;组件是编写应用的基本单元，通俗地说，一个组件包装了一个特定的功能，并且组件之间协同工作以组装成一个完整的应用程序。

&emsp;&emsp;举个现实中的例子，一辆汽车中包含各种各样的部件、零件，比如发动机、变速箱、轮胎等等，那么这些便可以理解为组成汽车的`组件`，当然这还不是最小粒度的组件，例如发动机本身也会由众多小零件组合而成。

&emsp;&emsp;那么作为Web应用开发者，怎么去理解组件呢？相信读者都应该用过或者知道jQueryUI、Bootstrap、YUI等一些经典的UI库，即使不知道也没关系，你肯定写过html、css和js。在Web开发中，组件一般是指有着独立的UI界面，并且提供相应的方法，以完成一系列的界面渲染和特定功能交互的代码集合。

&emsp;&emsp;以使用jQueryUI实现一个Dialog组件为例：

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/jquery-dialog-hello-world.png)

&emsp;&emsp;图 2-1 jquery对话框组件

&emsp;&emsp;jQueryUI的Dialog组件代码（部分）：

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

&emsp;&emsp;使用jQueryUI实现的一个HelloWorld对话框组件代码：

```html
<!doctype html>
<html lang="en">
<head>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.11.4/jquery-ui.js"></script>
  <script>
  // 组件代码javascript部分 start
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
  // 组件代码javascript部分 end
  </script>
</head>
<body>
<!-- 组件代码html部分 start -->
<div id="dialog" title="Dialog">
  <p>Hello World!</p>
</div>
<!-- 组件代码html部分 end -->
</body>
</html>
```

&emsp;&emsp;以上代码可以这样理解：

- 首先`$.widget( "ui.dialog" ...`这段代码，表示的是，ui.dialog是一个基础的对话框组件，它是属于jQueryUI库的组件。这个组件提供了对话框的配置、打开、关闭等属性和方法。
- 接下来的html中的代码段，便是使用jQueryUI的开发者，实现了一个“hello world对话框应用。而这个应用中（仅）包含了一个hello world对话框的组件（见上面注释中的`组件代码`部分）。它渲染了一个id为dialog的div，显示了标题、内容，并提供了“OK”和“Cancel”两个按钮给用户操作。

### 2.2 组件化的发展

&emsp;&emsp;前面的内容已经对组件有了初步的了解，下面来了解组件的概念是如何产生的，组件化又是如何发展的。

#### 2.2.1 模块化
&emsp;&emsp;谈到组件化，先要了解`模块化`。在node.js中，模块就是一个文件，引入一个文件就是简单地`require('xxx')`。在前端的领域，也衍生出不少模块化的规范，比如AMD、CMD，不过前端领域发展得很快，因为还未形成一种统一的规范，目前（本书写作的时候）无论是AMD还是CMD都已经过时了，新兴的ES6、TypeScript均采用了类似node的import module的方式，配合browserify、webpack等构建工具将所有模块转换、打包成一个可用于浏览器运行的js文件。

> node.js采用的是CommonJS规范。AMD全称是Asynchromous Module Definition，CMD全称是Common Module Definition，著名的RequireJS、SeasJS分别是AMD、CMD规范的实现之一。


&emsp;&emsp;不过在早期的模块化，只是针对js部分做了处理，比如AMD、CMD的其中一个实现RequireJS、SeasJS也只是管理js模块。后来的火起来的Angular1.x，vue.js都建议将同属一个功能的js、css、html放到一个目录下去管理，当这些具有关联功能的文件组织在一起后，便形成了“组件”的雏形。

#### 2.2.2 组件化
&emsp;&emsp;读者可以非常粗暴地理解，前端中的`组件`就是一堆为了实现共同目标的代码文件的组合。比如说一个hello-world的组件，它的文件结构很可能是这样的：

```
├── hello-world
│   ├── hello-world.component.js
│   ├── hello-world.html
│   ├── hello-world.css
```

&emsp;&emsp;随意前端的发展，组件的定义也逐渐清晰，一个典型的出自名门的例子便是React，React是Facebook出品的前端框架，它不但“重新”定义了html，开发了一套jsx的语法，将同一个组件的html模板写在同一个文件中，甚至将样式表也封装到了jsx里，例如用React写的HelloWorld代码如下：

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
&emsp;&emsp;在大型软件中，组件化的好处是显而易见的，并且已经是一种共识。通过高度的抽象，组件化提高了开发效率、代码复用率，降低开发维护成本。但是在Web前端并没有通用的组件标准，并不像Java或者C#那样提供了标准的UI组件，Web前端领域正是缺少标准的的实现方式，所以每个框架/库都有一套自己的组件化方式，包括本书讲解的Angular2也有自己的组件化方式。

#### 2.2.3 组件化的标准
&emsp;&emsp;W3C对Web组件提出了`WebComponent`的标准，通过标准化的非侵入方式封装组件，每个组件包含自己的html、css、js代码，并且不会对页面上其他代码产生影响。它包含以下几种重要的概念：

##### 模板
&emsp;&emsp;模板允许开发者预先写好一些html标记，用于后续使用或复用。如果你使用过angular1.x或者handlebars之类的东西，你应该熟悉模板是什么。例如：

```html
<template>
  <h1>Hello!</h1>
  <p>You can't see this script in the page.</p>
</template>
```

&emsp;&emsp;所有在`template`中的脚本都被浏览器看作“静态”的东西，即是说所有写在`template`里面的像\<img\>、\<video\>这些标签引用的资源都不会被加载，\<script\>标签也不会被执行，里面所有的标签也都不会被渲染到页面中。直到我们使用javascript去控制它。

##### Shadow DOM
&emsp;&emsp;通过 Shadow DOM 可以在文档流中创建一些完全独立于其他元素的DOM子树，这个特性可以可以让开发者开发一个独立的组件，并且不会干扰到其它 DOM 元素（非侵入的方式）。Shadow DOM 和标准的DOM行为一样，可以通过html、css、js去定义。居于这个特性，使得组件的复用变得简单。

##### 自定义元素
&emsp;&emsp;WebComponent规范允许开发者声明一个语义化的自定义元素来引用组件：

```html
<template id="hello-template">
  <h1>Hello!</h1>
</template>

<script>
  // 获得上面的模板
  var tmpl = document.querySelector('#hello-template');

  // 创建一个新元素的原型，继承自HTMLElement
  var HelloProto = Object.create(HTMLElement.prototype);

  // 设置 Shadow DOM 并将模板的内容clone进去
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

&emsp;&emsp;目前的浏览器只有 Chrome 和 Opera 对 WebComponent 的支持度比较较，其他浏览器不能运行使用 WebComponent 标准写的哪怕是很简单的 hello-world 代码。Google官方出口的Polymer框架则比较接近WebComponent的写法，它简直就是面向未来的框架。同样也是出自Google之手的Angular2——也就是本书的内容——的概念也有几分相似，虽然Angular1也能写模板和自定义元素，但Angular2的组件化比Angular1更加彻底。

### 2.3 Angular2的组件
&emsp;&emsp;前面的章节已经介绍了Angular2是什么，以及为什么要使用它。本章的开头也介绍了组件及组件化的概念，在Angular2中，组件是非常重要的组成部分，一种更面向对象的方法来开发Web应用。一般来说，每一个应用程序都有自己的根组件（一般被命名为XxxAppComponent），当应用被启动（bootstrap）时，Angular会从根组件开始启动，并解析组件树。

&emsp;&emsp;如果读者写过Java或者C#，或者其他强面向对象的语言，你会很容易理解“组件”，它实际上是一个类，一个有着自己特定的成员数据，并根据成员数据的特性将自己渲染到屏幕上的类。Angular2也不外乎这些，让我们来看看一个例子：

```typescript
import {Component} from 'angular2/angular2'

@Component({
  selector: 'my-component',
  template: '<div>Hello World, {{name}}</div>'
})
export class MyComponent {
  constructor() {
    this.name = 'Super Man';
  }
}
```

&emsp;&emsp;上面的代码创建了一个叫MyComponent的组件，这个组件有一个'name'的成员数据，它将template里指定的div渲染到了页面上。

&emsp;&emsp;组件是Angular2应用程序的基本构建模块，通过其关联的模板（视图），控制着屏幕的某部分，并与之交互。