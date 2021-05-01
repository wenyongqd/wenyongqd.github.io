---
title: React学习记录-3-箭头函数、定时器、动态对象、代码执行逻辑
date: 2020-08-12 09:15:01
tags:
---
# React学习记录-3-箭头函数、定时器、动态对象、代码执行逻辑 
## 前言
<!-- TOC -->

- [React学习记录-3-箭头函数、定时器、动态对象、代码执行逻辑](#react学习记录-3-箭头函数定时器动态对象代码执行逻辑)
    - [前言](#前言)
    - [第一个问题：怎么理解() => this.tick()](#第一个问题怎么理解--thistick)
    - [箭头函数的第一种书写格式](#箭头函数的第一种书写格式)
    - [箭头函数的第二种书写格式](#箭头函数的第二种书写格式)
    - [参数不是一个箭头函数的书写方式](#参数不是一个箭头函数的书写方式)
    - [返回值是对象的箭头函数的书写方式](#返回值是对象的箭头函数的书写方式)
    - [箭头函数是修正了this使用过程中的错误](#箭头函数是修正了this使用过程中的错误)
    - [() => this.tick()的理解](#--thistick的理解)
    - [第二个问题：setInterval()函数是怎么用的？](#第二个问题setinterval函数是怎么用的)
    - [第三个问题：this.timerID是怎么理解的？](#第三个问题thistimerid是怎么理解的)
    - [动态对象](#动态对象)
    - [固定对象](#固定对象)
    - [小结](#小结)

<!-- /TOC -->
作为我来说，对自己未知的领域，总是充满好奇。 对于公司那些整体忘我讨论技术问题的同事，我总是持有疑问： 是什么东西，让他们能够这样热烈、投入、废寝忘食讨论。 既然能够让人有这样的热情，那么势必如美食美景一样，是值得探索的。

我希望自己能够一窥技术世界的究竟。

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

## 第一个问题：怎么理解() => this.tick()

这是ES6中声明函数的一种方式，叫做 `箭头函数表达式` 。
ES6是指 `ECMAScript6` 。
为什么引入 `箭头函数(Arrow Function)`? 有两个方面的作用： 第一、这是更简短的函数。(这好理解。)

第二、不用绑定this。( **这不知道什么意思。** )

箭头函数有两种书写格式。

## 箭头函数的第一种书写格式

以前写函数的方式是：

```
function(x){
  return x*x;
}
```

换成箭头函数，就写成：

```
x => x*x
```

## 箭头函数的第二种书写格式

以前写函数的方式是：

```
function(x){
  if(x>0){
    retun x*x;
  }
  else{
    retun - x*x;
  }
}
```

用箭头表达式来写，就是下面的形式：

```
x => {
    if (x > 0) {
        return x * x;
    }
    else {
        return - x * x;
    }
}
```

## 参数不是一个箭头函数的书写方式

```
// 无参数:
() => 3.14

// 两个参数:
(x, y) => x * x + y * y

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```

## 返回值是对象的箭头函数的书写方式

```
//这么写是不对的
x => { foo: x }
//这么写是对的
x => ({ foo: x })
```

## 箭头函数是修正了this使用过程中的错误

javascript中有一个错误，就是 `函数对于this绑定的错误处理` 。
可以看下面的例子：

```
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = function () {
            return new Date().getFullYear() - this.birth; // this指向window或undefined
        };
        return fn();
    }
};
```

上面的例子中，使用this，就有问题。 第一个this，是外部函数中this还能够使用对象。 第二个this，内部函数中this已经指向不到对象了。

下面的例子中，使用箭头函数，就没有问题。

```
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
        return fn();
    }
};
obj.getAge(); // 25
```

用官方的说法是：箭头函数就是为了确定this的 `词法作用域` 。
这种绑定，让你即便使用 `call()`、`apply()` 调用箭头函数的时候，也没有办法改变this的绑定。
如下所示：

```
var obj = {
    birth: 1990,
    getAge: function (year) {
        var b = this.birth; // 1990
        var fn = (y) => y - this.birth; // this.birth仍是1990
        return fn.call({birth:2000}, year);
    }
};
obj.getAge(2015); // 25
```

## () => this.tick()的理解

这是一个没有参数的函数。返回的是 `this.tick()` 。 这里的this当然指的就是组件对象。 this.tick()就是组件的tick()方法。

我们能够从【前言】的代码中看到组件中是有这个tick()方法的。

```
tick() {
    this.setState({
      date: new Date()
    });
  }
```

tick()方法当中修改了组件的state状态。 是用一个对象{date:new Date()}修改了state的状态。 tick()方法返回的就是这个对象。

这个对象有一个date属性，值是new Date()。

() => this.tick()
如果用常规的方法来写，是这样子的：

```
let that = this;
this.timerID = setInterval(function(){
   return that.tick(); 
},1000)
```

## 第二个问题：setInterval()函数是怎么用的？

setInterval()的主要作用是：周期地调用并执行一个函数。
基本的语法，是这样的：

```
setInterval(函数名，执行周期)
```

在这里例子当中，

```
this.timerID = setInterval(
      () => this.tick(),
      1000
    );
```

表示的就是1秒钟就要调用一次 `this.tick()` 这个函数。
详情我是参考的 [这篇文章](https://jingyan.baidu.com/article/ff4116251f25f012e4823799.html)

## 第三个问题：this.timerID是怎么理解的？

这个涉及到javascript当中对象属性的添加问题。 这个有两种方法：

这里，我是参考 [这篇文章](https://www.cnblogs.com/xielong/p/9377447.html) 理解的。

## 动态对象

```
//创建obj对象
    var obj = new Object();
    //为对象添加动态属性
    obj.userName = "admin";
    obj.passWord = "123456";
    //输出
    console.log(obj);
```

删除对象属性

```
//创建obj动态对象
    var obj = new Object();
    //为对象添加动态属性
    obj.userName = "admin";
    obj.passWord = "123456";    
    //移除属性
    delete obj.passWord;
    console.log(obj);
```

## 固定对象

```
//创建固定对象
    var dt = {userName:"admin",password:"123456"};
    console.log(dt);
```

## 小结

这段代码，到这里，是基本上可以理解了。

```
//声明了一个组件类叫做Clock，继承自React.Component
class Clock extends React.Component {
  
  //这是组件类的构造函数，里面初始化了组件的状态state。
  //这是挂载时候，执行的生命周期方法的第一个。
  constructor(props) {
    super(props);
    this.state = {date: new Date()};//初始化了组件的状态state。
  }
 
 //这是组件挂载的生命周期函数，表示组件执行挂载的方法。
 //代码是重写了这个方法，表示在挂载的时候，设置了一个定时器。
 //组件类是一个动态对象，所以this.timerID表示是一个定时属性。
 //这个属性是一个setInterval函数，每1秒执行一个函数，就是tick()
 //采用()=>this.tick()是因为要限定this的词法作用域
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
 
  //这是组件的卸载方法。
  //代码重写了这个方法，然后在卸载的时候，清除定时器。
  //清除定时器，采用的方法，就是clearInterval()方法。 
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
 
  //这是自定义的组件类方法。
  //方法内是更新设置了组件的状态。
  //组件的状态是一个属性。属性的值是一个对象。
  //对象也有一个属性，属性的值也是一个对象。
  //所以这里是this.state这是属性的值。
  //this.state.date这个是属性的值对象的值。
  //通过this.state.date才能够调用到new Date()。
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  //一个组件类是必须要实现一个render()方法的。
  //这个render()方法是要返回一个JSX元素的。
  //这里返回**一个**元素，不是多个元素。
  //返回一个块元素，可以包含多个子元素。
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

//上面定义了一个组件类Clock
//类就是模板。
//我们的目的是把组件类插入到HTML DOM的节点当中。
//所以，要用ReactDOM.render()方法。 
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
```

这段代码的执行顺序，是这样的：

1. 当  被传递给 ReactDOM.render() 时，React 调用 Clock 组件的构造函数。 由于 Clock 需要显示当前时间，所以使用包含当前时间的对象来初始化 this.state 。 我们稍后会更新此状态。

2. React 然后调用 Clock 组件的 render() 方法。这是 React 了解屏幕上应该显示什么内容，然后 React 更新 DOM 以匹配 Clock 的渲染输出。

3. 当 Clock 的输出插入到 DOM 中时，React 调用 componentDidMount() 生命周期钩子。 在其中，Clock 组件要求浏览器设置一个定时器，每秒钟调用一次 tick()。

4. 浏览器每秒钟调用 tick() 方法。 在其中，Clock 组件通过调用 setState() 来调度UI更新。 通过调用 setState() ，React 知道状态已经改变，并再次调用 render() 方法来确定屏幕上应当显示什么。 这一次，render() 方法中的 this.state.date 将不同，所以渲染输出将包含更新的时间，并相应地更新 DOM。

5. 一旦 Clock 组件被从 DOM 中移除，React 会调用 componentWillUnmount() 这个钩子函数，定时器也就会被清除。

[React学习记录-3-箭头函数、定时器、动态对象、代码执行逻辑 - 逻辑协会 - 博客园](https://www.cnblogs.com/gnuzsx/p/11924960.html)