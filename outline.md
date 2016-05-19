## 序1

> 梁总

## 序2

> 业界牛人，NG高手

## 前言

1. 本书的背景
> TODO

2. 本书的读者
> TODO

3. 本书的组织
> TODO

4. 致谢
> TODO

## 目录

1. 常规目录部分
2. 参考资料

## 第一部分 Angular2 入门
> 章首说明，说明NG2背景

1.1 走进前端新时代  
> TODO

1.2 Angular2 基本概念  
1.3 TypeScript语言简介  
1.4 快速上手  

> 总结：本章讲述了什么内容，通过本章内容，学习到什么，同时能带出第二章的一些内容前奏

## 第二部分 深入理解
### 1. 总览
- 讲解架构图总览图
  - 从NG2的角度讲解Module，NG2的代码都是以Module为单元构成的
  - NG2的逻辑基本单元是组件，通过Metadata去自描述，讲述组件的在NG2所处的位置。
  - 组件需要展示内容，引出模板，通过属性绑定与事件绑定与组件关联。
  - 模板需要一些独立的UI逻辑单元能复用或扩展，引导出指令。
  - 组件同样需要一些独立的业务逻辑单元复用或扩展，引导出服务
  - 这些模块如何粘合到一块，引出NG2依赖注入机制
- 介绍第二部分的总体内容
  - 各章节大致内容

### 2. 组件

================= 2016-05-20 =================

注：第一作者写作

==============================================

引文（为什么以组件为作为第一讲述，从高纬度讲述）
- 组件是编写App的基本单元
- 组件组合成App的骨架
- 引导组件到底是什么东西，它包含什么东西，它是怎么演化过来的。

================= 2016-05-30 =================
交付内容：
- 学习预研准备工作
- 引文初稿
==============================================

#### 2.1 组件化的发展
1. 先从模块化讲起，简述其开发的流程（如AMD，CMD）。
2. 提出早期模块化的不足（只关注JS部分）。
3. 当模块内聚了CSS和HTML，形成一个相对独立的逻辑单元时候，这就是组件的雏形。
4. 为什么需要组件这种内聚JS、CSS和HTML的代码组织形式，这种方式的好处是什么（复用性，提高效率，降低成本等）。
5. 针对组件标准的空白，W3C推出WebComponent标准，明确界定了组件是什么，包括其构成的4个要素。
  - 自定义标签
  - 模板
  - ShadowDom
  - 引入机制
6. WebComponent现阶段支持度不好（NG1没遵循该标准、NG2的实现更贴合标准，由此引出NG2的组件实现）。

> 注：这一节不是重点内容，控制篇幅为1k字
>
> 参考文章: 
> 
> 1. https://github.com/xufei/blog/issues/19
> 2. http://www.alloyteam.com/2015/11/we-will-be-componentized-web-long-text/
> 3. http://developer.telerik.com/featured/front-end-application-frameworks-component-architectures/
> 4. https://css-tricks.com/modular-future-web-components/

#### 2.2 NG2的组件
引文（讲述NG2与WebComponent的4个要素关系，呼应上一节）
- 自定义标签（selector）
- 模板（template）
- ShadowDom (encapsulation)
- 引入机制 (说明跟模块ES6 Module的关系)

================= 2016-06-06 =================

==============================================

##### 2.2.1 组件基本构成
- 抽取通讯录里的某一个简单的组件例子（连带bootstrap部分），然后对例子进行剖析
  - import引入依赖模块
  - @Component修饰器，简述概念原理（下一节MetaData详解里面的具体内容）
  - 组件类，封装成员变量，封装组件逻辑

##### 2.2.2 组件功能详解
- @Component的MetaData成员大家族总览（通过Demo层层深入）
- 首先从上面的例子，我们已经知道了下面这些组件功能（继续扩展讲述）
  1. selector
    - 匹配HTML中的自定义标签
    - 继续讲解selector的一些注意事项
      - 省略后变成"div"
      - 驼峰命名还是烤肉串命名
  2. template
    - 如何引用成员类的变量及函数
    - 如果想将模板外链，可通过templateUrl指定路径
    - 详情引导至第三章

================= 2016-06-13 =================

==============================================

