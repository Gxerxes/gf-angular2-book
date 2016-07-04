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

## 1.3.3 类

传统的JavaScript程序使用函数和基于原型的继承来创建可重用的组件。 在TypeScript里，可以使用基于类的面向对象方法,并且编译后的JavaScript可以在所有主流浏览器和平台上运行。所以TypeScript对于用惯了面向对象方式的程序员来说来说相当友好。

### 类的说明

下面看一个使用类的例子。

    ```typescript
    class Car {
	    engine: string;
	    constructor(engine: string) {
	        this.engine = engine;
	    }
	    drive(distanceInMeters: number = 0) {
	        return "A car runs ${distanceInMeters}m  powered by" + this.engine;
	    }
	}

	let car = new Car("petrol");
    ```
上面声明一个Car类。这个类有3个成员：一个叫做engine的属性，一个构造函数和一个drive方法。注意到Car的属性engine，它表示我们访问的是类的成员。

let car = new Car("petrol")使用new构造了Car类的一个实例。 它会调用之前定义的构造函数，创建一个 Car类型的新对象，并执行构造函数初始化它。

### 继承
熟悉面向对象的人都了解，讲到类，肯定要提继承的，基于类的程序设计中最基本的模式是允许使用继承来扩展一个类。

看下面的例子。

    ```typescript
	
	class MotoCar extends Car {
    	constructor(engine: string) { super(engine); }
	    drive(distanceInMeters = 50) {
	        console.log("motoCar...");
	        super.move(distanceInMeters);
	    }
	}
	
	class Jeep extends Car {
	    constructor(engine: string) { super(engine); }
	    drive(distanceInMeters = 100) {
	        console.log("Jeep...");
	        super.move(distanceInMeters);
	    }
	}
	
	let tesla = new MotoCar("electricity");
	let landRover: Car = new Jeep("petrol");
	
	tesla.drive();
	landRover.move(200);
    ```
 
从上面的例子可以看到：MotoCar和Jeep 类是基类Car的子类，用extends来创建子类。并且子类可以访问父类属性和方法。

同时例子也说明了如何在子类里可以重写父类的方法。 MotoCar和Jeep都创建了drive方法，重写了从Car继承来的drive方法，使得drive方法根据不同的类而具有不同的功能。 注意，即使landRover被声明为Car类型，它依然是个Jeep，landRover.move(200)调用Jeep里的重写方法;包含constructor函数的派生类必须调用super()，它会执行基类的构造方法。

### 公共，私有、受保护的修饰符和参数属性

**默认为公有public**

在上面的例子里，我们可以自由的访问程序里定义的成员,是因为在TypeScript里，每个成员默认为 public的。把上面的Car类加上public后，
如下所示：

    ```typescript
    class Car {
	    public engine: string;
	    public constructor(engine: string) {
	        this.engine = engine;
	    }
	    public drive(distanceInMeters: number = 0) {
	        return "A car runs ${distanceInMeters}m  powered by" + this.engine;
	    }
	}
    ```
**private**

当成员被标记成private时，它就不能在声明它的类的外部访问。比如：

    ```typescript
    class Car {
    	private engine: string;
	    constructor(engine: string) {
	        this.engine = engine;
	    }
	}

	new Car("petrol").engine; // Error: 'engine' is private;
	```

**protected**

protected修饰符与private修饰符的行为很相似，但有一点不同，protected成员在派生类中仍然可以访问。例如：

    ```typescript
	 class Car {
	   	protected engine: string;
	   	constructor(engine: string) {
	        this.engine = engine;
	    }
	    drive(distanceInMeters: number = 0) {
	        return "A car runs ${distanceInMeters}m  powered by" + this.engine;
	    }
	}
	
	class MotoCar extends Car {
    	constructor(engine: string) { super(engine); }
	    drive(distanceInMeters = 50) {
	        console.log("motoCar powered by"+this.engine );
	        super.move(distanceInMeters);
	    }
	}
	
	
	let tesla = new MotoCar("electricity");
	console.log(tesla.drive());
	console.log(tesla.engine);

    ```
注意，不能在Car类外使用engine，但是仍然可以通过MotoCar类的实例方法访问，因为MotoCar是由Car派生出来的。

**参数属性**

