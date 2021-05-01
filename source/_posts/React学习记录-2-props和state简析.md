---
title: React学习记录-2-props和state简析
date: 2020-08-11 23:19:15
tags:
---

<!-- TOC -->

- [React 学习记录-2-props 和 state 简析 - 逻辑协会 - 博客园](#react学习记录-2-props和state简析---逻辑协会---博客园)
  - [前言](#前言)
  - [第一个问题：props 是什么，state 是什么](#第一个问题props是什么state是什么)
  - [类(class)属性](#类class属性)
  - [实例属性](#实例属性)
  - [第二个问题：props 和 state，有什么区别？](#第二个问题props和state有什么区别)
  - [props](#props)
    - [延伸问题-1：为什么 props 是不可变的？](#延伸问题-1为什么props是不可变的)
  - [state](#state)
  - [小结](#小结)

<!-- /TOC -->

# React 学习记录-2-props 和 state 简析 - 逻辑协会 - 博客园

## 前言

下面的代码，来自菜鸟教程 [这篇文章](https://www.runoob.com/react/react-state.html) 。

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
```

## 第一个问题：props 是什么，state 是什么

```
constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

通过 [前篇](https://www.cnblogs.com/gnuzsx/p/11923570.html) 的努力，
我已经能够知道 `constructor()` 函数，是一个构造器函数，是一个挂载生命周期方法了。
为什么 `constructor()` 函数构造组件类的时候，要传入 `props` ，这个 `props` 到底是什么？
函数体当中，有一个 `this.state` 。this 我们知道指代的是 `Clock` 这个类。那么这个 `state` 又是什么呢？

首先需要说明的是，props 和 state 是组件的两个 `属性` 注意，是属性。

前篇文章，关于组件生命周期学习的过程中，我主要参考了 [这个文章](https://react.docschina.org/docs/react-component.html)

组件是一个类，类就是对象。具体类就是实例。

> 类、对象、实例，这几个概念是同一个层级的。 类=对象=实例 类=方法+属性。

> 组件类=生命周期方法+属性。

在 [这篇文章](https://react.docschina.org/docs/react-component.html) 中提到 `class属性` 和 `实例属性` 。

## 类(class)属性

## 实例属性

从这里我们可以知道 `props` 和 `state` 是组件实例的一个属性。 在构造器函数被调用的时候，是构造了组件实例，当然是要传入组件的属性的。

但是，为什么 `props` 是在函数的参数列表中，

而 `state` 是在函数体当中呢？
`props` 和 `state` 两个属性，又有什么不同呢？

## 第二个问题：props 和 state，有什么区别？

在这里，我主要参考了 [这篇文章](https://www.cnblogs.com/ice--cream/p/8927091.html)

React 的核心思想就是 `组件化思想` 。
意思就是：页面会被切分成一些独立的、可服用的组件。

## props

组件从概念上看，就是一个函数，可以接受一个参数作为输入值。 这个参数，就是 props。

所以，可以把 props 理解为 **从外部传入组件内部的数据** 。

由于 React 是单向数据流，

所以 props 基本上，就是 **从父级组件向子级组件传递的数据** 。

props 经常被用作 **渲染组件** 和 **初始化状态** 。
当一个组件被实例化之后，它的 `props` 是只读的，不可改变的。

### 延伸问题-1：为什么 props 是不可变的？

如果 `props` 在渲染过程中可以被改变，那么会导致这个组件显示的形态变得不可预测。
只有通过父组件重新渲染的方式，才能够把新的 `props` 传入组件中。

> props 的本质：从外部传进组件的参数，方便父组件向子组件传递参数。  
> props 的性质：可读性、不可变性。

## state

state 就是组件内部数据的状态，是可以被改变的。

1. 在组件初始化的时候，构造函数中，通过 `this.state` 给组件设定一个初始的 state，在第一次 render 的时候就会用这个数据来渲染组件。
2. 修改 state 的时候，通过 `this.setState()` 方法来进行修改。 state 的主要作用，是组件用来保存、控制、修改自己的状态。

3. 它只能够在 `constructor` 当中初始化。

4. 它可以算是组件的 `私有属性` ，不可以通过外部访问和修改。
5. 只能够通过组件内部来修改， **修改 state 属性会导致组件的重新渲染** 。
   > 一个组件的显示形态由两部分组成：外部参数、内部数据状态。 外部参数就是 props。内部数据状态就是 state。

> props 和 state 的区别是：

1. state 是组件自己管理数据，控制自己的状态，可以改变。
2. props 是外部传入的数据参数，不可以改变。
3. 没有 state 的组件，叫做无状态组件。有 state 的组件，叫做有状态组件。
4. 多用 props，少用 state。多写无状态组件，少写有状态组件。

```
constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

在这个构造函数中， `super(props)` 就不用说了。 this.state 是为了初始化组件的状态。

{}在 javascript 当中表示的是一个对象。说明，它是 **用一个对象来初始化组件的状态** 的。

在 javascript 当中，变量是数据值的容器。

对象也是变量，包含了很多值，对象中的值以 `键值对` 的方式来书写。

参考 [这篇文章](https://www.w3school.com.cn/js/js_objects.asp) 进行理解。

## 小结

通过这一篇的讨论，主要是理解了 props 和 state 两个东西是什么。 也初步地，了解了一下 react 的设计思想。

最终是理解了【前言】代码当中构造器函数的书写内容。

[React 学习记录-2-props 和 state 简析 - 逻辑协会 - 博客园](https://www.cnblogs.com/gnuzsx/p/11923828.html)
