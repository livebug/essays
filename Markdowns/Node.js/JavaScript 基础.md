# 使用 Node.js 需要了解多少 JavaScript

在深入研究 Node.js 之前，我建议您能很好地掌握主要的 JavaScript 概念：


## 1. 计算耗时

```js
const doSomething = () => {
    let sum = 0;
    for (let index = 0; index < 10000; index++) {
        sum += 1
    }
    console.log(sum);
}
const measureDoingSomething = () => {
  console.time('doSomething()')
  //做点事，并测量所需的时间。
  doSomething()
  console.timeEnd('doSomething()')
}
measureDoingSomething()
```

## 2. 命令行交互 https://github.com/SBoudrias/Inquirer.js
```js
import pkg from 'inquirer';

var questions = [
  {
    type: 'input',
    name: 'name',
    message: "你叫什么名字?"
  }
]

pkg.prompt(questions).then(answers => {
  console.log(`你好 ${answers['name']}!`)
})
```

# 推荐库
|库|说明|
|--|---|
|[`Chalk`](https://github.com/chalk/chalk)|为控制台输出着色的最简单方法是使用库。 Chalk 是一个这样的库，除了为其着色外，它还有助于其他样式的设置（例如使文本变为粗体、斜体或带下划线）。|
|[readline](http://nodejs.cn/api/readline.html)|Node.js 提供了 readline 模块来执行以下操作：每次一行地从可读流（例如 process.stdin 流，在 Node.js 程序执行期间该流就是终端输入）获取输入。|
|[Inquirer.js](https://github.com/SBoudrias/Inquirer.js)|Inquirer.js 软件包则提供了更完整、更抽象的解决方案。 命令行交互|