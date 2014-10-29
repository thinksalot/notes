this
===

The value of `this` is determined by how a function is invoked.
`this` is mainly executed in the context of the object that is left of the `.` during function invocation.

### Global:
When `this` is used globally, this is set to the `window` object

```js
this.hello='Hello world !';
console.log(window.hello);
```

### Function:
When invoking a function with a `new` operator (constructor), a new instance of the function will be created and the value of `this` will be set to this newly created instance.

```js
function doSomething(){
  console.log(this);
}

doSomething(); // window object
new doSomething(); // doSomething

function bike(){
  this.sound='bhrumm bhrumm';
}

bike(); // inside function this referes to window
window.sound; // bhrumm bhrumm

var honda=new bike(); // using constructor, this will point to object
honda.sound; // bhrumm bhrumm

```

### Inside object function:

If a function is called as a method of another object, `this` is set to the object the method is called on.

`this` references to the object `Cow`. `this` can also be used to reference other functions in the same object.

```js
var Cow={
    init:function(){
    },
    boo:function(){
      console.log(this);
    },
    booAgain:function(){
      this.boo(); // short for Cow.boo()
    }
};
```

This behavior is unaffected by where a method is defined.

```js

var Football={
  title:'Football needs goals'
};

var goals=function(){
  alert(this.title);
};

Football.goals=goals;

Football.goals();


```

### Nested functions:

When nesting functions, the value of this is not longer referenced to the parent object.

```js
var Cow={
    init:function(){
    },
    boo:function(){
      console.log(this);
    },
    booAgain:function(){
      (function(){
        this.boo(); // TypeError: Object [object global] has no method 'boo'
        console.log(this);
      })();
    }
};
```

But the following is correct:

```js

var Cow={
    init:function(){
    },
    boo:function(){
      console.log(this);
    },
    booAgain:function(){
      var self=this;
      (function(){
        self.boo();
        console.log(self);
      })();
    }
};
```

### _call_ and _apply_ methods

A function can be bound to a particular object using `call` method.
First parameter to `call` is object to be use as this, second to last parameters are passed to the function

```js

function hello(name){
  console.log(this.say+name);
}

var greeting={
  say:'Hello '
}

hello.call(greeting,'Kitty');

```

The second param to `apply` is array containing params.

### _bind_ method

When used on a function, returns a copy of the function with `this` permanently bound to object argument regardless of how the function is invoked.

```js
function hello(){
  console.log(this.greeting);
}

var namaste=hello.bind({greeting:'Namaste'});  // new copy of hello
hello(); // undefined
namaste(); // Namaste

var hola={
  greeting:'Hola Senyor',
  hello:hello,
  namaste:namaste,
};

hola.hello(); // Hola Senyor
hola.namaste(); // Namaste

```

### Inside event handler

Inside DOM event handlers, this become the node element triggering the event.


References:

* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
