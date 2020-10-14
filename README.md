# v8-javascript-memory

V8 JavaScript 内存占用分析。

## 步骤

1. 使用 Chrome 浏览器访问 <https://justjavac.com/v8-javascript-memory/>

1. 打开 Dev Tools，如图：

![](./screen.png)

    1. 选择 Memory 标签页
    1. 点击 take heap snapsshot
    1. 在过滤框中输入 `ho` 快速过滤出 holder

## 名次解释

**Shallow Size**：对象自身占用内存的大小，不包括它引用的对象。JavaScript 对象会将一些内存用于自身的说明和保存中间值。通常，只有数组和字符串会有明显的浅层大小。

**Retained Size**：这是将对象本身连同其无法从 **GC root** 到达的相关对象一起删除后释放的内存大小。

单位是字节(Byte)。

## 分析

从截图中可以看到，`Symbol()` 的内存占用是 16。

`Object.create(null)` 自身占用 12，总占用 88。

`{}` 自身占用 28，总占用 28。

继续展开你会看到其他信息：

![](./screen2.png)

1. `__proto__` 是原型链。
2. `map` 就是很多文章都在介绍的 V8 对象的黑魔法 Hidden Class。