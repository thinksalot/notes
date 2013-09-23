### Closures:

Closure are functions that retain a reference to their free variables.

Closure occures when a **nested** function has access to variable of a parent function.

In javascript,the nested function has access to variable of parent function **even if** the parent function has returned.

Closures are very useful because they let us **associate** some data with a function. This is similar to **OOP** where object allow us to associate date with one or more functions.

This is because of **lexical scoping**

```js
function one(){
  var one_name='I am one';

  function two(){
    console.log(one_name);
  } 
  two();
}
one(); // I am one
```

In closure, nested function is made available **outside** the function in which it was defined.The nested function maintains access to arguments, variable of its parent as well as its own.

```js
function nest(){
  var name='I am a nest';
  return function(){
    console.log(name);
  }
}
var bird=nest();
bird(); // has access to inner private var 'name'
```

Here `nest()` is a closure function.

### Execution context 
* "Execution context" actually means scope 
* Single threaded nature of javascript allows only a single thing to be done at a time
* As javascript interpreter starts executing code, it first enters a global execution context. Each invocation of a function from this point on will result in creation of new execution context
* Name conflicts of variables within execution context is resolved by moving locally to globally ie the lookup process of variable will always start and locally and move up.


Example: Retaining reference to free variables
---

Here the `getName()` and `setName()` functions retaing their reference to the name variable even if the function has finished execution and returned an object. The `setName()` and `getName()` still see the same variable.

```
function Person(name){
  function setName(n){
    name=n;
  }

  function getName(){
    return name;
  }
  
  return {
    getName:getName,
    setName:setName
  };
}

var buddha=Person('Gautam');
console.log(buddha.getName())

buddha.setName('Siddhartha');
console.log(buddha.getName());

```
This pattern is somewhat similar to the module pattern below.

Example 
---
An example would be event based programming where a function/behavior is attach with an event.Our code is generally attached as a single function: a callback which is executed in response to the event.

```css
body {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 12px;
}

h1 {
  font-size: 1.5em;
}
h2 {
  font-size: 1.2em;
}
```
```js
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16)

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16
```

```html
<a href="#" id="size-12">12</a>
<a href="#" id="size-14">14</a>
<a href="#" id="size-16">16</a>
```

Here the closure always has access to the **intial value** of `font-size` which is `12` and changes size relative to this value.


Example: Module Pattern 
---

This pattern emulates private variables and functions in javascript.
A common environment is created using closure which is shared by all functions of the closure.
The private variable `privateCounter` and private function `changeBy()` cannot be accessed outside the anonymous function.Instead they must be accessed by the three functions returned by the anonymous object wrapper.

```js
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter();
var Counter2 = makeCounter();
alert(Counter1.value()); /* Alerts 0 */
Counter1.increment();
Counter1.increment();
alert(Counter1.value()); /* Alerts 2 */
Counter1.decrement();
alert(Counter1.value()); /* Alerts 1 */
alert(Counter2.value()); /* Alerts 0 */
```

The two counter variables maintain independent environments (execution contexts) from each other.


Example: function declaration inside loops 
---

```js
var el=document.getElementsByTagName('a');
for(i=0;i<el.length;i++){
  el[i].addEventListener('click',function(e){
    e.preventDefault();
    console.log(i);
  }); 
}
```

This will not alert index of each anchor element because the callback has access to the same environment as the loop.Therefore by the time the callback is executed, the loop will already have finished execution and alert will always show the final value of `i` which is the equal of the length of the `links` array.

Following makes use of closure to create a new environment everytime a function is executed in which `i` has corresponding value as set in each iteration of the loop. Notice the click event `e` being passed to the returning function.

```js
var el=document.getElementsByTagName('a');
for(i=0;i<el.length;i++){
  el[i].addEventListener('click',
      (function(i){
         return function(e){
           e.preventDefault()
           console.log(i);
         }
       })(i))
}
```

Another implementation of closure would be:

```js
var el=document.getElementsByTagName('a');
for(i=0;i<el.length;i++){
  (function(value){
   el[i].addEventListener('click',
     function(e){
       e.preventDefault();
       console.log(value);
     })
   })(i);

}

```

This works because during each iteration of the loop, the self-invoking function provides new environment or "execution context" for the function handler where the `value` is whatever number passed on to the self-invoking function.


Example: Using Prototype
---

Its generally a **bad idea** to associate methods with constructor because methods will need to get assigned **everytime** an object is created.
This technique can have **performance** and **memory** tradeoffs.

```js
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
  this.getName = function() {
    return this.name;
  };

  this.getMessage = function() {
    return this.message;
  };
}
```

Instead, methods should be associated with prototype to take advantage of closures.

```js
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
MyObject.prototype = {
  getName: function() {
    return this.name;
  },
  getMessage: function() {
    return this.message;
  }
}
```

or another way

```js
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
MyObject.prototype.getName = function() {
  return this.name;
};
MyObject.prototype.getMessage = function() {
  return this.message;
}
```


References:

* http://benalman.com/news/2010/11/immediately-invoked-function-expression/
 
* http://ryanmorr.com/understanding-scope-and-context-in-javascript/
 
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
