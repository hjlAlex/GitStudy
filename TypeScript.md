#### 1，全局安装typescript

```shell
npm install -g typescript
```

#### 2，编译ts文件

###### 例如：当前编辑好了index.ts文件

```shell
tsc index.ts
```

###### ps:上面的`tsc index.ts`默认会在**index.ts**同级下生成index.js，当然我们也可以指定js的输出路径，修改tsconfig.json即可（详情看第3,4点）。

#### 3，tsconfig.json文件

- ###### 生成tsconfig.json文件

  ```shell
  tsc --init
  ```

  ![](/images/typescript/img1.png)

- ###### 参数说明参考

  [tsconfig.json · TypeScript中文网 · TypeScript——JavaScript的超集 (tslang.cn)](https://www.tslang.cn/docs/handbook/tsconfig-json.html)

  [编译选项 · TypeScript中文网 · TypeScript——JavaScript的超集 (tslang.cn)](https://www.tslang.cn/docs/handbook/compiler-options.html)

#### 4，使用tsconfig.json文件进行编译

###### 直接使用命令`tsc`后面不加任何参数，默认会在当前路径下寻找tsconfig.json文件，根据里面的配置信息进行ts文件的编译，如果当前路径下没有找到，则继续往父级一直寻找。

![](/images/typescript/img2.png)

###### 回顾下第二点，我们修改编译后js文件的输出，对tsconfig.json文件的compilerOptions编辑改动如下：

![](/images/typescript/img3.png)

###### 然后使用`tsc`(后面不加任何参数)，如果tsconfig.json里面没有指定编译的文件，则默认会编译当前目录下所有的ts文件，同时会把编译后生成的js文件输出到js目录里面。

![](/images/typescript/img4.png)

#### 5，自动监视ts文件变更，自动编译

###### 菜单路径：终端-->运行任务，然后选择typescript

![](/images/typescript/img5.png)

###### 接着继续选中监视tsc

![](/images/typescript/img6.png)

###### 最后随便更改ts的内容，保存后tsc会立马编译，输出最新内容到js目录。

![](/images/typescript/img7.png)

#### 6，数据类型

- ###### 布尔值

  ###### 最基本的数据类型就是简单的true/false值，在JavaScript和TypeScript里叫做`boolean`（其它语言中也一样）。

  ```typescript
  let isDone: boolean = false;
  ```

- ###### 数字

  ###### 和JavaScript一样，TypeScript里的所有数字都是浮点数。 这些浮点数的类型是 `number`。 除了支持十进制和十六进制字面量，TypeScript还支持ECMAScript 2015中引入的二进制和八进制字面量。

  ```typescript
  let decLiteral: number = 6;
  let hexLiteral: number = 0xf00d;
  let binaryLiteral: number = 0b1010;
  let octalLiteral: number = 0o744;
  ```

- ###### 字符串

  ###### JavaScript程序的另一项基本操作是处理网页或服务器端的文本数据。 像其它语言里一样，我们使用 `string`表示文本数据类型。 和JavaScript一样，可以使用双引号（ `"`）或单引号（`'`）表示字符串。

  ```typescript
  let name: string = "bob";
  name = "smith";
  ```

  ###### 你还可以使用**模版字符串**，它可以定义多行文本和内嵌表达式。 这种字符串是被反引号包围 **``**，并且以${ expr }这种形式嵌入表达式。

  ```typescript
  let name: string = `Gene`;
  let age: number = 37;
  let sentence: string = `Hello, my name is ${ name }.
  
  I'll be ${ age + 1 } years old next month.`;
  ```

  ###### 这与下面的方式效果相同

  ```typescript
  let sentence: string = "Hello, my name is " + name + ".\n\n" +
      "I'll be " + (age + 1) + " years old next month.";
  ```

- ###### 数组

  ###### TypeScript像JavaScript一样可以操作数组元素。 有两种方式可以定义数组。 第一种，可以在元素类型后面接上 `[]`，表示由此类型元素组成的一个数组：

  ```typescript
  let list: number[] = [1, 2, 3];
  ```

  ###### 第二种方式是使用数组泛型，`Array<元素类型>`：

  ```typescript
  let list: Array<number> = [1, 2, 3];
  ```

- ###### 元组 Tuple

  ###### 元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，你可以定义一对值分别为 `string`和`number`类型的元组。

  ```typescript
  // Declare a tuple type
  let x: [string, number];
  // Initialize it
  x = ['hello', 10]; // OK
  // Initialize it incorrectly
  x = [10, 'hello']; // Error
  ```

  ###### 当访问一个已知索引的元素，会得到正确的类型：

  ```typescript
  console.log(x[0].substr(1)); // OK
  console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
  ```

  ###### 当访问一个越界的元素，会使用联合类型(后面章节会继续讨论)替代：

  ```typescript
  x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型             (这里其实vscode会给出语法错误提示)
  
  console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString	(这里其实vscode会给出语法错误提示)
  
  x[6] = true; // Error, 布尔不是(string | number)类型		(这里其实vscode会给出语法错误提示)
  ```

- ###### 枚举

  ###### `enum`类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

  ```typescript
  enum Color {Red, Green, Blue}
  let c: Color = Color.Green;
  ```

  ###### 默认情况下，从`0`开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从 `1`开始编号：

  ```typescript
  enum Color {Red = 1, Green, Blue}
  let c: Color = Color.Green;
  ```

  ###### 或者，全部都采用手动赋值：

  ```typescript
  enum Color {Red = 1, Green = 2, Blue = 4}
  let c: Color = Color.Green;
  ```

  ###### 枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：

  ```typescript
  enum Color {Red = 1, Green, Blue}
  let colorName: string = Color[2];
  
  console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
  ```

- ###### Any

  ###### 有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用 `any`类型来标记这些变量：

  ```typescript
  let notSure: any = 4;
  notSure = "maybe a string instead";
  notSure = false; // okay, definitely a boolean
  ```

  ###### 在对现有代码进行改写的时候，`any`类型是十分有用的，它允许你在编译时可选择地包含或移除类型检查。 你可能认为 `Object`有相似的作用，就像它在其它语言中那样。 但是 `Object`类型的变量只是允许你给它赋任意值 , 但是却不能够在它上面调用任意的方法，即便它真的有这些方法：

  ```typescript
  let notSure: any = 4;
  notSure.ifItExists(); // okay, ifItExists might exist at runtime
  notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)
  
  let prettySure: Object = 4;
  prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
  ```

  ###### 当你只知道一部分数据的类型时，`any`类型也是有用的。 比如，你有一个数组，它包含了不同的类型的数据：

  ```typescript
  let list: any[] = [1, true, "free"];
  
  list[1] = 100;
  ```

- ###### Void

  ###### 某种程度上来说，`void`类型像是与`any`类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 `void`：

  ```typescript
  function warnUser(): void {
      console.log("This is my warning message");
  }
  ```

  ###### 声明一个`void`类型的变量没有什么大用，因为你只能为它赋予`undefined`和`null`：

  ```typescript
  let unusable: void = undefined;
  ```

- ###### Null 和 Undefined

  ###### TypeScript里，`undefined`和`null`两者各自有自己的类型分别叫做`undefined`和`null`。 和 `void`相似，它们的本身的类型用处不是很大：

  ```typescript
  // Not much else we can assign to these variables!
  let u: undefined = undefined;
  let n: null = null;
  ```

  ###### 默认情况下`null`和`undefined`是所有类型的子类型。 就是说你可以把 `null`和`undefined`赋值给`number`类型的变量。

  ###### 然而，当你指定了`--strictNullChecks`标记，`null`和`undefined`只能赋值给`void`和它们各自。 这能避免 *很多*常见的问题。 也许在某处你想传入一个 `string`或`null`或`undefined`，你可以使用联合类型`string | null | undefined`。 再次说明，稍后我们会介绍联合类型。

- ###### Never(用的貌似不多)

  ###### `never`类型表示的是那些永不存在的值的类型。 例如， `never`类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 `never`类型，当它们被永不为真的类型保护所约束时。

  ###### `never`类型是任何类型的子类型，也可以赋值给任何类型；然而，*没有*类型是`never`的子类型或可以赋值给`never`类型（除了`never`本身之外）。 即使 `any`也不可以赋值给`never`。

  ###### 下面是一些返回`never`类型的函数：

  ```typescript
  // 返回never的函数必须存在无法达到的终点
  function error(message: string): never {
      throw new Error(message);
  }
  
  // 推断的返回值类型为never
  function fail() {
      return error("Something failed");
  }
  
  // 返回never的函数必须存在无法达到的终点
  function infiniteLoop(): never {
      while (true) {
      }
  }
  ```

- ###### Object

  ###### `object`表示非原始类型，也就是除`number`，`string`，`boolean`，`symbol`，`null`或`undefined`之外的类型。

  ###### 使用`object`类型，就可以更好的表示像`Object.create`这样的API。例如：

  ```typescript
  declare function create(o: object | null): void;
  
  create({ prop: 0 }); // OK
  create(null); // OK
  
  create(42); // Error
  create("string"); // Error
  create(false); // Error
  create(undefined); // Error
  ```

#### 7，类型断言（有的像java的强转）

1. ###### 尖括号断言

   ```typescript
   let someValue: any = "this is a string";
   
   let strLength: number = (<string>someValue).length;
   ```

2. ###### `as`断言

   ```typescript
   let someValue: any = "this is a string";
   
   let strLength: number = (someValue as string).length;
   ```

#### 8，函数

- ###### 和js的function语法一样，多了形参类型和返回值

  ```typescript
  function add(num1:number,num2:number): number {
      return num1 + num2;
  }
  //或者
  let add = function (num1:number,num2:number): number {
      return num1 + num2;
  }
  ```

- ###### 可选参数

  ```typescript
  function add(num1:number,num2:number,flag?:boolean): number {
      if(flag){
          //...
      }
      return num1 + num2;
  }
  ```

- ###### 默认值

  ```typescript
  function add(num1:number,num2:number,flag:boolean = false): number {
      if(flag){
          //...
      }
      return num1 + num2;
  }
  ```

- ###### 剩余参数(...操作)

  ```typescript
  function add(num1:number,num2:number,...args:any[]): number {
      let sum = 0;
      sum = sum + num1;
      sum = sum + num2;
      if(args && args.length > 0) {
         	for(let i = 0;i < args.length; i++) {
          	sum = sum + args[i];
      	} 
      }    
      return sum;
  }
  ```

- ###### 重载（先声明，后实现）

  ![](/images/typescript/img8.png)

- 箭头函数（es6语法）

  ```typescript
  //es5
  setTimeout(function(){
      //do something...
      console.log(this);
  },1000);
  //es6
  setTimeout(() => {
      //do something...
      console.log(this);
  },1000);
  ```

  ###### ps:es6的箭头函数和es5的匿名函数，最大的区别在于箭头函数里面的this是当前上下文。

  ![](/images/typescript/img9.png)

#### 9，类

- ###### es5类实现

  ```typescript
  function Person() {
      this.name = "hjl";
      this.age = 29;
      this.showThis = function () {
          console.log(this);
      }
  }
  var p = new Person();
  console.log(p.age);
  //也可以原型链上进行定义
  Person.prototype.sex = "男";
  Person.prototype.work = function () {
      console.log(this.name + "在工作");
  }
  p.showThis();
  p.work();
  ```

  ###### 注意：原型链上进行扩展的属性和类会被所有的实例共享，而构造函数里面的属性和方法不会！！！

- ###### es5静态方法

  ###### 上面调用的方法是实例方法，都是需要经过new对象后进行调用的，而静态方法则不需要，直接类点出来调用

  ```typescript
  Person.staticMethod = function () {
      console.log("staticMethod...");
  }
  Person.staticMethod();
  ```

- ###### es5继承(对象冒充继承和原型链继承)

  ```typescript
  //对象冒充继承
  function Web() {
      Person.call(this);//通过call实现对象冒充继承
  }
  var w = new Web();
  console.log(w.name + w.age);
  w.showThis();
  w.work();//报错，work为Persion原型链上的方法，对象冒充继承获取不到
  ```

  ###### 对象冒充继承可以继承父级构造函数里面的属性和方法，但继承不了父级原型链上的属性和方法。

  ```typescript
  function Web2() {
  }
  Web2.prototype = new Person();
  var w2 = new Web2();
  console.log(w2.name + w2.age);// 正常
  w2.showThis();// 正常
  w2.work();// 正常
  ```

  ###### 原型链继承可以继承父级构造函数里面的属性和方法，也可以父级原型链上的属性和方法。

  ###### 原型链接继承带来的问题

  ```typescript
  function Person(name, age) {
      this.name = name;
      this.age = age;
      this.showThis = function () {
          console.log(this);
      }
  }
  Person.prototype.sex = "男";
  Person.prototype.work = function () {
      console.log(this.name + "在工作");
  }
  
  function Web2(name, age) {
  
  }
  Web2.prototype = new Person();//通过原型链继承
  var w2 = new Web2("lm", 28);
  w2.work();//输出   undefined在工作
  ```

  ###### 通过原型链继承的时候是没有办法从子类中传参数到父类的

  ###### 所以，一般情况下是使用二者的组合模式，即对象冒充继承和原型链继承组合使用，上面的例子可以修改为：

  ```typescript
  function Person(name, age) {
      this.name = name;
      this.age = age;
      this.showThis = function () {
          console.log(this);
      }
  }
  Person.prototype.sex = "男";
  Person.prototype.work = function () {
      console.log(this.name + "在工作");
  }
  
  function Web2(name, age) {
      Person.call(this, name, age);//通过call实现对象冒充继承
  }
  Web2.prototype = new Person();//或者Web2.prototype = Person.prototype;
  var w2 = new Web2("lm", 28);
  w2.work();//输出   lm在工作
  ```

- ###### TS（es6）的继承和接口

  和java的语法大同小异，暂时跳过，emmm。。。

- ###### TS的泛型

  **函数泛型**

  ```typescript
  function getData<T>(value: T): T {
      return value;
  }
  ```

  **类泛型**

  ```typescript
  class MinClass<T>{
      public list: T[];
  
      constructor() {
          this.list = [];
      }
  
      add(value: T): void {
          this.list.push(value);
      }
  }
  ```

  **泛型接口**

  ```typescript
  //接口泛型1
  interface ConfigFn {
      <T>(value: T): T;
  }
  var getInfo: ConfigFn = function <T>(value: T): T {
      return value;
  }
  //接口泛型2
  interface ConfigFn2<T> {
      (value: T): T;
  }
  var getInfo2 = function <T>(value: T): T {
      return value;
  }
  var cf2: ConfigFn2<string> = getInfo2;
  ```

- ###### TS的export和import

  **方式一**

  ```typescript
  //./modules/DB.ts
  let url = "DB URL...";
  export function getURL(): string {
      return url;
  }
  export let username = "hjl";
  export function save(): void {
      console.log("save...");
  }
  ```

  ```typescript
  //引用
  import { getURL, username, save } from './modules/DB';//注意后面不需要加ts后缀名
  console.log(getURL());
  console.log(username);
  save();
  ```

  **方式二**

  ```typescript
  let url = "DB URL...";
  function getURL(): string {
      return url;
  }
  let username = "hjl";
  function save(): void {
      console.log("save...");
  }
  
  export { getURL, username, save }
  ```

  ```typescript
  //引用
  import { getURL, username, save } from './modules/DB';//注意后面不需要加ts后缀名
  console.log(getURL());
  console.log(username);
  save();
  ```

  **import** 和 **export**可以使用**as**来增加别名

  **export default**

  ###### export default只能在模块里面使用一次，而export可以使用多次，这个要注意，另外使用export default的时候，外面import的时候也有点区别，不需要加花括号

  ```typescript
  let url = "DB URL...";
  function getURL(): string {
      return url;
  }
  let username = "hjl";
  function save(): void {
      console.log("save...");
  }
  
  export default getURL;//默认导出getURL
  ```

  ```typescript
  //引用
  import getURL from './modules/DB';//getURL不用加{}
  console.log(getURL());
  ```

#### 10，装饰器

###### 	装饰器是一种特殊类型的声明，它能够被附加都类声明，方法，属性，或者参数上，可以修改类的行为。

###### 	通俗的讲，装饰器就是一个**方法**，可以注入到类、方法、属性参数上来扩展类、属性、参数的功能。

###### 	常见的装饰器有：类装饰器，属性装饰器，方法装饰器，参数装饰器。

###### 	装饰器的写法：普通装饰器（无法传参）、装饰器工厂（可传参）

- ###### 	类普通装饰器（无法传参）

  ```typescript
  //类修饰器方法定义
  function decorationFn(target: any): void {
      //target为修饰的类的定义
      console.log("修饰器...", target);
  }
  
  @decorationFn
  class A {
      name: string;
      constructor(name: string) {
          this.name = name;
          console.log("A的构造函数...");
      }
      showInfo(): void {
          console.log(this.name);
      }
  }
  new A("黄杰龙");
  ```

  ###### 执行结果

  ![](/images/typescript/img10.png)

- ###### 类装饰器工厂（可传参）

  ```typescript
  function decorationFn(param: any): Function {
      return function (target: any) {
          console.log("修饰器获取参数...", param);
          console.log("修饰器...", target);
      }
  }
  
  @decorationFn("hjl")
  class A {
      name: string;
      constructor(name: string) {
          this.name = name;
          console.log("A的构造函数...");
      }
      showInfo(): void {
          console.log(this.name);
      }
  }
  new A("黄杰龙");
  ```

  ###### 执行结果

  ![](/images/typescript/img11.png)

  ###### 特别1，我们还可以改类装饰器目标类的原型链

  ```typescript
  function decorationFn(param: any): Function {
      return function (target: any) {
          console.log("修饰器获取参数...", param);
          console.log("修饰器...", target);
          //因为target为修饰类的定义，我们甚至还可以改上面的原型链
          target.prototype.exp = "exp params...";
      }
  }
  
  @decorationFn("hjl")
  class A {
      name: string;
      constructor(name: string) {
          this.name = name;
          console.log("A的构造函数...");
      }
      showInfo(): void {
          console.log(this.name);
      }
  }
  let aaa: any = new A("黄杰龙");
  console.log(aaa.exp);
  ```

  ###### 执行结果

  ![](/images/typescript/img12.png)

  ###### 特别2，我们还可以重载目标类的构造函数

  ```typescript
  function decorationClass(target: any): any {
      return class C extends target {//class 最终也是 function，装饰器最终还是一个function，记住这个点
          constructor(name: string) {
              super(name);
              console.log("C的构造函数...");
          }
      }
  }
  
  @decorationClass
  class B {
      name: string;
      constructor(name: string) {
          this.name = name;
          console.log("B的构造函数...");
      }
      showInfo(): void {
          console.log(this.name);
      }
  }
  let bbb: any = new B("黄杰龙");
  ```

  ###### 执行结果

  ![](/images/typescript/img13.png)

- ###### 属性装饰器

  ###### 注意属性装饰器获取的参数和类装饰器的区别，特别是target，类装饰器target为目标类的定义，属性装饰器为目标类的原型对象实例。

  ```typescript
  function decorationClass(...args: any[]): void {
      console.log(args);
  }
  
  function decorationProp(defaultValue: string): Function {
      return function (target: any, prop: string) {
          target[prop] = defaultValue;
          console.log(target, prop);
      }
  }
  
  @decorationClass
  class D {
      @decorationProp("默认url")
      url: string | undefined;
      name: string | undefined;
  }
  ```

  ###### 执行结果

  ![](/images/typescript/img14.png)

  ###### ps:属性装饰器先执行，然后再到类装饰器

- ###### 各装饰器执行顺序

  **属性装饰器>方法装饰器>方法参数装饰器>类装饰器**

  **同级下，装饰器后面>前面**

  
