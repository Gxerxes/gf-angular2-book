##1.3.1 什么是Typescript?
TypeScript是一种由微软开发的自由和开源的编程语言。它是**ES6**的一个超集，所以也是**JavaScript**的一个超集，本质上是向JS语言添加了可选的静态类型和基于类的面向对象编程。
Javascript是一种弱类型的语言，这种简单粗暴的编写模式随着前端在软件开发的地位增强而显得越发无力。类型检查，面向对象，泛型，模块化等这些服务端玩了几十年的语言功能，对前端开发者来说是时候享受这些特性带来的乐趣了，Typescript正是提供了这个魔术棒，让开发者们遨游在面向对象开发的世界里，虽然最后还是编译成目前浏览器所能识别的JavaScript代码。
** 如果有很多js代码，项目中不好上手怎么办？**
虽然typescript给了你type的能力。不意味着给了你太多的限制。
1. 它支持自动类型推断。一些很明显的类型，编译器可以智能推断出来，比如。**var x = 1;**
2. 好在它的类型是可选的。你完全可以全都写any类型。编译器会对该变量放弃类型检查。
即使类型匹配失败，仍然会生成javascript。你可以逐渐把js代码慢慢迁移到typescript上。

##1.3.2 基本类型

Typescript提供了boolean, number, string, array, tuple,enum, any, void几种基本类型。

### 布尔值

最简单的数据类型，值为true/false，在Typescript中类型名为boolean

    ```typescript
    let flag: boolean = true;
    ```
### 数字

Typescript的数字都是浮点类型，也支持ECMScript2015中的二进制跟八进制字面量。
    
    ```typescript
    let decLiteral: number = 6;
    let hexLiteral: number = 0xf00d;
    let binaryLiteral: number = 0b1010;
    let octalLiteral: number = 0o744;
    
    var flag: boolean = true;
    var s: string = 'hello';
    var n: number = 123;
    
    enum Color {Red = 1, Green, Blue};
    var color: Color = Color.Green;
    
    function log(msg: string): void {
    	console.log(`${new Date().toUTCString()} ${msg}`);
    }
    ```
### 字符串 

跟JavaScript中的字符串一样，用单引号（'）或双引号（“）隔开，另外，Typescript还支持C#等常用的模板字符串,可以定义多行文本和内嵌表达式，用反引号（`）以 ${ expr } 方式嵌入。类似C#中的String.format，在处理拼接字符串的时候很有用。

    ``` typscript
    let name: string = `GF Security`;
    let years: number = 25;
    let words: string = `你好, ${ name }.
    								今年是成立 ${ years + 1 } 周年了.`;
    ```

### 数组

跟JavaScript操作数组一样，typescript有两种方式可以定义。

    ``` typescript
    	let array:  number[] = [1,2];
    	let arrayList: Array<number> = [1,2];
    ```

### 元组

元组类型可以创建一个指定数量跟类型的数组，类型可以不相同，比如可以把年龄跟名字放在同一个元组内。

    ``` typescript
    	let x: [string, number];
    	x = ['广发证券', 25]; // OK
    	x = [10, '广发证券']; // Error
    ```

### 枚举

enum 类型是对JavaScript类型的一个补充，像c语言等其它一样，用enum可以为一个数组赋予有意义的名字，增强可读性。

    ``` typescript
    	enum Color {Red, Green, Blue};
    	let c: Color = Color.Green;
    ```
同c语言等一样，默认下标是0，可以手动修改默认下标值。

    ``` typescript
    	enum Color {Red = 1, Green, Blue};
    	let c: Color = Color.Green;
    ```
### 任意值
任意值是typescript针对数据类型不明确的时候可使用的一种类型，这可能是来自动态内容，也可能是第三方库导出，any能跳过编译阶段的类型错误检查。

    ``` typescript
    	let notSure: any = 4;
    	notSure = "maybe a string instead"; // string
    	notSure = false; // boolean
    ```
### 空值
void表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是void,跟C#等语言一样：

    ``` typescript
    function hello(): void {
    alert("helloworld");
    }
    ```

##1.3.3 类

类的语法和ES6的Class类似，有constructor，可以继承。这里列举几点不同。

### 属性声明
ES6的class属性是直接赋值给this.varName声明的，typescript里面需要显示声明。
    ```typescript
    class Point{
    	x: number;
    	y: number;
    }
    ```
### 构造函数属性声明
属性也可以在构造函数中添加public, private描述声明。
    ```typescript
    class Point{
    	constructor (public x:number, public y:number){}
    }
    ```

