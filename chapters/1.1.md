
2015年6月17日，`ECMAScript 2015`（又名`ES6`）正式发布，这是JavaScript语言的一次重大的革新，也意味着前端界即将迎来一个崭新的时代。

在早些年间，以`jQuery`为代表的DOM操作库曾经给前端界带来过一轮技术革新。`jQuery`以巧妙的封装，链式的调用和清晰的接口使用，大大提升了前端开发的生产力，也降低了前端的入门门槛。在一段时间里很多前端工程师招聘要求里都提及到需要熟悉(精通)jQuery，可见其使用的广泛性与重要性。

近几年来，前端界可谓是百家争鸣，日益兴旺。`jQuery`一统前端的时代也已一去不复还，在与各端和各技术栈的融合中，前端工程师们创造出了很多新奇而又具颠覆性的新东西出来。
 - 使用`Node.js`，前端工程师可以进行服务端开发；
 - 使用`React Native、Ionic`，前端工程师可以进行移动APP开发；
 - 使用`nw.js、Electron`，前端工程师可以进行桌面应用开发。
 
还有很多好玩、实用的框架与库，这些都让前端越发绽放光彩，也让前端工程师成为市场上炙手可热的抢手岗位。

而在众多新技术中以`Angular`为代表的`MVVM`框架又给前端界带来了新一轮的技术革新。

`MVVM (Model-View-ViewModel)`这个概念最早是在2005年由微软提出的，相对于1979年提出的`MVC (Model-View-Controller)`架构来说，还是比较新颖的。
MVVM最主要的特点是双向绑定技术，View层与ViewModel层是相互关联、自动变化的，ViewModel层同时又与Model层是相互通信、自动变化的，从而可以实现了Model和View的真正解耦，代码量也减少了很多。凡是能提升生产力的模式自然是会被提倡与实现的。

实现MVVM这个框架理念的技术有很多种，关键是要实现ViewModel层与其他层的双向绑定，以`Knockout.js`，`Vue.js`等框架均采用的`Object.defineProperty`来设置getter/setter,采用这种做法要比Angular 1.x使用的Dirty check的性能高（注：Angular 2已去除Dirty check这套技术）。但`Object.defineProperty`使用的是ES5的技术，只能兼容到IE8，要兼容更旧的浏览器只能采用其他手段如用VBScript模拟之类的。在Angular 1.2版本加入了`controllerAs`语法，将controller变成了真正意义上的ViewModel, 这使得Angular成为严格意义上的MVVM框架。

正当MVVM框架大行其道时，Facebook公司也推出`React.js`，不同于MVVM框架，React.js只是一个相当于View层的库，其数据更新机制来源自游戏开发领域的理念，采用了"整体刷新"的套路，但由于使用了自身的`Virtual DOM`，避免了开销昂贵的DOM操作，加上其高效的DOM Diff算法（将Diff算法复杂度由O(n^3)降低到了O(n)）能精准地对变化的节点进行更新，所以性能还是非常不错。

对于构建程序的架构设计上，Facebook也提出了`Flux`的概念。不同于`MVC`架构，`Flux`是一个包括了dispatcher、store和views(React components)的单向数据流的架构思想。市场上有很多实现Flux架构的库，其中以`React Hot Reload` 的作者写的`Redux`尤为出名，`Redux`采用了大量ES6的新语法，同时也非常遵循函数式编程的思想。

React社区吸收了很多函数式编程的理念，而函数式编程的一大特点是尽可能减少可变动的部分。过去有人提出 `Om`（用ClojureScript写的React）在速度上比原生js版本的React快了近3倍，震惊了整个社区。究其背后原因，其中一个是`ClojureScript`使用了Immutable Data，受此启发，React社区也冒出了`immutable.js`，弥补了js这门弱类型语言对数据对象比较的先天性不足，也更好地提升了性能。

在其他前端社区高速发展的时候，Angular正面临着臃肿的架构、低效的代码等沉重的历史包袱。在Angular被Google接手后，以Google员工组建的新团队对Angular现状进行了分析，做出了重写Angular的决定，并在2015年3月推出了Angular 2的预览版。

Angular 2走的是完全颠覆1.x版的激进路线，以组件化的理念全面拥抱移动端。在基于ECMAScript 2015的大背景下，吸收其他社区的精华如Flux的单向数据流，Immutable Data等,又遵循性能至上的原则进行设计。同时Angular团队也放弃自家研发的AtScript,使用微软团队的TypeScript进行主要的开发工作。

由于Angular1.x学习曲线比较陡峭，不利于新人上手，因此Angular团队在Angular2的设计中将降低复杂度与上手成本，让开发理念更加简洁，接口更加易用。在经历了长达9个月的bugfix与特性修整，Angular 2在2015年12月也迎来了它的Beta版本。在融合了这么多前沿高端的技术方案与更接地气的设计理念，可以预见Angular 2又将掀起新一波前端的大浪潮。