- 继续扩展组件功能（Demo功能层层丰富）
  1. 响应用户输入
    - 组件需要根据用户输入做出不同的处理逻辑，这时候就需要用到Inputs属性
    - Demo里追加Inputs的逻辑说明
    - 可以在组件类里的『@Input()』替代（指定别名）
  2. 除了响应用户输入，通常还需要对外触发一些事件通知外界
    - 这时候需要用到outpus属性
    - Demo里追加Outputs的逻辑说明
    - 可以在组件类里的『@Output()』替代（指定别名）
    - 简述EventEmitter的作用
  3. 维护组件的样式
    - 组件需要指定样式时可通过styleUrls & styles设置
    - 与sass等预处理如何协作
  4. 引入其他依赖组件（引导至注入章节详解，本章不展开）
    - directives可引入其他依赖的组件以及指令，只对引入组件列举简单的使用例子说明，directive放到第四章再讲述
    - pipes可引入管道（引导到模板章节学习）
    - provider可引入服务等依赖（引导到服务章节说明）
  5. 组件希望引入用户自定义元素
    - 可通过ng-content实现
    - Demo追加ng-content的逻辑详细讲述
- 组件的其他功能讲述（不常用的，为了内容完整度，都说明一下）
  - host
  - viewProviders（跟『ng-content』结合一起）
  - exportAs
  - queries
  - moduleId 
  - encapsulation (shadow dom)
  - changeDetection（简单讲解用法，后面详解，结合input，output引出后面的交互和变化检测等进阶内容）

> 参考
>
> 1. 官网的例子
>
> 2. 老外的一些实践文章

================= 2016-06-20 =================

==============================================

#### 2.3 生命周期
引文
- 生命周期是什么
- 为什么需要生命周期

##### 2.3.1 生命周期的勾子（按触发顺序讲述）
- ngOnChanges（Angular设置数据绑定输入属性后的响应）
- ngOnInit（在Angular初始化数据绑定输入属性之后初始化组件/指令）
  - 跟constructor区别
- ngDoCheck（每次Angular变化检测时，跟ngOnChanges关系，触发时机的注意事项）
- ngAfterContentInit（在Angular将外部内容放到视图内之后）
- ngAfterContentChecked（在Angular检测放到视图内的外部内容的绑定后）
- ngAfterViewInit（在Angular创建了组件视图之后）
- ngAfterViewChecked（在Angular检测了组件视图的绑定之后）
- ngOnDestroy（在Angular销毁组件/指令之前的清理工作）

##### 2.3.2 路由勾子
- canActivate
- onActivate
- canDeactivate

================= 2016-06-27 =================
第一作者结束初稿
==============================================

================= 2016-05-20 =================
注：第二作者并行写作
==============================================

#### 2.4 组件交互
引文：
- 简单介绍组件交互是什么？
- 介绍组件的组织形态组件树的概念（Root Component，Parent Component，Child Component）

##### 2.4.1 父组件向子组件传送数据
- 通过input的简单例子入门讲解
- 利用input的setter和getter属性做拦截
- 实时监听数据变换（ngOnChanges，2.5节详解原理）

##### 2.4.2 子组件向父组件传送数据
- 通过output的简单属性入门讲解
- 通过local variable调用子组件的成员函数
- 使用viewChild获取子组件的引用

================= 2016-05-30 =================
注：第二作者并行写作
==============================================

#### 2.5 变动监测机制
引文：
- 介绍变动监测机制是什么
- 各种ChangeDetectionStrategy的区别

##### 2.5.1 引起变动的来源
- 事件（click，touch）
- XHR（fetch data）
- Timers（setTimeout, setInterval）

##### 2.5.2 变动通知机制
- 介绍zone原理
- 稍微深入介绍zone（from dr.Li）

================= 2016-06-06 =================

==============================================


##### 2.5.3 变动响应处理
- 2.4小节已描述过，这里简单带过即可
- 组件树自顶向下对变动事件的传递
- 单个组件内的处理流程

##### 2.5.4 性能分析
- 使用immutable机制提升响应精准度，减少触发次数
- 根据组件场景选择不同的ChangeDetectionStrategy可提升性能。
- 手动改变ChangeDetection的状态（使用ChangeDetectorRef）

