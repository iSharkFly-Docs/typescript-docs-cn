# 什么是 TypeScript

> TypeScript is JavaScript with syntax for types (TypeScript 是一个使用了 types 类型的 JavaScript 语言)。
> 添加了类型系统的 JavaScript，适用于任何规模的项目。

上面的英文是从官方网站 <sup>[[1]](#link-1)</sup> 上抄录下来的。

从上面的文字，可以简单的理解就是针 JavaScript 语言，TypeScript 添加了「类型（types）」。 如果你写过或者了解 Java 程序的，你会知道 Java 在定义
变量的时候需要对变量的类型进行定义。

在实际使用的时候，因为变量的类型进行了定义，因此 Java 语言就涉及到类型转换，比如说要把 String 转换为 Int，虽然 Java 对其类型转换进行了一些包装，但是整个转换过程还是有点学习曲线的。

对比 Java 而言，JavaScript 就完全不需要对类型进行定义了，JavaScript 会在运行的时候帮你进行类型的自动判断和转换。这个就导致 JavaScript 非常灵活，灵活的同时就会带来困惑，
原因是你在程序运行的时候，完全不知道你的变量是什么类型的，这会导致一些莫名其妙的错误发生，而且 Debug 的时候也是比较纠结。

## TypeScript 语言特性 
JavaScript 是一门非常灵活的编程语言，在了解为什么要有 TypeScript 之前，觉得还是有必要说说这个世界对 JavaScript 的误解。

### JavaScript 语言特性和不足
因为 JavaScript 堪称世界上被人误解最深的编程语言。虽然常被嘲为“玩具语言”，但在它看似简洁的外衣下，还隐藏着强大的语言特性。 

JavaScript 目前广泛应用于众多知名应用中，对于网页和移动开发者来说，深入理解 JavaScript 就尤为必要。

我们有必要先从这门语言的历史谈起。在1995 年 Netscape 一位名为 Brendan Eich 的工程师创造了 JavaScript，随后在 1996 年初，JavaScript 首先被应用于 Netscape 2 浏览器上。最初的 JavaScript 名为 LiveScript，但是因为一个糟糕的营销策略而被重新命名，该策略企图利用Sun Microsystem 的 Java 语言的流行性，将它的名字从最初的 LiveScript 更改为 JavaScript——尽管两者之间并没有什么共同点。 

这便是之后混淆产生的根源。

> 敲黑板：JavaScript 和 Java 一点关系都没有，甚至可以说是 2 个完全不同的动物。

几个月后，Microsoft 随 IE 3 发布推出了一个与之基本兼容的语言 JScript。
又过了几个月，Netscape 将 JavaScript 提交至 Ecma International（一个欧洲标准化组织）， ECMAScript 标准第一版便在 1997 年诞生了，随后在 1999 年以 ECMAScript 第三版的形式进行了更新，从那之后这个标准没有发生过大的改动。由于委员会在语言特性的讨论上发生分歧，ECMAScript 第四版尚未推出便被废除，但随后于 2009 年 12 月发布的 ECMAScript 第五版引入了第四版草案加入的许多特性。
第六版标准已经于 2015 年 6 月发布。

如果要说说 JavaScript 还有什么特性的话就是大致可以考虑下有：
- 它没有类型约束，一个变量可能初始化时是字符串，过一会儿又被赋值为数字。
- 由于隐式类型转换的存在，有的变量的类型很难在运行前就确定。
- 基于原型的面向对象编程，使得原型上的属性或方法可以在运行时被修改。
- 函数是 JavaScript 中的一等公民<sup>[[2]](#link-2)</sup>，可以赋值给变量，也可以当作参数或返回值。
- JavaScript 的代码质量参差不齐，维护成本高，运行时错误多多。

针对 Java 程序员来说，最最头疼重要的就是 **JavaScript 毫无章法的变量类型**，完全不知道自己的变量是什么，和另外一个就是 JavaScript 是一种解释型的脚本语言，
与 Java 等语言先编译后执行不同, JavaScript 是在程序的运行过程中逐行进行解释。这就导致 **JavaScript 的很多错误在编译的过程中无法发现，运行后又问题多多**。

### TypeScript 类型系统
针对 JavaScript 上面的问题，聪明的同学就想那我们就给 JavaScript 加个类型吧，和 Java 一样，能够对变量的类型进行定义，这个想法就是 TypeScript 的类型系统,
在很大程度上弥补了 JavaScript 的带来的困惑。

从 TypeScript 的名字就可以看出来，「类型」是其最核心的特性，TypeScript 也主要致力于解决 JavaScript 的类型混乱问题。

#### TypeScript 是静态类型

类型系统按照「类型检查的时机」来分类，可以分为下面 2 种
* 动态类型
* 静态类型

**动态类型**是指在运行时才会进行类型检查，这种语言的类型错误往往会导致运行时错误。
JavaScript 是一门解释型语言<sup>[[4]](#link-4)</sup>，没有编译阶段（这个就是另外一个针对 Java 同学经常吐槽的地方），所以它是动态类型，以下这段代码在运行时才会报错：

```js
let foo = 1;
foo.split(' ');
// Uncaught TypeError: foo.split is not a function
// 运行时会报错（foo.split 不是一个函数），在运行的时候造成 bug。
// 打开你浏览器 F12 看看上面有多少错误你就能了解到了。
```

**静态类型**是指编译阶段就能确定每个变量的类型，这种语言的类型错误往往会导致语法错误。TypeScript 在运行前需要先编译为 JavaScript，而在编译阶段就会进行类型检查，所以 **TypeScript 是静态类型**，这段 TypeScript 代码在编译阶段就会报错了：

```ts
let foo = 1;
foo.split(' ');
// Property 'split' does not exist on type 'number'.
// 编译时会报错（数字没有 split 方法），无法通过编译
```

你可能会奇怪，这段 TypeScript 代码看上去和 JavaScript 没有什么区别呀。

没错！大部分 JavaScript 代码都只需要经过少量的修改（或者完全不用修改）就变成 TypeScript 代码，这得益于 TypeScript 强大的[类型推论][]，即使不去手动声明变量 `foo` 的类型，也能在变量初始化时自动推论出它是一个 `number` 类型。

完整的 TypeScript 代码是这样的：

```ts
let foo: number = 1;
foo.split(' ');
// Property 'split' does not exist on type 'number'.
// 编译时会报错（数字没有 split 方法），无法通过编译
```

#### TypeScript 是弱类型

类型系统按照「是否允许隐式类型转换」来分类，可以分为强类型和弱类型。

以下这段代码不管是在 JavaScript 中还是在 TypeScript 中都是可以正常运行的，运行时数字 `1` 会被隐式类型转换为字符串 `'1'`，加号 `+` 被识别为字符串拼接，所以打印出结果是字符串 `'11'`。

```js
console.log(1 + '1');
// 打印出字符串 '11'
```

TypeScript 是完全兼容 JavaScript 的，它不会修改 JavaScript 运行时的特性，所以 **它们都是弱类型**。

与弱类型对应的就是强类型语言，比如说 Java。
强类型语言是一种强制类型定义的语言，即一旦某一个变量被定义类型，如果不经强制转换，那么它永远就死该数据类型。 强类型语言包括：Java、.net、Python、C++ 等语言。

虽然有时候 Java 也会给你做一些隐式转换，但是大部分情况类型不匹配，在编译的时候就会报错了。


例如，我们可以看看下面的 Python 代码，因为 Python 是强类型，以下代码会在运行时报错：

```py
print(1 + '1')
# TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

若要修复该错误，需要进行强制类型转换：

```py
print(str(1) + '1')
# 打印出字符串 '11'
```

> 强/弱是相对的，Python 在处理整型和浮点型相加时，会将整型隐式转换为浮点型，但是这并不影响 Python 是强类型的结论，因为大部分情况下 Python 并不会进行隐式类型转换。
> 相比而言，JavaScript 和 TypeScript 中不管加号两侧是什么类型，都可以通过隐式类型转换计算出一个结果——而不是报错——所以 JavaScript 和 TypeScript 都是弱类型。

> 虽然 TypeScript 不限制加号两侧的类型，但是我们可以借助 TypeScript 提供的类型系统，以及 ESLint 提供的代码检查功能，来限制加号两侧必须同为数字或同为字符串<sup>[[5]](#link-5)</sup>。
> 这在一定程度上使得 TypeScript 向「强类型」更近一步了——当然，这种限制是可选的。

这样的类型系统体现了 TypeScript 的核心设计理念<sup>[[6]](#link-6)</sup>：在完整保留 JavaScript 运行时行为的基础上，通过引入静态类型系统来提高代码的可维护性，减少可能出现的 bug。

这就是为什么对 Java 同学来说，可能更喜欢 TypeScript 一些。

### 适用规模和迁移性
TypeScript 非常适用于大型项目——这是显而易见的，类型系统可以为大型项目带来更高的可维护性，以及更少的 bug。

在中小型项目中推行 TypeScript 的最大障碍就是认为使用 TypeScript 需要写额外的代码，降低开发效率。但事实上，由于有[类型推论][]，大部分类型都不需要手动声明了。
相反，TypeScript 增强了编辑器（IDE）的功能，包括代码补全、接口提示、跳转到定义、代码重构等，这在很大程度上提高了开发效率。
而且 TypeScript 有近百个[编译选项][]，如果你认为类型检查过于严格，那么可以通过修改编译选项来降低类型检查的标准。

TypeScript 与 JavaScript 是共存的。这意味着如果你有一个使用 JavaScript 开发的旧项目，又想使用 TypeScript 的特性，那么你并不需要把整个项目都迁移到 TypeScript，
你可以使用 TypeScript 编写新文件，然后在后续更迭中逐步迁移旧文件。

如果一些 JavaScript 文件的迁移成本太高，TypeScript 也提供了一个方案，可以让你在不修改 JavaScript 文件的前提下，编写一个[类型声明文件][]，实现旧项目的渐进式迁移。

事实上，就算你从来没学习过 TypeScript，你也可能已经在不知不觉中使用到了 TypeScript——在 VSCode 编辑器中编写 JavaScript 时，代码补全和接口提示等功能就是通过 TypeScript Language Service 实现的<sup>[[7]](#link-7)</sup>：

![what-is-typescript-vscode](../assets/what-is-typescript-vscode.png)

一些第三方库原生支持了 TypeScript，在使用时就能获得代码补全了，比如 Vue 3.0<sup>[[8]](#link-8)</sup>：

![what-is-typescript-vue](../assets/what-is-typescript-vue.png)

有一些第三方库原生不支持 TypeScript，但是可以通过安装社区维护的类型声明库<sup>[[9]](#link-9)</sup>（比如通过运行 `npm install --save-dev @types/react` 来安装 React 的类型声明库）来获得代码补全能力——不管是在 JavaScript 项目中还是在 TypeScript 中项目中都是支持的：

![what-is-typescript-react](../assets/what-is-typescript-react.png)

TypeScript 的发展已经深入到前端社区的方方面面了，任何规模的项目都或多或少得到了 TypeScript 的支持。
同时 TypeScript 也能够帮助解决 JavaScript 诟病的问题。

### 与标准同步发展

TypeScript 的另一个重要的特性就是坚持与 ECMAScript 标准<sup>[[10]](#link-10)</sup>同步发展。

ECMAScript 是 JavaScript 核心语法的标准，自 2015 年起，每年都会发布一个新版本，包含一些新的语法。

一个新的语法从提案到变成正式标准，需要经历以下几个阶段：

- Stage 0：展示阶段，仅仅是提出了讨论、想法，尚未正式提案。
- Stage 1：征求意见阶段，提供抽象的 API 描述，讨论可行性，关键算法等。
- Stage 2：草案阶段，使用正式的规范语言精确描述其语法和语义。
- Stage 3：候选人阶段，语法的设计工作已完成，需要浏览器、Node.js 等环境支持，搜集用户的反馈。
- Stage 4：定案阶段，已准备好将其添加到正式的 ECMAScript 标准中。

一个语法进入到 Stage 3 阶段后，TypeScript 就会实现它。一方面，让我们可以尽早的使用到最新的语法，帮助它进入到下一个阶段；另一方面，处于 Stage 3 阶段的语法已经比较稳定了，基本不会有语法的变更，这使得我们能够放心的使用它。

除了实现 ECMAScript 标准之外，TypeScript 团队也推进了诸多语法提案，比如可选链操作符（`?.`）<sup>[[11]](#link-11)</sup>、空值合并操作符（`??`）<sup>[[12]](#link-12)</sup>、Throw 表达式<sup>[[13]](#link-13)</sup>、正则匹配索引<sup>[[14]](#link-14)</sup>等。

## TypeScript 总结
TypeScript 的出现就是为了解决 JavaScript 发展过程中遇到的因为类型问题出现的奇葩错误。

简单来说就是：
 - TypeScript 增强了 JavaScript 语言特性，通过添加类型尽量减少 Bug 和错误。
 - TypeScript 与 JavaScript 是完全兼容的。
 - TypeScript 可以编译为 JavaScript，然后运行在任何可以运行 JavaScript 的环境中。
 - TypeScript 拥有复杂编译选项，让程序员可以自行控制编译输出，从另外的角度来说这个增加了编译配置的难度和学习曲线。
 - TypeScript 可以完全 JavaScript 共存。JavaScript 项目能够渐进式的迁移到 TypeScript，但因为接口暴露的问题，有些 JavaScript 代码在迁移的时候会出现编译错误。
 - TypeScript 增强了编辑器（IDE）的功能，为 IDE 提供更多的编辑选项，通过这些编辑选项来尽量降低错误。
 - TypeScript 与标准同步发展，符合最新的 ECMAScript 标准（stage 3）。

## TypeScript 的发展历史

- 2012-10：微软发布了 TypeScript 第一个版本（0.8），此前已经在微软内部开发了两年。
- 2014-04：TypeScript 发布了 1.0 版本。
- 2014-10：Angular 发布了 2.0 版本，它是一个基于 TypeScript 开发的前端框架。
- 2015-01：ts-loader 发布，webpack 可以编译 TypeScript 文件了。
- 2015-04：微软发布了 Visual Studio Code，它内置了对 TypeScript 语言的支持，它自身也是用 TypeScript 开发的。
- 2016-05：`@types/react` 发布，TypeScript 可以开发 React 应用了。
- 2016-05：`@types/node` 发布，TypeScript 可以开发 Node.js 应用了。
- 2016-09：TypeScript 发布了 2.0 版本。
- 2018-06：TypeScript 发布了 3.0 版本。
- 2019-02：TypeScript 宣布由官方团队来维护 typescript-eslint，以支持在 TypeScript 文件中运行 ESLint 检查。
- 2020-05：Deno 发布了 1.0 版本，它是一个 JavaScript 和 TypeScript 运行时。
- 2020-08：TypeScript 发布了 4.0 版本。
- 2020-09：Vue 发布了 3.0 版本，官方支持 TypeScript。

## 参考资料

1. <span id="link-1">[TypeScript 官网](https://www.typescriptlang.org/)</span>
2. <span id="link-2">[第 2 章: 一等公民的函数](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch2.html) · 函数式编程指北</span>
3. <span id="link-3">[StackOverflow 2020 开发者调查报告](https://insights.stackoverflow.com/survey/2020)</span>
4. <span id="link-4">[斯坦福 JavaScript 第一课](https://web.stanford.edu/class/cs98si/slides/overview.html)</span>
5. <span id="link-5">[TypeScript ESLint 规则 `restrict-plus-operands`](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/docs/rules/restrict-plus-operands.md)</span>
6. <span id="link-6">[TypeScript 设计理念](https://github.com/microsoft/TypeScript/wiki/TypeScript-Design-Goals)</span>
7. <span id="link-7">[Visual Studio Code 中集成了 TypeScript](https://code.visualstudio.com/docs/languages/typescript)</span>
8. <span id="link-8">[Vue 3.0 支持 TypeScript](https://v3.vuejs.org/guide/typescript-support.html)</span>
9. <span id="link-9">[Definitely Typed](https://github.com/DefinitelyTyped/DefinitelyTyped)——TypeScript 团队帮助维护的类型定义仓库</span>
10. <span id="link-10">[ECMAScript 标准](https://tc39.es/process-document/)</span>
11. <span id="link-11">[可选链操作符（`?.`）](https://github.com/tc39/proposal-optional-chaining)</span>
12. <span id="link-12">[空值合并操作符（`??`）](https://github.com/tc39/proposal-nullish-coalescing)</span>
13. <span id="link-13">[Throw 表达式](https://github.com/tc39/proposal-throw-expressions)</span>
14. <span id="link-14">[正则匹配索引](https://github.com/tc39/proposal-regexp-match-indices)</span>