参数属性通过给构造函数参数添加一个访问限定符来声明。 使用 private限定一个参数属性会声明并初始化一个私有成员；对于public和protected来说也是一样。参数属性可以方便地让我们在一个地方定义并初始化一个成员。 下面的例子是对之前 Car类的修改版，使用了参数属性：

   	```typescript
	 class Car {
	    constructor(protected engine: string) {}
		drive(distanceInMeters: number = 0) {
	        return "A car runs ${distanceInMeters}m  powered by" + this.engine;
	    }
	}

    ```
仅在构造函数里使用protected engine: string参数来创建和初始化engine成员,从而把声明和赋值合并至一处。

### 存取器

TypeScript支持getters/setters来， 它能帮助你有效的控制对对象成员的访问，外部可以通过getters/setters来访问设置和类的私有成员。看下面的例子：

   	```typescript
	 class Car {
		private _carColor:String

	    constructor(protected engine: string) {}

	    getCarcolor(): string {
	        return this._carColor;
	    }
	
	    setCarcolor(color: string) {
	         this._carColor = color;
	    }
	}

	let redCar = new  Car("petrol");
	redCar.setCarcolor('red');
	console.log(redCar.getCarcolor());

    ```
注意：若要使用存取器，要求设置编译器输出目标为ECMAScript 5或更高

### 静态属性

类的静态成员存在于类本身上面而不是类的实例上。  如同在实例属性上使用 `this.前缀`来访问属性一样，这里我们使用*类名.*来访问静态属性。

    ```typescript
    class Grid {
	    static origin = {x: 0, y: 0};
	    calculateDistanceFromOrigin(point: {x: number; y: number;}) {
	    let xDist = (point.x - Grid.origin.x);
	    let yDist = (point.y - Grid.origin.y);
	    return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
	    }
	    constructor (public scale: number) { }
    }
    
    let grid1 = new Grid(1.0);  // 1x scale
    let grid2 = new Grid(5.0);  // 5x scale
    
    console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
    console.log(grid2.calculateDistanceFromOrigin({x: 10, y: 10}));
    
    ```

### 抽象类

抽象类是供其它类继承的基类，一般不会直接被实例化。 不同于接口，抽象类可以包含成员的实现细节。 abstract关键字是用于定义抽象类和在抽象类内部定义抽象方法。抽象类中的抽象方法不包含具体实现并且必须在派生类中实现。

	 ```typescript
    abstract class Department {
    
	    constructor(public name: string) {}
	    
	    printName(): void {
	    	console.log('Department name: ' + this.name);
	    }
	    
	    abstract printMeeting(): void; // 必须在派生类中实现
	}
	    
	class AccountingDepartment extends Department {
	    
	    constructor() {
	    	super('Accounting and Auditing'); // constructors in derived classes must call super()
	    }
	    
	    printMeeting(): void {
	    	console.log('The Accounting Department meets each Monday at 10am.');
	    }
	    
	    generateReports(): void {
	    	console.log('Generating accounting reports...');
	    }
    }
    
    let department: Department; // ok to create a reference to an abstract type
    department = new Department(); // error: cannot create an instance of an abstract class
    department = new AccountingDepartment(); // ok to create and assign a non-abstract subclass
    department.printName();
    department.printMeeting();
    department.generateReports(); // error: method doesn't exist on declared abstract type
    
    ```