> 参考点
> - http://blog.thoughtram.io/angular/2016/02/22/angular-2-change-detection-explained.html


#### 本章总结
- 完整Demo例子
- 回顾本章中心内容
- 列举关键知识点

================= 2016-06-13 =================

==============================================

### 3 模板
- overview todo...

#### 3.1 插值(Interpolation)  简单的代码示例展示插值的实现方式，顺带提一下插值中表达式和如何运用宿主组件中的函数，以此来引出下面两小节

- 3.1.1 模板表达式（Template expressions）

    - 如何定义一个模板表达式
    - 与JavaScript表达式类比，列出哪些是不合法的模板表达式
    - 在模板表达式中如何引用成员变量，讲解其作用域范围
    
- 3.1.2 模板声明（Template statements） 参考初稿对应章节.

#### 3.2 数据绑定（Binding syntax）
##### 3.2.1 数据绑定概览

- 讲述数据绑定在Angular2中的作用于意义
- 根据数据的流向列出数据绑定的三种类型，从数据流向、语法和绑定类型三个维度说明
- 以绑定类型的维度，列出属性、事件、双向、HTML元素属性、类和样式绑定的绑定target，加上示例代码

##### 3.2.2 属性绑定（Property binding）
- 介绍属性绑定的定义，应用场景，结合简单的代码示例展示属性绑定的用法
- 3.2.2.1 单向数据流
    - 讲述清楚属性绑定数据的流向
- 3.2.2.2 属性绑定的中括号&绑定目标
    - 讲述清楚[]和bind-两种绑定形式，最好结合代码示例来表述，并说明绑定目标
- 3.2.2.3 避免副作用
    - 举出一些会出现副作用的例子，如不能使用属性绑定表达式做赋值操作，也不能使用增量操作符和修饰符，进一步引出Angular2中如何使用才会更优，如保证属性绑定的值和调用的方法仅仅是为了返回值，而不是完成其他的操作，或者确保返回正确的数据类型
- 3.2.2.4 插值和属性绑定的区别与联系
    - 先抛出Angular2在处理插值时会首先把插值转换成相对应的属性绑定，然后从技术角度说明没有所谓的孰优孰劣，建议开发者开发中使用其中一种开发规范即可
- 3.2.2.5 属性绑定的扩展 包括HTML元素绑定, class属性绑定,style绑定，都需要给出相应的代码示例
    - HTML元素绑定 指出没有对应DOM对象属性的html元素，给他们插值会行不通。标注attr.的方式来实现HTML属性绑定
    - class绑定 类比一下用class和class属性绑定，重点突出class绑定是用来重设特殊的class，说明class属性绑定的用法，即class.xx
    - style属性绑定 讲述style属性绑定如何设置内联样式

##### 3.2.3 事件绑定
- 介绍事件绑定的定义，应用场景，结合简单的代码示例展示属性绑定的用法
- 3.2.3.1 事件目标
    - 用简单的伪代码介绍小括号之间的名字标识目标事件，顺带on-的方式来绑定事件等
- 3.2.3.2 $event对象和事件处理表达式
    - 介绍`$event`对象，要讲述模板声明中的事件信息和`$event`的联系等
    - $event就是一个DOM事件对象，介绍其target属性
    - 最好有例子
- 3.2.3.3 自定义事件
    - 围绕EventEmitter对象展开，包括指令发起自定义事件，讲述该指令如何触发一个事件，结合实例代码给出

##### 3.2.4 双向绑定 -  two-way data binding, change tracking
> todo 需要参考组件部分，避免内容重叠

##### 3.2.5 输入和输出属性（Input and output properties）从下面两方面介绍
- 什么是输入输出属性 
- 输入输出属性的别名

#### 3.3 局部模板变量（Template reference variables）
##### 3.4.1 作用域
##### 3.4.2 NgForm和模板局部变量  主要是如何运用

#### 3.4 内置指令
- overview 模板内置指令在Angular中发挥的作用，起到引入的作用.
- 3.4.1 NgClass
    - 类比一下class属性绑定，用伪代码来引出NgClass方法的使用，绑定一个key-value对象的组件方法
