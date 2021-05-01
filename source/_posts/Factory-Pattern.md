---
title: Factory Pattern
date: 2020-08-04 23:10:22
tags:
---

## What is the factory pattern? 
The factory pattern is a creational pattern that provides a template that can be used to create objects. It is used in complex situations where the type of the object required varies and needs to be specified in each case.

It does not use the new keyword directly to instantiate objects. This means it does not explicitly require the use of a constructor to create objects. Instead, it provides a generic interface that delegates the object creation responsibility to the corresponding subclass.

### Example
As the name “factory” implies, we can use this pattern when we want to create different objects that have some similar characteristics. Let’s look at an example to understand this better.

Consider the example from the previous chapter where an ice cream factory can be used to create multiple flavors of ice cream. Let’s see how we can apply the factory pattern in this example.
```javascript
class IceCreamFactory {
  constructor() {
    this.createIcecream = function(flavor) {
      let iceCream;
      if (flavor === 'chocolate'){
          iceCream = new Chocolate();
      }  
      else if (flavor === 'mint'){
          iceCream = new Mint();
      } 
      else if (flavor === 'strawberry'){
          iceCream = new Strawberry();
      }
      return iceCream;
    };
  }
}

class Chocolate {
  constructor() {
    this.icecreamFlavor = "chocolate";
    this.message = function() {
      return `You chose the ${this.icecreamFlavor} flavor.`;
    };
  }
}

class Mint {
  constructor() {
    this.icecreamFlavor = "mint";
    this.message = function() {
      return `You chose the ${this.icecreamFlavor} flavor.`;
    };
  }
}

class Strawberry{
  constructor() {
    this.icecreamFlavor = "strawberry";
    this.message = function() {
      return `You chose the ${this.icecreamFlavor} flavor.`;
    };
  }
}

// creating objects
const iceCreamfactory = new IceCreamFactory();

const chocolate = iceCreamfactory.createIcecream('chocolate');
const mint = iceCreamfactory.createIcecream('mint');
const strawberry = iceCreamfactory.createIcecream('strawberry');

console.log(chocolate.message()); 
console.log(mint.message()); 
console.log(strawberry.message()); 
```

### Explanation 
In the example above, we created a factory called `IceCreamFactory`. Its `constructor` has a function createIcecream that accepts the parameter `flavor`. Depending on the `flavor`, it instantiates an object of the corresponding class. For example, if the `flavor` is `chocolate`, it instantiates an object of the `Chocolate` class (line 6). It does the same if the `flavor` is `mint` or `strawberry` (lines 9 and 12).

![image](factory.jpg)

## When to use the factory pattern? - 
- When the type of objects required cannot be anticipated beforehand

- When multiple objects that share similar characteristics need to be created

- When you want to generalize the object instantiation process since the object set up is complex in nature

## Q1 Explain event delegation?

Event delegation is a technique involving adding event listeners to a parent element instead of adding them to the descendant elements. The listener will fire whenever the event is triggered on the descendant elements due to event bubbling up the DOM. The benefits of this technique are:

- Memory footprint goes down because only one single handler is needed on the parent element, rather than having to attach event handlers on each descendant.
- There is no need to unbind the handler from elements that are removed and to bind the event for new elements.