### 支持public, private, static描述
ES6的static只支持在函数上声明，而typescript支持方法和属性。

    ```typescript
    class Popup{
    static inst: Popup;
    constructor() {
    if (!Popup.inst) {
    Popup.inst = this;
    }
    }
    static getInstance() {
    return new Popup();
    }
    }
    
    Popup.getInstance();
    ```

##1.3.4 函数

- 可选/默认参数

    	```typescript
    	function reset(hard?: boolean) {
    		if (hard) {
    			resetDB();
    		}
    		resetUI();
    	}
    	reset();
    	reset(true);
    	```

- 剩余参数

	可变数目的参数需要使用剩余参数的写法。获得的参数将是一个数组。

	    ```typescript
    	function max(...nums: number[]) {
    		...
    	}
    	```

- 箭头函数

	这点和ES6一致。箭头函数内部保持和外部一样的this上下文。
    
    	```typescript
    	var Scheduler = {
    		queue: [],
    		schedule(t: Task) {
    			setTimeout(()=> {
    				this.queue.push(t);
    			}, 0);
    		}
    	};
    	Scheduler.schedule(new Task());
    	```

- 重载

	js函数支持不同的参数进行重载。例如jquery的css函数
    
    	```typescript
    	css({
    		width: '100px'
    	})
    	css('width', '100px')
    	```

	可以这样调用。我们可以为该函数声明重载。

    	```typescript
    	function css(config: object);
    	function css(config: string, value: string);
    	function css(config: any, value?: any) {
    		if (typeof config == 'string') {
    			...
    		} else if (typeof config == 'object') {
    			...
    		}
    	}
    	```
	这个函数有两个重载，编译器会判断参数类型是否符合其中一个。

- 装饰器(decorator)

	Typescript的装饰器和ES6里面的一致。可以修改已有的类或类的方法，也可以在它们的基础上提供一层封装。
	Angular2里面大量使用装饰器，为组件注册元数据。

	1. 类的装饰器

	我们先来看看类的装饰器，以下面类的装饰器为例：

	    ```typescript
    	@decorator
    	class A {}
    	```
    
	这段代码其实等同于

	    ```typescript
    	class A {}
    	A = decorator(A) || A;
    
    	function decorator(klass) {
    		klass.meta = 'my awesome class';
    	}
    	```

	Angular里面的装饰器可以传入meta信息，如下：

	    ```typescript
    	@Component({
    		selector: 'my-app'
    	})
    	class MyApp {
    
    	}
    	```

	Component其实是angular库里面实现的一个装饰器工厂，接受一个meta信息，返回一个装饰器。类似如下实现：

	    ```typescript
    	function Component(meta) {
    		return function (klass) {
    			...
    		};
    	}
    	```

	2. 类的方法的装饰器。

	还有一种装饰器是类的方法的装饰器。

    	```typescript
    	class Person {
    		@readonly
    		name() { return `${this.first} ${this.last}` }
    	}
	```

	以上readonly方法将被如下的方式调用。

    	```typescript
    	function readonly(target, name, descriptor){
    		descriptor.writable = false;
    		return descriptor;
    	}
    
    	readonly(Person.prototype, 'name', descriptor);
    	// descriptor对象的初始值如下
    	// {
    	//   value: oneFunction,
    	//   enumerable: false,
    	//   configurable: true,
    	//   writable: true
    	// };
    	```
	
	3. 函数的装饰器呢？
	可惜的是由于函数存在提升，没有函数的装饰器。


##1.3.5 模块
Typescript模块包括内部模块和外部模块两种。