- 3.4.2 NgStyle
    - 同上
- 3.4.3 NgIf
    - 如何在模板中使用NgIf，更深入一点，用class属性绑定的其它方法也可以达到相同的效果，如class.hidden
- 3.4.4 NgSwitch
    - 在模板中NgSwitch如何使用
- 3.4.5 NgFor
    - 在模板中NgFor如何使用，说明白指令是如何循环的，对NgFor中的模板变量捎带讲一下，特别地讲解它的索引-index

#### 3.5 表单
- overview 直接用模板章节中的概述即可

##### 3.5.1 Template-Driven Forms 讲述表单组件类和表单模板
##### 3.5.2 表单指令
- NgForm - 指令依赖声明 & 局部变量
- NgControl - 从NgControl的运用来讲 包括Track change-state & validity
- NgModel - NgModel的运用、NgModel双向绑定原理【TODO ？？】 
- NgSumit

##### 3.5.3 用户自定义css （Add Custom CSS for Visual Feedback）
- ng-touched
- ng-dirty
- ng-valid

##### 3.5.4 表单验证（Validation） -  more...such as custom validator

#### 3.6 管道（pipes）

- overview 讲解什么是管道，管道的应用场景即可

##### 3.6.1 管道的用法 - eg.Parameterizing a Pipe & Chaining pipes
##### 3.6.2 管道的内置方法 管道的内置方法怎么使用，列举一下的内置指令
- DatePipe
- JsonPipe
- UpperCasePipe
- LowerCasePipe
- CurrencyPipe
- PercentPipe
- SlicePipe

##### 3.6.3 自定义管道(Custom Pipes)
- 声明元数据
- 实现transform方法

##### 3.6.4 管道状态
- 无状态的管道
- 有状态的管道
- 管道无状态和有状态的区别

#### 3.7 模板操作符（Template expression operators）
##### 3.7.1 pipe操作符（|）
##### 3.7.2 Elvis操作符(?.)

#### 3.8 Summary
- todo

### 4. 指令（8k字）
引文：
- 呼应组件章节，指令和组件实际上有点相似的，区别在哪里呢？，由此引入本章内容

#### 4.1 指令概述
- 指令的概念
- 指令的作用，逻辑复用

##### 4.1.1 指令分类
- 属性指令及其定义（列举对应内置指令，如NgStyle，NgClass）
- 结构指令及其定义（列举对应内置指令，如NgIf，NgFor）
- 组件
  - 呼应组件章节
  - 二者的区别是什么（是否带模板）
  - 前面的组件的特性如一些MetaData，生命周期等都适用于指令

##### 4.1.2 集合指令简述
- COMMON_DIRECTIVES
- CORE_DIRECTIVES
- FORM_DIRECTIVES
- PLATFORM_DIRECITVES
- ROUTER_DIRECTIVES

#### 4.2 属性指令
- 从通讯录quickstart里抽离一个简单的属性指令例子（包括在模板如何引入使用）
  - 简述@Directive修饰符（与@Component比对）
  - 简述指令类（跟组件类似）
  - ElementRef对DOM元素的引用
- 属性指令继续深入
  - 获取输入参数（Input）
    - Demo追加Input逻辑讲解
  - 响应用户事件（host）
    - Demo追加host逻辑讲解

#### 4.3 结构指令
- 从通讯录quickstart里抽离一个简单的结构指令例子（包括在模板如何引入使用）
  - @Directive和指令类与属性指令相同
  - 简述TemplateRef和ViewContainerRef作用
- 结构指令继续深入
  - 详细介绍"Template"标签机制
  - 详细介绍"*"的作用
- 结合上面的解释，分析ngIf原理

#### 本章总结
- 完整Demo例子
- 回顾本章中心内容
- 列举关键知识点


### 5.服务

#### 5.1 服务介绍

##### 5.1.1 什么是服务  
- 简单描述什么是服务，服务在系统中的作用：服务为系统提供了基础功能，通过独立的接口跟功能给外部调用  

##### 5.1.2 NG2中的Service（Injectable）  
- 描述NG2中的服务概念：介绍内置service（http等）跟自定义service（每个class都    可以是一个单例可服用的服务，通过@Injectable()注解标示，component可直接 注入）  