## 1.3.4 函数

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
    	```
descriptor对象的初始值如下

	```typescript
    	 descriptor = {
    	   value: oneFunction,
    	   enumerable: false,
    	   configurable: true,
    	   writable: true
    	 };
    	 ```


##1.3.5 模块

关于本节的讲解的模块要明确一点：为了与 ECMAScript 2015里的术语保持一致， “内部模块”称做“命名空间”， “外部模块”简称为“模块”。这里所说的模块即是”外部模块“

### 介绍

模块是自声明的，两个模块之间的关系是通过在文件级别上使用imports和exports建立的。TypeScript与ECMAScript 2015一样，任何包含顶级import或者export的文件都被当成一个模块。

模块在其自身的作用域里执行，而不是在全局作用域里；这意味着定义在一个模块里的变量，函数，类等在模块外部是不可见的，除非明确地使用export导出它们。 相反，如果想使用其它模块导出的变量，函数，类，接口等的时候，必须要导入它们，可以使用 import。导入

模块使用模块加载器去导入其它的模块。 在运行时，模块加载器的作用是在执行此模块代码前去查找并执行这个模块的所有依赖。 大家最熟知的JavaScript模块加载器是服务于Node.js的 CommonJS和服务于Web应用的Require.js。

### 导出

**导出声明**

任何声明（比如变量，函数，类，类型别名或接口）都能够通过添加export关键字来导出。

Validation.ts
	
	export interface StringValidator {
	    isAcceptable(s: string): boolean;
	}

ZipCodeValidator.ts
	
	export const numberRegexp = /^[0-9]+$/;
	
	export class ZipCodeValidator implements StringValidator {
	    isAcceptable(s: string) {
	        return s.length === 5 && numberRegexp.test(s);
	    }
	}

**导出语句**

我们可能需要对导出的部分重命名，就用到了导出语句。上面的例子可以这样改写：

	class ZipCodeValidator implements StringValidator {
	    isAcceptable(s: string) {
	        return s.length === 5 && numberRegexp.test(s);
	    }
	}
	export { ZipCodeValidator };
	export { ZipCodeValidator as mainValidator };

**重新导出**

经常可能需要扩展其它模块，并且只导出那个模块的部分内容。 重新导出功能并不会在当前模块导入那个模块或定义一个新的局部变量。

ParseIntBasedZipCodeValidator.ts
	
	export class ParseIntBasedZipCodeValidator {
	    isAcceptable(s: string) {
	        return s.length === 5 && parseInt(s).toString() === s;
	    }
	}

	// 导出原先的验证器但做了重命名
	export {ZipCodeValidator as RegExpBasedZipCodeValidator} from "./ZipCodeValidator";

或者一个模块可以包裹多个模块，并把他们导出的内容联合在一起通过语法：export * from "module"。

AllValidators.ts
	
	export * from "./StringValidator"; // exports interface StringValidator
	export * from "./ZipCodeValidator";  // exports class ZipCodeValidator

### 导入

模块的导入操作与导出一样简单。 可以使用以下 import形式之一来导入其它模块中的导出内容。

**导入一个模块中的某个导出内容**

	import { ZipCodeValidator } from "./ZipCodeValidator";
	
	let myValidator = new ZipCodeValidator();

可以对导入内容重命名
	
	import { ZipCodeValidator as ZCV } from "./ZipCodeValidator";
	let myValidator = new ZCV();

**将整个模块导入到一个变量，并通过它来访问模块的导出部分**

	import * as validator from "./ZipCodeValidator";
	let myValidator = new validator.ZipCodeValidator();

**具有副作用的导入模块**

尽管不推荐这么做，一些模块会设置一些全局状态供其它模块使用。 这些模块可能没有任何的导出或用户根本就不关注它的导出。 使用下面的方法来导入这类模块：

	import "./my-module.js";

### 默认导出

每个模块都可以有一个default导出。 默认导出使用 default关键字标记；并且一个模块只能够有一个default导出。 需要使用一种特殊的导入形式来导入 default导出。类和函数声明可以直接被标记为默认导出，标记为默认导出的类和函数的名字是可以省略的。
	
ZipCodeValidator.ts
	
	export default class ZipCodeValidator {
	    static numberRegexp = /^[0-9]+$/;
	    isAcceptable(s: string) {
	        return s.length === 5 && ZipCodeValidator.numberRegexp.test(s);
	    }
	}
	
Test.ts
	
	import validator from "./ZipCodeValidator";
	
	let myValidator = new validator();
或者

StaticZipCodeValidator.ts
	
	const numberRegexp = /^[0-9]+$/;
	
	export default function (s: string) {
	    return s.length === 5 && numberRegexp.test(s);
	}
	
Test.ts
	
	import validate from "./StaticZipCodeValidator";
	
	let strings = ["Hello", "98052", "101"];
	
	// Use function validate
	strings.forEach(s => {
	  console.log(`"${s}" ${validate(s) ? " matches" : " does not match"}`);
	});

default导出也可以是一个值

OneTwoThree.ts

	export default "123";
	
Log.ts
	
	import num from "./OneTwoThree";
	
	console.log(num); // "123"

**export = 和 import = require()**

CommonJS和AMD都有一个exports对象的概念，它包含了一个模块的所有导出内容。

它们也支持把exports替换为一个自定义对象。 默认导出就好比这样一个功能；然而，它们却并不相互兼容。 TypeScript模块支持 export =语法以支持传统的CommonJS和AMD的工作流模型。

export =语法定义一个模块的导出对象。 它可以是类，接口，命名空间，函数或枚举。

若要导入一个使用了export =的模块时，必须使用TypeScript提供的特定语法import let = require("module")。
	
ZipCodeValidator.ts

	let numberRegexp = /^[0-9]+$/;
	class ZipCodeValidator {
	    isAcceptable(s: string) {
	        return s.length === 5 && numberRegexp.test(s);
	    }
	}
	export = ZipCodeValidator;
	
Test.ts

	import zip = require("./ZipCodeValidator");
	
	// Some samples to try
	let strings = ["Hello", "98052", "101"];
	
	// Validators to use
	let validator = new zip();
	
	// Show whether each string passed each validator
	strings.forEach(s => {
	  console.log(`"${ s }" - ${ validator.isAcceptable(s) ? "matches" : "does not match" }`);
	});
	
### 如何创建模块结构

**尽可能地在顶层导出**

”在顶层上导出”可以减少用户使用的难度，默认导出就满足了次要求：*如果仅导出单个 class 或 function，使用 export default*。 如果一个模块是为了导出特定的内容，那么应该考虑使用一个默认导出， 这会令模块的导入和使用变得些许简单。 比如：

MyClass.ts

	export default class SomeType {
	  constructor() { ... }
	}

MyFunc.ts

	export default function getThing() { return 'thing'; }

Consumer.ts

	import t from "./MyClass";
	import f from "./MyFunc";
	let x = new t();
	console.log(f());

使用默认导出，用户可以随意命名导入模块的类型（本例为t），并且不需要多余的（.）来找到相关对象。

*如果要导出多个对象，把它们放在顶层里导出*

MyThings.ts
	
	export class SomeType { /* ... */ }
	export function someFunc() { /* ... */ }

相反地，当导入的时候：

*明确地列出导入的名字*

Consumer.ts

	import { SomeType, SomeFunc } from "./MyThings";
	let x = new SomeType();
	let y = someFunc();

*使用命名空间导入模式当你要导出大量内容的时候*

MyLargeModule.ts

	export class Dog { ... }
	export class Cat { ... }
	export class Tree { ... }
	export class Flower { ... }

Consumer.ts

	import * as myLargeModule from "./MyLargeModule.ts";
	let x = new myLargeModule.Dog();

*使用重新导出进行扩展*

我们可能经常需要去扩展一个模块的功能，推荐的方案是 不要去改变原来的对象，而是导出一个新的实体来提供新的功能。

假设Calculator.ts模块里定义了一个简单的计算器实现。 这个模块同样提供了一个辅助函数来测试计算器的功能，通过传入一系列输入的字符串并在最后给出结果。

Calculator.ts
	
	export class Calculator {
	    private current = 0;
	    private memory = 0;
	    private operator: string;
	
	    protected processDigit(digit: string, currentValue: number) {
	        if (digit >= "0" && digit <= "9") {
	            return currentValue * 10 + (digit.charCodeAt(0) - "0".charCodeAt(0));
	        }
	    }
	
	    protected processOperator(operator: string) {
	        if (["+", "-", "*", "/"].indexOf(operator) >= 0) {
	            return operator;
	        }
	    }
	
	    protected evaluateOperator(operator: string, left: number, right: number): number {
	        switch (this.operator) {
	            case "+": return left + right;
	            case "-": return left - right;
	            case "*": return left * right;
	            case "/": return left / right;
	        }
	    }
	
	    private evaluate() {
	        if (this.operator) {
	            this.memory = this.evaluateOperator(this.operator, this.memory, this.current);
	        }
	        else {
	            this.memory = this.current;
	        }
	        this.current = 0;
	    }
	
	    public handelChar(char: string) {
	        if (char === "=") {
	            this.evaluate();
	            return;
	        }
	        else {
	            let value = this.processDigit(char, this.current);
	            if (value !== undefined) {
	                this.current = value;
	                return;
	            }
	            else {
	                let value = this.processOperator(char);
	                if (value !== undefined) {
	                    this.evaluate();
	                    this.operator = value;
	                    return;
	                }
	            }
	        }
	        throw new Error(`Unsupported input: '${char}'`);
	    }
	
	    public getResult() {
	        return this.memory;
	    }
	}
	
	export function test(c: Calculator, input: string) {
	    for (let i = 0; i < input.length; i++) {
	        c.handelChar(input[i]);
	    }
	
	    console.log(`result of '${input}' is '${c.getResult()}'`);
	}

这是使用导出的test函数来测试计算器。

TestCalculator.ts

	import { Calculator, test } from "./Calculator";
	
	
	let c = new Calculator();
	test(c, "1+2*33/11="); // prints 9

现在扩展它，添加支持输入其它进制（十进制以外），让我们来创建ProgrammerCalculator.ts。

ProgrammerCalculator.ts

import { Calculator } from "./Calculator";

	class ProgrammerCalculator extends Calculator {
	    static digits = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "C", "D", "E", "F"];
	
	    constructor(public base: number) {
	        super();
	        if (base <= 0 || base > ProgrammerCalculator.digits.length) {
	            throw new Error("base has to be within 0 to 16 inclusive.");
	        }
	    }
	
	    protected processDigit(digit: string, currentValue: number) {
	        if (ProgrammerCalculator.digits.indexOf(digit) >= 0) {
	            return currentValue * this.base + ProgrammerCalculator.digits.indexOf(digit);
	        }
	    }
	}
	
	// Export the new extended calculator as Calculator
	export { ProgrammerCalculator as Calculator };
	
	// Also, export the helper function
	export { test } from "./Calculator";

新的ProgrammerCalculator模块导出的API与原先的Calculator模块很相似，但却没有改变原模块里的对象。 下面是测试ProgrammerCalculator类的代码：

TestProgrammerCalculator.ts

	import { Calculator, test } from "./ProgrammerCalculator";
	
	let c = new Calculator(2);
	test(c, "001+010="); // prints 3

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

### 接口初探
在TypeScript里，接口的作用就是为类型命名和为你的代码或第三方代码定义契约。下面通过一个简单示例来观察接口是如何工作的：
    
    ```typescript
    interface FullName {
	    firstName: string;
	    secondName: string;
    }

	function printLabel(name:FullName) {
  		console.log(name.firstName+" "+name.secondName);
	}

	let myObj = {age: 10, firstName: 'Jim', secondName: 'Raynor'};

	printLabel(myObj);
    ```
从上面的例子可以看出：接口FullName必须包含一个firstName属性和secondName属性且类型都为string。

这里有两点需要注意：

1.传给 printLabel的对象只要“形式上”满足接口的要求即可：对象myObj必须包含一个firstName属性和secondName属性且类型都为string。

2. 接口类型检查器不会去检查属性的顺序，只要相应的属性存在且类型匹配就可以
	
### 可选属性

可选属性在应用“option bags”模式时很常用，即给函数传入的参数对象中只有部分属性赋值了。带有可选属性的接口与普通的接口定义差不多，只是在可选属性名字定义的后面加一个?符号。下面通过一个例子来说明：

    ```typescript
	 interface FullName {
	    firstName: string;
	    secondName?: string;
    }

	function printLabel(name:FullName) {
  		console.log(name.firstName+" "+name.secondName);
	}

	let myObj = {firstName: 'Jim', secondName: 'Raynor'};

	printLabel(myObj);
	 ```

可选属性有两个好处：一是可以对可能存在的属性进行预定义；二是可以捕获引用了不存在的属性时的错误。 比如，将printLabel里的secondName属性名拼错成second，就会得到一个错误提示，这就是下面要讲的 额外属性检查。

### 额外的属性检查

  	```typescript
	 interface FullName {
	    firstName: string;
	    secondName?: string;
    	}
	function printLabel(name:FullName) {
	
  		console.log(name.firstName+" "+name.secondName);
	}

	let myObj = {age: 10, firstName: 'Jim', secondName: 'Raynor'};

	printLabel(myObj);
	 ```
 上面的例子编译时会报错：.... property'age' does not exist in type 'FullName',使用了可选属性就不能像接口初探小节里面的例子，给函数传接口里没有的属性了。

加了可选属性后，对象字面量会被特殊对待而且会经过额外属性检查，当将它们赋值给变量或作为参数传递的时候。如果一个对象字面量存在任何“目标类型”不包含的属性时，就会编译失败。绕开这些检查非常简单。 最好而简便的方法是使用类型断言

     ```typescript
    printLabel({age: 10, firstName: 'Jim', secondName: 'Raynor'} as  FullName);
    ```

另一个方法，就是将一个对象赋值给另一个变量：

     ```typescript
    let myObj = {age: 10, firstName: 'Jim', secondName: 'Raynor'};
    printLabel(myObj);
     ```

对于包含方法和内部状态的复杂对象字面量来讲，你可能需要使用这些技巧。但是一般出现额外属性检查错误有可能会是真正的bug，当遇到了额外类型检查出的错误，比如选择包，你应该去审查一下你的类型声明。

### 函数类型

接口能够描述JavaScript中对象拥有的各种各样的外形。 除了描述带有属性的普通对象外，接口也可以描述函数类型，如下例所示：

    ```typescript
    interface SearchFunc {
  		(source: string, subString: string): boolean;
	}
     ```

为了使用接口表示函数类型，我们需要给接口定义一个调用签名。 它就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型。这样定义后，我们可以像使用其它接口一样使用这个函数类型的接口。 下例展示了如何创建一个函数类型的变量，并将一个同类型的函数赋值给这个变量。

     ```typescript
     let mySearch: SearchFunc;
     mySearch = function(src: string, sub: string) {
     	let result = src.search(sub);
      	if (result == -1) {
    		return false;
      	}
      	else {
    		return true;
      	}
     }
     ```
对于函数类型的类型检查来说，函数的参数名不需要与接口里定义的名字相匹配。 函数的参数会逐个进行检查，要求对应位置上的参数类型是兼容的。  函数的返回值类型是通过其返回值推断出来的（此例是 false和true）。 如果让这个函数返回数字或字符串，类型检查器会警告我们函数的返回值类型与 SearchFunc接口中的定义不匹配。

### 数组类型
数组类型具有一个 index类型表示索引的类型，还有一个相应的返回值类型表示通过索引得到的元素的类型。支持两种索引类型：string和number。 数组可以同时使用这两种索引类型，但是有一个限制，数字索引返回值的类型必须是字符串索引返回值的类型的子类型。

    ```typescript
    interface StringArray {
      [index: number]: string;
    }
    
    let myArray: StringArray;
    myArray = ["Bob", "Fred"];
    ```
### 类类型

与C#或Java里接口的基本作用一样，TypeScript也能够用它来明确的强制一个类去符合某种契约。
    
    ```typescript
    interface ClockInterface {
    	currentTime: Date;
    }
    
    class Clock implements ClockInterface {
    	currentTime: Date;
    	constructor(h: number, m: number) { }
    }
    ```

可以在接口中描述一个方法，在类里实现它，如同下面的setTime方法一样：

    ```typescript
    interface ClockInterface {
    	currentTime: Date;
    	setTime(d: Date);
    }
    
    class Clock implements ClockInterface {
    	currentTime: Date;
    	setTime(d: Date) {
    		this.currentTime = d;
    	}
    	constructor(h: number, m: number) { }
    }
    ```

接口描述了类的公共部分，而不是公共和私有两部分。 它不会帮你检查类是否具有某些私有成员。

### 扩展接口

和类一样，接口也可以相互扩展，能够从一个接口里复制成员到另一个接口里，这样就可以更灵活地将接口分割到可重用的模块里。

    ```typescript
    interface Shape {
    	color: string;
    }
    
    interface Square extends Shape {
    	sideLength: number;
    }
    
    let square = <Square>{};
    square.color = "blue";
    square.sideLength = 10;
    ```

一个接口可以继承多个接口，创建出多个接口的合成接口。

    ```typescript
    interface Shape {
    	color: string;
    }
    
    interface PenStroke {
    	penWidth: number;
    }
    
    interface Square extends Shape, PenStroke {
    	sideLength: number;
    }
    
    let square = <Square>{};
    square.color = "blue";
    square.sideLength = 10;
    square.penWidth = 5.0;  
    ```

### 混合类型

由于JavaScript其动态灵活的特点，有时希望一个对象可以同时具有上面提到的多种类型。下面这个例子里面一个对象可以同时做为函数和对象使用，并带有额外的属性。

    ```typescript
    interface Counter {
    	(start: number): string;
    	interval: number;
    	reset(): void;
	}
	
	function getCounter(): Counter {
	    let counter = <Counter>function (start: number) { return "123"; };
	    counter.interval = 123;
	    counter.reset = function () { };
	    return counter;
	}
	
	let c = getCounter();
	c(10);
	c.reset();
	c.interval = 5.0;
    ```

## 装饰器

###装饰器介绍

装饰器（Decorators装饰器是一种特殊类型的声明，它能够被附加到类声明，方法， 访问符，属性，或 参数上。 装饰器利，形如 @expressio，expression，求值后必须为一个函数，它使用被装饰的声明信息在运行时被调用。

*注：由于Javascript里的Decorators目前处在建议征集的第一阶段， 所以Decorators在TypeScript是实验性的特性，在未来的版本中可能会发生改变。*

若要启用实验性的decorator，须启用experimentalDecorators编译器选项，在命令行中或在tsconfig.json：

命令行:
    
    tsc --target ES5 --experimentalDecorators

tsconfig.json:

    {
    	"compilerOptions": {
    		"target": "ES5",
    		"experimentalDecorators": true
    	}
    }
    
### 装饰器组合

多个装饰器同时应用到一个声明上，可以写在同一行上，也可以写在多行上，如下例所示：

	@f @g x

或

	@f
	@g
	x

当多个装饰器应用于一个声明上，它们求值方式与复合函数相似。在这个模型下，当复合f和g时，复合的结果(f ∘ g)(x)等同于f(g(x))。同样的，在TypeScript里，当多个装饰器应用在一个声明上时会进行如下步骤的操作：由上至下依次对装饰器表达式求值。求值的结果会被当作函数，由下至上依次调用。如果我们使用装饰器工厂的话，可以通过下面的例子来观察它们求值的顺序：

	function f() {
	    console.log("f(): evaluated");
	    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
	        console.log("f(): called");
	    }
	}
	
	function g() {
	    console.log("g(): evaluated");
	    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
	        console.log("g(): called");
	    }
	}
	
	class C {
	    @f()
	    @g()
	    method() {}
	}

在控制台里会打印出如下结果：
	
	f(): evaluated
	g(): evaluated
	g(): called
	f(): called

### 类装饰器

类装饰器在类声明之前被声明（紧贴着类声明）。 类装饰器应用于类构造函数，可以用来监视，修改或替换类定义。 类装饰器不能用在声明文件中( .d.ts)，也不能用在任何外部上下文中（比如declare的类）。

类装饰器表达式会在运行时当作函数被调用，类的构造函数作为其唯一的参数。如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明。

*注意  如果你要返回一个新的构造函数，你必须注意处理好原来的原型链。 在运行时的装饰器调用逻辑中 不会为你做这些。*

下面是使用类装饰器(@sealed)的例子，应用到Greeter类：
	
	@sealed
	class Greeter {
	    greeting: string;
	    constructor(message: string) {
	        this.greeting = message;
	    }
	    greet() {
	        return "Hello, " + this.greeting;
	    }
	}

我们可以这样定义@sealed装饰器

	function sealed(constructor: Function) {
	    Object.seal(constructor);
	    Object.seal(constructor.prototype);
	}

当@sealed被执行的时候，它将密封此类的构造函数和原型。(注：参见Object.seal)

### 方法装饰器

方法装饰器声明在一个方法的声明之前（紧贴着方法声明）。 它会被应用到方法的 属性描述符上，可以用来监视，修改或者替换方法定义。 方法装饰器不能用在声明文件( .d.ts)，重载或者任何外部上下文（比如declare的类）中。

方法装饰器表达式会在运行时当作函数被调用，传入下列3个参数：

1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
1. 成员的名字。
1. 成员的属性描述符。

*注意：如果代码输出目标版本小于ES5，Property Descriptor将会是undefined。*

如果方法装饰器返回一个值，它会被用作方法的属性描述符。

*注意：如果代码输出目标版本小于ES5返回值会被忽略。*

下面是一个方法装饰器（@enumerable）的例子，应用于Greeter类的方法上：

	class Greeter {
	    greeting: string;
	    constructor(message: string) {
	        this.greeting = message;
	    }
	
	    @enumerable(false)
	    greet() {
	        return "Hello, " + this.greeting;
	    }
	}

我们可以用下面的函数声明来定义@enumerable装饰器：

	function enumerable(value: boolean) {   // 这是一个装饰器工厂
		//  这是装饰器
	    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
	        descriptor.enumerable = value;
	    };
	}

当装饰器 @enumerable(false)被调用时，它会修改属性描述符的enumerable属性。这里的@enumerable(false)是一个装饰器工厂，所谓的装饰器工厂就是一个简单的函数，它返回一个表达式，以供装饰器在运行时调用。

### 访问符装饰器

访问符装饰器声明在一个访问符的声明之前（紧贴着访问符声明）。 访问符装饰器应用于访问符的属性描述符并且可以用来监视，修改或替换一个访问符的定义。 访问符装饰器不能用在声明文件中（.d.ts），或者任何外部上下文（比如 declare的类）里。

*注意：TypeScript不允许同时装饰一个成员的get和set访问符。相反，所有装饰的成员必须被应用到文档顺序指定的第一个访问符。这是因为，装饰器应用于一个属性描述符，它联合了get和set访问符，而不是分开声明的。*

访问符装饰器表达式会在运行时当作函数被调用，传入下列3个参数：

1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
1. 成员的名字。
1. 成员的属性描述符。

*注意：如果代码输出目标版本小于ES5，Property Descriptor将会是undefined。*

如果访问符装饰器返回一个值，它会被用作方法的属性描述符。

*注意：如果代码输出目标版本小于ES5返回值会被忽略。*

下面是使用了访问符装饰器（@configurable）的例子，应用于Point类的成员上：

	class Point {
	    private _x: number;
	    private _y: number;
	    constructor(x: number, y: number) {
	        this._x = x;
	        this._y = y;
	    }
	
	    @configurable(false)
	    get x() { return this._x; }
	
	    @configurable(false)
	    get y() { return this._y; }
	}

我们可以通过如下函数声明来定义@configurable装饰器：
	
	function configurable(value: boolean) {
	    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
	        descriptor.configurable = value;
	    };
	}

### 属性装饰器

属性装饰器声明在一个属性声明之前（紧贴着属性声明）。 属性装饰器不能用在声明文件中（.d.ts），或者任何外部上下文（比如 declare的类）里。

属性装饰器表达式会在运行时当作函数被调用，传入下列2个参数：

1. 对于静态成员来说是类的构造函数，对于实例成员是类的原型对象。
1. 成员的名字。

*注意：属性描述符不会做为参数传入属性装饰器，这与TypeScript是如何初始化属性装饰器的有关。 因为目前没有办法在定义一个原型对象的成员时描述一个实例属性，并且没办法监视或修改一个属性的初始化方法。 因此，属性描述符只能用来监视类中是否声明了某个名字的属性。*

如果属性装饰器返回一个值，它会被用作方法的属性描述符。

注意：如果代码输出目标版本小于ES5，返回值会被忽略。

如果访问符装饰器返回一个值，它会被用作方法的属性描述符。

我们可以用它来记录这个属性的元数据，如下例所示：

	class Greeter {
	    @format("Hello, %s")
	    greeting: string;
	
	    constructor(message: string) {
	        this.greeting = message;
	    }
	    greet() {
	        let formatString = getFormat(this, "greeting");
	        return formatString.replace("%s", this.greeting);
	    }
	}

然后定义@format装饰器和getFormat函数：

	import "reflect-metadata";
	
	const formatMetadataKey = Symbol("format");
	
	function format(formatString: string) {
	    return Reflect.metadata(formatMetadataKey, formatString);
	}
	
	function getFormat(target: any, propertyKey: string) {
	    return Reflect.getMetadata(formatMetadataKey, target, propertyKey);
	}

这个 @format("Hello, %s") 装饰器是个 装饰器工厂。 当 @format("Hello, %s")被调用时，它添加一条这个属性的元数据，通过reflect-metadata库里的Reflect.metadata函数。 当 getFormat被调用时，它读取格式的元数据。

*注意：这个例子需要使用reflect-metadata库。 查看 元数据了解reflect-metadata库更详细的信息。*


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


