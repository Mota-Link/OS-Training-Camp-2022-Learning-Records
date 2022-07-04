# OS-Training-Camp-2022-Learning-Records
2022年开源操作系统训练营 - 学习记录
---
## 2022-07-01
学习Rust圣经 3.2.1章：理解并掌握了Rust的闭包、Fn系列特征。

闭包较难理解的一点是**捕获方式**、**Fn系列特征**、**使用方式**三者之间的关系。

理解后梳理如下：

- 闭包实现的**Fn系列特征**，取决于自由变量在闭包内的**使用方式**。
- 自由变量的**捕获方式**，取决于闭包实现的**Fn系列特征**。
- `move`关键字：能改变自由变量的**捕获方式**，但不影响实现的**Fn系列特征**。（原因见第一点）

## 2022-07-02
思考：闭包的生命周期。

Rust圣经之中，对闭包的生命周期一笔带过，遂去其他地方搜索，得出闭包的生命周期主要通过**Fn系列特征**来显式标注。

而对**Fn系列特征**进行生命周期标注时，有时候会有**Early bound**与**Late bound**的区别冲突，为此引入了**HRTB**。

此时深感当初生命周期章节学得不扎实，欠下了许多技术债。

## 2022-07-03
深入学习了昨天未学完的HRTB相关知识，并参考《Rust参考手册》对生命周期相关的知识进行了查漏补缺。

在生命周期省略的章节，发现了许多没学过的用法：在trait对象上进行生命周期省略。

与昨天的闭包生命周期知识点相结合，又扣上了缺失的一环。

## 2022-07-04
学习Rust圣经 3.2.2章：理解迭代器

迭代器对于我来说还算是比较陌生的概念，所以理解的时候免不了磕磕绊绊、绕进误区。

我主要遇到的误区如下：

**1. 跟闭包一样，迭代器有独立的、复杂的“迭代器类型”？**

> 错，迭代器可以是任何类型：只要实现了`Iterator`特征.

  

**2. Array 与 Vec 都是迭代器类型？**

> 不是，它们调用`.into_iter()`转换成的迭代器是`IntoIter`类型.

  

**3. `iter()`与`iter_mut()`与`into_iter()`分别来源于不同的trait？**

> 否，都是来源于`IntoIterator trait`，只不过标准库里对于`T`、`&T`、`&mut T`都实现一次这个trait。
> 
> `iter()`与`iter_mut()`实际上是对应`&T`与`&mut T`实现的`into_iter()`方法的别名。

若理解有错，还请指正！