##### 5.1.3 NG2中的service跟NG1中的service   
- 对比NG2跟NG1关于service的区别：  
                NG1：factory，service，provider                         
                NG2：class  

#### 5.2 Http  

##### 5.2.1 Http client介绍 （1000字内）  
- 介绍客户端与服务端通讯的方式：XHR，JSONP，Fetch  
- 介绍NG2中的http服务  

##### 5.2.1 结合通讯录例子编写用http模块实现的例子 （详细，step by step）  
- 编写从服务端获取通讯录列表并展示在ui中例子  

###### 5.2.2 Http与observable  
- 带一下NG2中的返回obserable对象  

#### 5.3 响应式编程  //TODO:（可以把第九章的响应式编程搬过去）  

##### 5.3.1 什么是响应式编程  

##### 5.3.2 为什么要响应式编程  

#### 5.4 Rxjs  

##### 5.4.1 什么是rxjs  
- 响应式编程的js实现，观察者模式的改写  
- 介绍rxjs开发的套路，具体包含几部分 
- Rx.Observable.create()  
- Rx.Observer.create()  
- subscribe()    

##### 5.4.2 rx操作符  
- 介绍rx操作符的工作流程，结合珠宝图（简单即可，毕竟这不是rxjs的书）  
- NG2中常用的几种即可，包括map(结合http)，fromevent(用click事件作为例子)  
- 普通数据类型跟observable对象的转换：使用from转换，用to还原  

##### 5.4.3 NG2中rxjs  
- 描述NG2中如何使用rxjs（rxjs过于庞大，ng2只使用简约版）  
- 结合通讯录例子中的通讯列表讲解NG2中rxjs，根据官网的例子改造即可  

##### 5.4.4 observble 与 promise  
- promise只是obserable的弱化版，用toPromise(success, fail)可简单实现转化  
- 用通讯录例子改造成promise（可参照官网的例子）  

##### 5.4.5 jsonp  
- 简单介绍jsonp  
- 改造通讯录例子，用jsonp方式实现（参照官网即可）  

#### 5.5 总结

references：  
https://angular.io/docs/ts/latest/guide/server-communication.html#!#rxjs  
https://angular.io/docs/ts/latest/tutorial/toh-pt4.html  
https://docs.angularjs.org/guide/services   
http://www.tutorialspoint.com/angularjs/angularjs_services.htm  
http://reactivex.io/rxjs/  


### 6 依赖注入  

#### 6.1 什么是依赖注入  
- 阐述软件设计中依赖注入这种设计模式  
- 大型OO框架必备，面向接口编程  
- 解耦，工厂模式的升华  

#### 6.2 Angular2中的依赖注入   

##### 6.2.1 为什么需要依赖注入  
- angular的最大亮点  
- 组件（服务）间很方便相互调用  
- 方便单元测试编写  
- 结合通讯录的产品设计一个例子，一步一步解释依赖注入以及介绍必要性（目前的版本已经不错，改造为统一的通讯录例子即可）  

##### 6.2.2 Angular2跟Angular1依赖注入对比  
- Angualr1中依赖注入存在问题  
- Internal Cache(内建缓存)：依赖一般是被当做单例对待，任何一个服务在整个应用的生命周期中都应该只被创建一次。
- Synchronous by default(默认异步)：Angular 1中的服务创建不是异步创建的。
- Namespace collision(命名空间冲突)：在应用的生命周期中某个”type”的token是唯一的，如果我们自定义了一个名为Car的服务，而引入的第三方框架中也存在着同名的Car的服务，那么整个系统就会存在问题  
- Built into the framework(框架内建)：Angular 1的依赖注入是内建的，我们无法单独的进行使用。  
- Angular2的依赖注入是一个完全的重写，解决了NG1中存在的痛点  

##### 6.2.3 Angular2中依赖注入几个定义  
- Injector(注入器)：Injector就类似于Spring里面的ApplicationContext，提供了一						系列的接口以供依赖实例的创建。  
- Binding(绑定)：Binding的作用在于告诉Injector如何去为某个依赖创建实例。一个					Binding需要映射到一个工厂类型的方法。  
-	Dependence(依赖)：一个Dependence是某个对象被创建的类型。  

