---
title: Font End Interview Questions
date: 2020-08-04 23:55:37
tags:
---
## Explain event delegation?
Event delegation is a technique involving adding event listeners to a parent element instead of adding them to the descendant elements. The listener will fire whenever the event is triggered on the descendant elements due to event bubbling up the DOM. The benefits of this technique are:

- Memory footprint goes down because only one single handler is needed on the parent element, rather than having to attach event handlers on each descendant.
- There is no need to unbind the handler from elements that are removed and to bind the event for new elements.
## Explain how this works in JavaScript#
There's no simple explanation for `this`; it is one of the most confusing concepts in JavaScript. A hand-wavey explanation is that the value of `this` depends on how the function is called. I have read many explanations on `this` online, and I found Arnav Aggrawal's explanation to be the clearest. The following rules are applied:

1. If the `new` keyword is used when calling the function, `this` inside the function is a brand new object.
2. If `apply`, `call`, or `bind` are used to call/create a function, `this` inside the function is the object that is passed in as the argument.
3. If a function is called as a method, such as `obj.method()` — `this` is the object that the function is a property of.
4. If a function is invoked as a free function invocation, meaning it was invoked without any of the conditions present above, `this` is the global object. In a browser, it is the `window` object. If in strict mode ('`use strict`'), `this` will be undefined instead of the global object.
5. If multiple of the above rules apply, the rule that is higher wins and will set the `this` value.
6. If the function is an ES2015 arrow function, it ignores all the rules above and receives the `this` value of its surrounding scope at the time it is created.
For an in-depth explanation, do check out his article on Medium.

Can you give an example of one of the ways that working with this has changed in ES6?#
ES6 allows you to use arrow functions which uses the enclosing lexical scope. This is usually convenient, but does prevent the caller from controlling context via .call or .apply—the consequences being that a library such as jQuery will not properly bind this in your event handler functions. Thus, it's important to keep this in mind when refactoring large legacy applications.
## Explain how prototypal inheritance works#
This is an extremely common JavaScript interview question. All JavaScript objects have a `__proto__` property, that is a reference to another object, which is called the object's "prototype". When a property is accessed on an object and if the property is not found on that object, the JavaScript engine looks at the object's `__proto__`, and the `__proto__'s` `__proto__` and so on, until it finds the property defined on one of the __proto__s or until it reaches the end of the prototype chain. This behavior simulates classical inheritance, but it is really more of delegation than inheritance.

Example of Prototypal Inheritance#
We already have a build-in `Object.create`, but if you were to provide a polyfill for it, that might look like:
```javascript
if (typeof Object.create !== 'function') {
  Object.create = function (parent) {
    function Tmp() {}
    Tmp.prototype = parent;
    return new Tmp();
  };
}

const Parent = function () {
  this.name = 'Parent';
};

Parent.prototype.greet = function () {
  console.log('hello from Parent');
};

const child = Object.create(Parent.prototype);

child.cry = function () {
  console.log('waaaaaahhhh!');
};

child.cry();
// Outputs: waaaaaahhhh!

child.greet();
// Outputs: hello from Parent
```
Things to note are:

- .greet is not defined on the child, so the engine goes up the prototype chain and finds .greet off the inherited from Parent.
- We need to call Object.create in one of following ways for the prototype methods to be inherited:
 - Object.create(Parent.prototype);
 - Object.create(new Parent(null));
 - Object.create(objLiteral);
 - Currently, child.constructor is pointing to the Parent:
 ```javascript
 child.constructor
ƒ () {
  this.name = "Parent";
}
child.constructor.name
"Parent"
```
- If we'd like to correct this, one option would be to do:
```javascript
function Child() {
  Parent.call(this);
  this.name = 'child';
}

Child.prototype = Parent.prototype;
Child.prototype.constructor = Child;

const c = new Child();

c.cry();
// Outputs: waaaaaahhhh!

c.greet();
// Outputs: hello from Parent

c.constructor.name;
// Outputs: "Child"
```

## What do you think of AMD vs CommonJS?#
Both are ways to implement a module system, which was not natively present in JavaScript until ES2015 came along. CommonJS is synchronous while AMD (Asynchronous Module Definition) is obviously asynchronous. CommonJS is designed with server-side development in mind while AMD, with its support for asynchronous loading of modules, is more intended for browsers.

I find AMD syntax to be quite verbose and CommonJS is closer to the style you would write import statements in other languages. Most of the time, I find AMD unnecessary, because if you served all your JavaScript into one concatenated bundle file, you wouldn't benefit from the async loading properties. Also, CommonJS syntax is closer to Node style of writing modules and there is less context-switching overhead when switching between client side and server side JavaScript development.

I'm glad that with ES2015 modules, that has support for both synchronous and asynchronous loading, we can finally just stick to one approach. Although it hasn't been fully rolled out in browsers and in Node, we can always use transpilers to convert our code.