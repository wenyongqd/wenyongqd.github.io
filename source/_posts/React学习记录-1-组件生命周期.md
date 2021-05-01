---
title: React学习记录-1-组件生命周期
date: 2020-08-11 23:17:22
tags:
---

<!-- TOC -->

- [React 学习记录-1-组件生命周期 - 逻辑协会 - 博客园](#react学习记录-1-组件生命周期---逻辑协会---博客园)
  - [前言](#前言)
  - [第一个问题：React.Component 是什么意思？](#第一个问题reactcomponent是什么意思)
  - [第二个问题：什么是 DOM？](#第二个问题什么是dom)
  - [第三个问题：什么是组件的生命周期？](#第三个问题什么是组件的生命周期)
  - [1. 挂载](#1-挂载)
  - [2. 更新](#2-更新)
  - [3. 卸载](#3-卸载)
  - [4. 错误处理](#4-错误处理)
  - [小结](#小结)

<!-- /TOC -->

# React 学习记录-1-组件生命周期 - 逻辑协会 - 博客园

## 前言

准备学习前端。
从【反动君】的文章中，我知道了 `系统性学习` 这个词语。 他说的是很对的。系统性学习，是很难的。 作为一个在技术公司做综合工作的人，我产生了系统性学习技术的兴趣。 就从前端开始吧。 先确立学习的方法论。

我的方法是：系统性学习分为有限数量的点，将每个点都理解，贴上标签，划分优先级，排列分布。最终才产生应用的价值。

```
class Clock extends React.Component{
  constructor(props){
    super(props);
    this.state = {date:new Date()};
  }

  componentDidMount(){
    this.timerID = setInterval(() => this.tick(),1000);
  }

  componentWillUnmount(){
    clearInterval(this.timerID);
  }

  tick(){
    this.setState({date:new Date()});
  }

  render(){
    return(
      <div>
        <h1>Hello,world!</h1>
        <h2>现在是{this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }

  ReactDOM.render(
    <Clock />,
    document.getElementById('example')
  );
}
```

这是菜鸟教程的 [这篇文章](https://www.runoob.com/react/react-state.html) 中的代码。

## 第一个问题：React.Component 是什么意思？

在 React 前端框架当中，有一个 `组件` 的概念。
这个 `组件` 是可以两种定义的形式： `类(class)` 和 `函数` 。

> 既然有两种形式，那么怎么决定，什么时候用哪一种呢？ 这可以作为一个【待确认问题】。

> 首先可以确定的是，class 组件目前是提供了更多的功能。

如果是定义 class 组件，就是上面代码中的如下部分：

```
class Clock extends React.Component{
  constructor(props){
    super(props);
    this.state = {date:new Date()};
  }
```

这里 `extends` 英文翻译是 `延伸` 的意思，可以引申为 `继承` 的意思。
第一句话，是说有一个类 Clock，是继承自 `React.Component` 的。
也就是说，Clock 是 `React.Component` 的子类。

> 这里 Component 就是组件的意思。 React.Component 好像是所有组件类的爹的样子。 它是所有组件类的爹，它最牛逼。

> Component 的源代码在 ReactBaseClasses.js 中。

上面的代码，就是创建了一个 `Clock组件` 了。

## 第二个问题：什么是 DOM？

DOM，是 `document object model` 的缩写。 意思是文档对象模型。 本意上，它是一种接口(API)，类似一种操作方法。

比如说 `HTML DOM` 就是访问和操作 HTML 文档的标准方法。

但是，在一般性的表达中，DOM 还具有一层经常使用的指代意思。

就是 `DOM就是文档` 。

在【第一个问题】中，我们是创建了 React 的组件。
组件是一个类，是一个对象，所以，组件是有实例的。

> 当组件实例被创建并插入到 DOM 当中的时候。  
> 这句话中，我就可以理解 DOM，指代的就是文档。

## 第三个问题：什么是组件的生命周期？

组件的生命周期，有几个阶段： `挂载` ， `更新` ， `卸载` ， `错误处理` 。
组件的每个阶段都包含 `生命周期方法` 。

> 注意：加粗的，都是组件常用的生命周期方法。不加粗的，不常用。

## 1. 挂载

当组件实例被创建，并且插入到 DOM 当中的时候，这个过程叫做挂载。
组件挂载的生命周期方法的调用顺序如下：

- **constructor()** //constructor 英文是构造器的意思。
- static getDerivedStateFromProps() //Derive 英文是从...中获得。从 Props 中获得派生状态(State)。
- **render()** //render 英文意思是提供，提出，使成为的意思。
- **compenentDidMount()** //Mount 英文的意思，是安装...于高处的意思。翻译为挂载。
  我看挂载的顺序就是 `构造 - 获取派生状态 - 提供 - 安装` 。

## 2. 更新

当组件的 props 或 state 发生变化的时候，会触发更新。

> props 是属性？state 是状态？

组件更新的生命周期方法调用顺序如下：

- static getDerivedStateFromProps() //从 props 当中获得派生状态
- shouldComponentUpdate() // 判断组件是否应该更新
- **render()** //提供
- getSnapshotBeforeUpdate() // 组件更新前获得快照(Snapshot)
- **componentDidUpdate()** //组件实施更新

## 3. 卸载

当组件从 DOM 当中移除的时候，会调用如下的方法：

- **componentWillUnmount()** //组件将会卸载

## 4. 错误处理

当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：

- static getDerivedStateFromError() //从 Error 中获得派生状态。
- componentDidCatch() //组件执行捕获异常
  > 到了这里，我基本上能够看懂：【前言】代码中 componentDidMount()和 componentWillUnmount() 这两个函数，都是生命周期方法，一个是挂载的，一个是卸载的。 这两个方法被叫做【生命周期钩子】。 constructor()和 render()也是生命周期方法。

> 但是代码里面的内容，我还是不太理解。

## 小结

为了使我的问题点，能够有清晰的界限。我先决定一篇文章，就记录 3 个问题。 主要是理解了【前言】代码中的几个函数的作用。

对这一段代码的完全理解，还没有达到。

[React 学习记录-1-组件生命周期 - 逻辑协会 - 博客园](https://www.cnblogs.com/gnuzsx/p/11923570.html)