### 内部模块
内部模块创建一个封闭的作用域，供同一个js文件内的代码使用。
(也可以使用 **/// <reference path="utils.js"/>** 引入其他文件的内部模块。)
    
    ```typescript
    module com.gf.Utils{
    	export function foo(msg:string){
    		alert(msg);
    	}
    	export var name = 'some random tools';
    }
    
    import Utils = com.osamu.Utils; // alias
    Utils.foo('hi')
    Utils.name = 'Jack';
    ```

### 外部模块

外部模块和ES6的模块类似。使用外部模块和文件夹结构，保持合理的组织结构是大型项目必备的。
编译时可以为 *--module* 参数提供 *commonjs*, *amd*, *umd*, *systemjs* 几个值，选择编译为几种模块格式，供不同的加载器使用。
    ```typescript
    // mylib.ts
    export function log(msg){
    	console.log(msg);
    }
    
    // app.ts
    import {log} from 'mylib';
    log('Hello, world!');
    
    // 可以使用 `tsc --module amd main.ts` 编译
    ```
    
##1.3.6 接口

typescript和其他解释性语言采取了类似的类型系统，duck typing。它听起来像鸭子看起来像鸭子就是鸭子。
而这个类型有可以由接口来描述。它强大到可以描述js内一切东西。
    
    ```typescript
    interface Name {
    first: string;
    second: string;
    }
    
    var name: Name;
    name = {
    first: 'Jim',
    second: 'Raynor'
    };
    
    name = {   // Error : `second` is missing
    first: 'Jim'
    };
    name = {   // Error : `second` is the wrong type
    first: 'Jim',
    second: 1337
    };
    ```
第二个和第三个name对象由于却少相应的属性抛出类型不匹配的错误。


### 更多接口描述
Interface可以支持更为复杂的对象描述，如：

    ```typescript
    interface FooType {
    	(arg: string):void;	// 可以被当作函数调用 myFunc('hello');
    	new (): Object; // 可以被当作构造函数 new myFunc();
    	[idx:number]:string; // 支持下标 myFunc[3];
    	name: string; // 支持属性 myFunc.name
    	name?: number; // 可选属性
    	id: string|number // 属性可以是某一种类型
    	innerFunc():void; // 成员函数 myFunc.innerFunc();
    
    };
    
    ```

### type别名
类型可以通过type关键字声明别名，比如：

    ```typescript
    type StrOrNum = string|number;
    type Record = [number, string];
    ```

### 周围声明
使用Typescript的项目如果需要整合大量已经存在的js代码，需要相应的js库的 *.d.ts* 类型定义文件。

并在引用的文件中声明类型依赖。

    ```typescript
    /// <reference path="node.d.js"/>
    ```

实在太懒的话，也可以使用

    ```typescript
    declare var process:any;
    ```
使typescript放弃对外部依赖库的类型校验。

很多常见的库的.d.ts文件开源项目DefinitelyTyped上人已经贡献了，详见下章。

##1.3.7 泛型(Generic)

泛型是为了提升代码的复用性而开发的，与Java，C#中的泛型类似。
比如我们有个最小堆算法，需要同时支持number和string。这样可以把集合类型改为any。这样就完全放弃了类型检查。
这样实现有很大的瑕疵，而使用泛型解决更为优雅。
我们可以声明一个最小堆适用于number类型 *new MinHeap<number>()* ，
然后声明一个最小堆适用于string类型 *new MinHeap<string>()* 。
类似如下的泛型类：

    ```typescript
    class MinHeap<T> {
    list: T[] = [];
    add(element: T): void {
    		...
    }
    min(): T{
    return this.list.length ? this.list[0] : null;
    }
    }
    
    var heap1 = new MinHeap<number>();
    heap1.add(3);
    heap1.add(5);
    console.log(heap1.min());
    
    var heap2 = new MinHeap<string>();
    heap2.add('a');
    heap2.add('c');
    console.log(heap2.min());
    ```

泛型也支持函数。下面zip函数声明了两个泛型类型`T1` `T2`，并把两个数组压缩到一起。

    ```typescript
    function zip<T1, T2>(l1: T1[], l2: T2[]): [T1, T2][] {
    var len = Math.min(l1.length, l2.length);
    var ret = [];
    for (let i = 0; i < len; i++) {
    ret.push([l1[i], l2[i]]);
    }
    return ret;
    }
    console.log(zip<number, string>([1,2,3], ['Jim', 'Sam', 'Tom']));
    ```

##1.3.8 Typescript工具
### tsconfig.json
tsc编译器有很多命令行参数，但是都写在命令行上十分繁琐。于是有了 *tsconfig.json* 文件。
当运行 *tsc* 时，编译器从当前目录向上搜索 *tsconfig.json* 文件加载配置，类似于 *package.json* 文件的搜索方式。

我们可以从一个空的tsc文件开始。

    ```json
    {}
    ```
tsc有合理的默认设置，空的json运气好的话也work。
下面是一个更为复杂的angular环境用的tsc配置。

    ```json
    {
      "compilerOptions": {
    "target": "ES5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
      },
      "exclude": [
    "node_modules"
      ]
    }
    ```

###DefinitelyTyped
在使用第三方非typescript开发的库的时候，会需要 *.d.ts* 外部接口描述文件。
幸运的是很多这样的描述已经被开发了，并开源在 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
可以使用tsd工具，方便的安装.d.ts文件。
首先安装tsd工具
    
    ```bash
    npm install tsd -g
    ```

然后安装 *d.ts* 文件
    ```bash
    tsd install jquery --save
    ```

###编辑器
typescript可以有非常强大的类型提示。官方推荐VS作为typescript的编辑器，可惜VS对前端开发童鞋实在不习惯。
喜欢IDE的可以试试WebStorm或atom。atom的插件 [atom-typescript](https://atom.io/packages/atom-typescript) 很不错。