#### 6.3 Angular2中如何使用依赖注入  

##### 6.3.1 组件注入Service：结合通讯录实现一个简单的组件依赖注入demo，参照官网的实现步骤 
- 结合例子如何注入：通过bootstrap全局注入或在组件中通过provider注入，组件的构造函数可以直接获取singleton实例（angular在看到构造函数的参数时，会去组件的metadata中找prodiver，匹配后初始化一个单一实例，【**这里先不要去讲层级注入，先让读者浅显易懂即可，可以提到后面会讲层级注入**】）  
- Angular2的注入实现讲解

##### 6.3.2 Service注入Service: Service依赖另一个service时候如何实现注入，可参考官网结合通讯录的场景设计一个demo!

##### 6.3.3 介绍optional injection：Ng2中如何实现可选的依赖注入  

### 6.4 Provider  

##### 6.4.1 什么是provider  
- provider提供了一个运行时的注入  
- 注入器根据provider初始化实例  

##### 6.4.2 provider使得NG2的注入灵活，解耦 ![](media/14628038696047/14628087058882.jpg)￼  

##### 6.4.3 介绍几种provider：![](media/14628038696047/14628088565501.jpg)￼  

##### 6.4.4 provider声明依赖项：![](media/14628038696047/14628090445630.jpg)￼  

#### 6.5 层级注入  

##### 6.5.1 注入树介绍  
- 组件树的每个层级都可独立注入，都是单例
- 注入的冒泡查找，从当前组件冒泡到bootstrap

##### 6.5.2 结合通讯录例子demo  
- 在不同层级注入同一个service，证明分别是独立  

##### 6.5.3 对比在各层级注入的应用场景  
- 在组件，父组件，根组件，bootstrap这几个地方注入的对比  

#### 6.6 总结


### 7 路由（router）
#### 7.1 Overview
- 初探路由，简单讲述路由的定义
- 路由的应用场景，结合路由在单页应用中的导航模式简单的讲述即可

#### 7.2 路由的基本概念
- 一个表格列出ng2所有的关于路由的相关概念，可以参考官网或者初稿中对应的内容
- 分三个小结，进一步讲述这些基本概念，讲述内容包括
    - 路由的配置 -  routerConfig ，列出demo示例代码，讲述如何定义一个RouterConfig数组
    - 讲述具体参数的用途和定义，如 path、name、component、useAsDefault等
    - 讲述路由的两种使用情况可以参考：![](https://github.com/JTangming/tm/blob/master/images/25.pic.jpg?raw=true)
    
- 视图的渲染 - RouterOutlet 说明RouterOutlet指令的用途即可
- 组件间的导航 - RouterLink，可以直接参考初稿的相应内容

#### 7.3 路由的基本用法
- 讲述具体的应用流程即可，结合我们的路由demo，按以下路径来阐述路由的用法

>
##### 加载路由库
##### 设置base href
##### 注入ROUTER_PROVIDER
##### 定义路由表

#### 7.4 路由参数
- 路由参数的传递 ， 说明路由参数船体的几种方式
    - 通过路由传递参数
    - 在模板中传递
    - 在组件中传递

- 路由参数的接收

#### 7.5 子路由组件
- 介绍子路由的使用场景及其优越性
- 子路由的使用，包括两方面，均要以我们的路由demo进一步扩展，结合代码示例进一步说明
    - 父路由组件的定义
    - 子路由的定义

#### 7.5 路由的生命周期
- 由组件的生命周期对比性的引入路由的钩子方法
- 具体介绍RouterCanDeactive，包括暂停、确认和取消导航
- 一小段文字概括路由的生命周期


#### 7.3 Summary
> todo


### 8 测试 4-5千字
#### 8.1 Overview
- 交待需要测试的背景，对angular当前的测试技术做个预览或者对比
- 阐述测试技术及其实践的必要性
- 常用的测试技术有哪些？ -unit test & e2e test
    - unit test&e2e test的基本概述、responsibility、介绍技术流、使用的场景

#### 8.2 Unit testing
##### 8.2.1 单元测试
- 介绍什么是单元测试 what？
- 单元测试引用场景，剖析单元测试要解决什么问题 why？
- 常用的单元测试方案及技术简介 What testing framework should I use?

##### 8.2.2 单元测试技术选型  本节预选Jasmine & Karma作为unit test的技术支持，需要从下面几方面来介绍
- Karma简介
- Jasmine简介及Jasmine常用api 主要介绍describe，it语法，结合几个简单的例子介绍一下beforeEach、Expectations如toBe、toEqual等

##### 8.2.3 一个基于karma+Jasmine的单元测试例子
- 介绍karma+jasmine的配置
    - 所需的依赖（Installation)
    - 环境配置搭建等（Configuration,如：karma.conf.js）
- 如何写测试用例，具体可参考官网
- 编写测试例子 需要覆盖Testing a Controller、Testing Filters、Testing Directives、Testing Promises的例子

##### 8.2.4 编写第一个typeScript测试 
- 搭建所需的依赖 Dependencies & Installing
- 准备好typeScript Configuration 如tsconfig.json
- 从quickStart中挑选demo来编写测试用例，需要涵盖 component test、Asynchronous Service
- 导入测试模块
- 运行测试代码
- 如何Debug测试 可从具体的一写tips写起

可参考：
- http://karma-runner.github.io/0.12/intro/installation.html
- https://github.com/karma-runner/karma-jasmine
- https://blog.logentries.com/2015/01/unit-testing-with-karma-and-jasmine-for-angularjs/
- http://jasmine.github.io/edge/introduction.html
- https://docs.angularjs.org/guide/unit-testing
- https://github.com/AngularClass/angular2-webpack-starter

#### 8.3 e2e test（简单介绍即可）
- e2e test简介
- 讲述如何搭建一个具体的e2e测试的环境
- 通过简单的例子，注明e2e如何跑起来
- 相关总结

#### 8.4 Summary
- 回顾本章核心内容
- 罗列本节关键知识点
- 为第三部分做个引出


## 第三章 实战

9.简单的问卷调查系统

9.1 案例背景

9.1.1 关于问卷服务 

简单的介绍问卷服务的内容及其实际用途等（体现案例的实际意义）。

9.1.2 模仿的产品 - 腾讯问卷

简单类比下已经存在问卷种类，重点介绍下腾讯问卷，并且从易用性和功能性两个方面说明选择模板腾讯问卷的原因。（给出腾讯问卷的截图）

9.2 产品功能和设计

产品共包括四个主要模块，本节将从功能和设计两个方面介绍每个模块的功能。

9.2.1 主页面/帮助说明

主页面的主要功能点是导航菜单，简单介绍下每个菜单项及使用帮助；另外一个就是轮询图片（美化效果）。（给出首页截图）

9.2.2 创建/编辑问卷

创建和编辑问卷的功能介绍和设计说明。（给出截图）

9.2.3 我的问卷

问卷展示列表和信息统计的功能介绍和设计说明。（给出截图）

9.3 项目实施

9.3.1 使用技术

罗列项目中使用到的技术（rx.js，immutable.js，json-server等）

9.3.2 配置 & 启动

介绍环境配置、基础依赖等，项目启动的步骤。

9.3.3 组件拆解

通过组件树完成对项目各个模块组件的拆解。

9.3.4 数据建模

依据上节中对组件的拆解说明，引出我们预定义的数据结构，核心的数据类型主要包括问题和问卷两种，对每个属性做简要说明。

9.4 组件开发

本节依据组件树和定义好的数据结构为基础，以模块为分类，阐述组件的开发过程。每部分都将贴出代码和截图。

9.4.1 主页面/帮助说明

介绍主页和帮助页面的代码，重点介绍项目的一些初始化配置以及json后台。（http，router等）

9.4.2 创建/编辑问卷

核心代码部分，首先说明问题操作组件和问题大纲组件，并由此引出四类问题组件（单选，多选，文本，分值）。接下来讲解问卷组件（组件内容，状态管理，子组件状态管理）。

9.4.3 我的问卷

介绍我的问卷模块涉及到的详情组件，功能组件和单个问卷项组件。统计简单的介绍下信息统计功能。 我们把发布页面也放到此小节中。

## 参考资料
> TODO
