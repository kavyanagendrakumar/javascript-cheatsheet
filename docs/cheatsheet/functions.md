## Function
In JavaScript, functions are objects. A good way to imagine functions is as callable “action objects”. We can not only call them, but also treat them as objects: add/remove properties, pass by reference etc.

1. The “name” property - a function’s name is accessible as the “name” property. Object methods have names too:
2. The “length” property - There is another built-in property “length” that returns the number of function parameters
3. Custom properties - We can also add properties of our own. A property is not a variable and vice versa. A property assigned to a function like sayHi.counter = 0 does not define a local variable counter inside it. Variables are not function properties and vice versa. The count is now stored in the function directly, not in its outer Lexical Environment. Is it better or worse than using a closure? The main difference is that if the value of count lives in an outer variable, then external code is unable to access it. Only nested functions may modify it. And if it’s bound to a function, then such a thing is possible.

Many well-known JavaScript libraries make great use of this feature. They create a “main” function and attach many other “helper” functions to it. For instance, the jQuery library creates a function named $. The lodash library creates a function _ , and then adds _.clone, _.keyBy and other properties to it. They do it to lessen their pollution of the global space, so that a single library gives only one global variable. That reduces the possibility of naming conflicts. So, a function can do a useful job by itself and also carry a bunch of other functionality in properties.

```javascript
//Name
  let sayHi = function() {
    alert("Hi");
  };
  alert(sayHi.name); // sayHi (there's a name!)

let user = {
  sayHi() {
  // ...
  }
}
alert(user.sayHi.name); // sayHi

//Length
function many(a, b, ...more) {}
alert(many.length); // 2. Here we can see that rest parameters are not counted

//Property
function makeCounter() {
  // instead of:
  // let count = 0
  function counter() {
    return counter.count++;
  };
  counter.count = 0;
  return counter;
}
let counter = makeCounter();
alert( counter() ); // 0
alert( counter() ); // 1
```


## Function Declaration

A function declaration in JavaScript is a way to define a function. It's also known as a function statement. The function keyword is used, followed by the name of the function, a list of parameters in parentheses, and the function body enclosed in curly braces.

```javascript
function greet() {
  console.log("Hello, world!");
}
```

`greet` is a function that prints "Hello, world!" to the console. You can call this function using its name followed by parentheses:

```javascript
greet(); // Calls the function and prints "Hello, world!" to the console
```

One of the key characteristics of function declarations is that they are hoisted, which means you can call the function before it's declared in your code:

```javascript
greet(); // This will work

function greet() {
  console.log("Hello, world!");
}
```

In this case, even though the function call appears before the function declaration in the code, it still works because function declarations are hoisted to the top of their containing scope.

## Function Parameters

In JavaScript, function parameters are the names listed in the function definition. They are used to pass values (arguments) into functions.

```javascript
function add(a, b) {
  return a + b;
}
```

`a` and `b` are the parameters of the `add` function. When you call the function, you provide values for `a` and `b`:

```javascript
let sum = add(1, 2); // 1 is the argument for 'a', and 2 is the argument for 'b'
```

1 and 2 are the arguments that are passed into the function. The function adds these values together and returns the result.

You can have as many parameters as you want, separated by commas. If you call a function with more arguments than there are parameters, the extra arguments are ignored. If you call a function with fewer arguments than there are parameters, the missing arguments are set to `undefined`.

## Function Return

In JavaScript, the `return` statement ends function execution and specifies a value to be returned to the function caller.

```javascript
function add(a, b) {
  return a + b;
}

let sum = add(1, 2); // sum is now 3
```

`add` is a function that takes two parameters, `a` and `b`, and returns their sum. The `return` statement specifies that the sum of `a` and `b` should be returned to the function caller. When you call this function with arguments 1 and 2, the return value is 3, which is then assigned to the variable `sum`.

<base-disclaimer>
  <base-disclaimer-title>
    Functions without a return statement
  </base-disclaimer-title>
  <base-disclaimer-content>
  If a function doesn't have a `return` statement, it returns `undefined` by default. If the `return` statement is used without a value, the function also returns `undefined`.
  </base-disclaimer-content>
</base-disclaimer>

## Function Expressions

A function expression in JavaScript is a way to define a function as an expression, rather than as a statement. It can be anonymous, or it can have a name. The function is defined and assigned to a variable, and it can be used later by referencing that variable.

```javascript
let greet = function() {
  console.log("Hello, world!");
}

greet(); // Calls the function and prints "Hello, world!" to the console
```

The function is assigned to the variable `greet`. This is a function expression. The function can be called later by referencing the variable `greet`.

Function expressions are not hoisted, unlike function declarations. This means that you can't use the function before it's defined:

```javascript
greet(); // This will throw an error

let greet = function() {
  console.log("Hello, world!");
}
```

In this case, calling `greet` before it's defined results in an error, because function expressions are not hoisted to the top of their containing scope.

## Named Function Expression 
Named Function Expression, or NFE, is a term for Function Expressions that have a name. For instance, let’s take an ordinary Function Expression: And add a name to it. Adding the name "func" after function did not make it a
Function Declaration, because it is still created as a part of an assignment expression. What’s the purpose of that additional "func" name? - There are two special things about the name func, that are the reasons for it:
1. It allows the function to reference itself internally.
2. It is not visible outside of the function.

Why do we use func? Maybe just use sayHi for the nested call? - The problem with that code is that sayHi may change in the outer code. If the function gets assigned to another variable instead, the code will start to give errors:
```javascript
  let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
    } else {
    sayHi("Guest"); // Error: sayHi is not a function. So use func to re-call itself
    }
  };
  sayHi(); // Hello, Guest
  // But this won't work:
  func(); // Error, func is not defined (not visible outside of the function)
```

## new Function 
new Function allows to turn any string into a function. For example, we can receive a new function from a server and then execute it. It is used in very specific cases, like when we receive code from a server, or to dynamically compile a function from a template, in complex web-applications. Functions created with new Function, have [[Environment]] referencing the global Lexical Environment, not the outer one. So, such function doesn’t have access to outer variables, only to the global ones. If new Function had access to outer variables, it would have problems with minifiers because minifiers change names to shorter alphabets for optimization. 
```javascript
  let func = new Function ([arg1, arg2, ...argN], functionBody);

  new Function('a', 'b', 'return a + b'); // basic syntax
```

## Anonymous Functions

An anonymous function in JavaScript is a function that is not given a name. Instead, it is usually used where a function is expected as an argument, such as in a callback function or an event handler.

```javascript
let greet = function() {
  console.log("Hello, world!");
}

greet(); // Calls the function and prints "Hello, world!" to the console
```

In this example, the function is assigned to the variable `greet`, but the function itself does not have a name. This is an example of a function expression, which creates a function and assigns it to a variable.

Anonymous functions can also be used as arguments to other functions:

```javascript
setTimeout(function() {
  console.log("This message is delayed by 1 second.");
}, 1000);
```

Here, the anonymous function is passed as an argument to `setTimeout`. The function will be called after 1 second (1000 milliseconds).


## Arrow Functions

Arrow functions in JavaScript provide a concise syntax to write function expressions. They are anonymous and change the way `this` binds in functions.

```javascript
let greet = () => {
  console.log("Hello, world!");
}

greet(); // Calls the function and prints "Hello, world!" to the console
```

The function is assigned to the variable `greet`. This is an arrow function, indicated by the `() =>` syntax.

Arrow functions can also take parameters:

```javascript
let add = (a, b) => a + b;

let sum = add(1, 2); // sum is now 3
```

In this case, `add` is an arrow function that takes two parameters, `a` and `b`, and returns their sum. The function body is on the same line as the arrow, indicating that the result of the expression `a + b` is automatically returned.

If there's only one parameter, you can omit the parentheses:

```javascript
let square = x => x * x;

let result = square(5); // result is now 25
```

`square` is an arrow function that takes one parameter, `x`, and returns its square.

1. Arrow functions come in handy where we usually don’t want to leave the current context.
2. Not having this naturally means another limitation: arrow functions can’t be used as constructors. They can’t be called with new.
3. Arrow functions VS bind - The arrow => doesn’t create any binding. The function simply doesn’t have this. The lookup of this is made exactly the same way as a regular variable search: in the outer lexical environment.
4. Arrow functions also have no arguments variable. That’s great for decorators, when we need to forward a call with the current this and arguments.

    ```javascript
    // Regular function
    let obj1 = {
      value: 'a',
      createAnonFunction: function() {
        return function() {
          console.log(this.value);
        };
      }
    };

    obj1.createAnonFunction()(); // undefined

    // Arrow function
    let obj2 = {
      value: 'a',
      createArrowFunction: function() {
        return () => {
          console.log(this.value);
        };
      }
    };

    obj2.createArrowFunction()(); // 'a'


    //Decorator
      function defer(f, ms) {
        return function() {
        setTimeout(() => f.apply(this, arguments), ms);
        };
      }
      function sayHi(who) {
        alert('Hello, ' + who);
      }
      let sayHiDeferred = defer(sayHi, 2000);
      sayHiDeferred("John"); // Hello, John after 2 seconds

      // The same without an arrow function would look like:
      function defer(f, ms) {
        return function(...args) {
          let ctx = this;
          setTimeout(function() {
            return f.apply(ctx, args);
          }, ms);
        };
      }
    ```

## Arrow Functions vs Regular Functions

Arrow functions and regular functions in JavaScript are similar in many ways, but there are some key differences:

1. **Syntax**: Arrow functions have a shorter syntax compared to function expressions. Here's a comparison:

    ```javascript
    // Regular function
    let add = function(a, b) {
      return a + b;
    }

    // Arrow function
    let add = (a, b) => a + b;
    ```

2. **`this` keyword**: In regular functions, the `this` keyword represents the object that called the function. In arrow functions, `this` is lexically bound. It means that it uses `this` from the code that contains the arrow function.

5. **Arguments object**: Regular functions have an "arguments" object which contains all the arguments passed to the function. It is an array-like iterable object not an array. Arrow functions do not have an "arguments" object. If you need to access arguments with an arrow function, you can use rest parameters instead.

6. **Constructors and prototypes**: Regular functions, when used with the `new` keyword, can act as constructors. Arrow functions, however, do not have a `prototype` property and cannot act as constructors, so they can't be used with `new`.

7. **Method definitions**: If you're defining a method in an object literal, a method definition or a regular function is often preferable, because it's shorter than an arrow function and it keeps the correct `this` context.

## Decorators and forwarding, call/apply. 
Forward calls between functions and decorate them.

Transparent caching - If the function is called often, we may want to cache (remember) the results to avoid spending extra-time on recalculations. If the function is called often, we may want to cache (remember) the results to avoid spending extra-time on recalculations. In the code below **cachingDecorator** is a decorator: a special function that takes another function and alters its behavior.
```javascript
  function slow(x) {
    // there can be a heavy CPU-intensive job here
    alert(`Called with ${x}`);
    return x;
  }
  function cachingDecorator(func) {
    let cache = new Map();
    return function(x) {
      if (cache.has(x)) { // if there's such key in cache
        return cache.get(x); // read the result from it
      }
      let result = func(x); // otherwise call func
      cache.set(x, result); // and cache (remember) the result
      return result;
      };
  }
  slow = cachingDecorator(slow);
  alert( slow(1) ); // slow(1) is cached and the result returned
  alert( "Again: " + slow(1) ); // slow(1) result returned from cache
```

## Using “func.call/apply” for the context - Call forwarding 
The caching decorator mentioned above is not suited to work with object methods. Once a method is passed somewhere separately from the object – this is lost.
Passing all arguments along with the context to another function is called call forwarding.
```javascript
  // we'll make worker.slow caching
  let worker = {
    someMethod() {
      return 1;
  },
  slow(x) {
    // scary CPU-heavy task here
    alert("Called with " + x);
    return x * this.someMethod(); // (*)
  }
  };
  // same code as before
  function cachingDecorator(func) {
    let cache = new Map();
    return function(x) {
      if (cache.has(x)) {
        return cache.get(x);
      }
      let result = func(x); // (**)
      cache.set(x, result);
      return result;
      };
    }
    alert( worker.slow(1) ); // the original method works
    worker.slow = cachingDecorator(worker.slow); // now make it caching
    alert( worker.slow(2) ); // Whoops! Error: Cannot read property 'someMethod' of undefined
```
The reason is that the wrapper calls the original function as func(x) in the line (**). And, when called like that, the function gets this = undefined. We would observe a similar symptom if we tried to run:
```javascript
  let func = worker.slow;
    func(2);
```
So, the wrapper passes the call to the original method, but without the context this. Hence the error.
To fix this, There’s a special built-in function method func.call(context, …args) that allows to call a function explicitly setting this.
As an example, in the code below we call sayHi in the context of different objects: sayHi.call(user) runs sayHi providing this=user, and the next line sets this=admin:
```javascript
  func.call(context, arg1, arg2, ...) // It runs func providing the first argument as this, and the next as the arguments.
  function sayHi() {
    alert(this.name);
  }
  let user = { name: "John" };
  let admin = { name: "Admin" };
  // use call to pass different objects as "this"
  sayHi.call( user ); // John
  sayHi.call( admin ); // Admin
```
In our case, we can use call in the wrapper to pass the context to the original function:
```javascript
  let worker = {
  someMethod() {
    return 1;
  },
  slow(x) {
    alert("Called with " + x);
    return x * this.someMethod(); // (*)
  }
  };
  function cachingDecorator(func) {
    let cache = new Map();
    return function(x) {
      if (cache.has(x)) {
        return cache.get(x);
      }
      let result = func.call(this, x); // "this" is passed correctly now
      cache.set(x, result);
      return result;
    };
  }
  worker.slow = cachingDecorator(worker.slow); // now make it caching
  alert( worker.slow(2) ); // works
  alert( worker.slow(2) ); // works, doesn't call the original (cached)
```

## func.apply
The only syntax difference between call and apply is that call expects a list of arguments, while apply takes an array-like object with them. And for objects that are both iterable and array-like, such as a real array, we can use any of them, but apply will probably be faster, because most JavaScript engines internally optimize it better.
There’s only a subtle difference regarding args:
1. The spread syntax ... allows to pass iterable args as the list to call.
2. The apply accepts only array-like args.

## Method Borrowing
```javascript
  function hash() {
    alert( arguments.join() ); // Error: arguments.join is not a function because arguments is array-like not array
  }
  hash(1, 2);

  function hash() {
    alert( [].join.call(arguments) ); // 1,2
  }
  hash(1, 2);
```
We take (borrow) a join method from a regular array ( [].join) and use [].join.call to run it in the context of arguments. Why does it work? That’s because the internal algorithm of the native method arr.join(glue) is very simple. technically it takes this and joins this[0], this[1] …etc together. It’s intentionally written in a way that allows any array-like this (not a coincidence, many methods follow this practice). That’s why it also works with this=arguments.

**Notes**: It is generally safe to replace a function or a method with a decorated one, except for one little thing. If the original function had properties on it, like func.calledCount or whatever, then the decorated one will not provide them. Because that is a wrapper. So one needs to be careful if one uses them. E.g. in the example above if slow function had any properties on it, then cachingDecorator(slow) is a wrapper without them.
Some decorators may provide their own properties. E.g. a decorator may count how many times a function was invoked and how much time it took, and expose this information via wrapper properties. There exists a way to create decorators that keep access to function properties, but this requires using a special Proxy object to wrap a function. We’ll discuss it later in the article Proxy and Reflect.

Decorator is a wrapper around a function that alters its behavior. The main job is still carried out by the function. Decorators can be seen as “features” or “aspects” that can be added to a function. We can add one or add many. And all this without changing its code!
We also saw an example of method borrowing when we take a method from an object and call it in the context of another object. It is quite common to take array methods and apply them to arguments. The alternative is to use rest parameters object that is a real array.

The method setTimeout in-browser is a little special: it sets this=window for the function call

## Bind
Functions provide a built-in method bind that allows to fix this when functions and methods are forwarded. The result of func.bind(context) is a special function-like “exotic object”, that is callable as function and transparently passes the call to func setting this=context. In other words, calling boundFunc is like func with fixed this. All arguments are passed to the original func “as is”, for instance:
```javascript
  let user = {
    firstName: "John"
  };
  function func(phrase) {
    alert(phrase + ', ' + this.firstName);
  }
  // bind this to user
  let funcUser = func.bind(user);
  funcUser("Hello"); // Hello, John (argument "Hello" is passed, and this=user)

  //Now let’s try with an object method:
  let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
  };
  let sayHi = user.sayHi.bind(user); // (*)
  // can run it without an object
  sayHi(); // Hello, John!
  setTimeout(sayHi, 1000); // Hello, John!
  // even if the value of user changes within 1 second
  // sayHi uses the pre-bound value which is reference to the old user object
  user = {
    sayHi() { alert("Another user in setTimeout!"); }
  };

  //bindAll methods of user   
  for (let key in user) {
    if (typeof user[key] == 'function') {
      user[key] = user[key].bind(user);
    }
  }
```

**Partial functions**
We can bind not only this, but also arguments. That’s rarely done, but sometimes can be handy. For instance, we have a function send(from, to, text). Then, inside a user object we may want to use a partial variant of it: sendTo(to, text) that sends from the current user.

Going partial without context - What if we’d like to fix some arguments, but not the context this? For example, for an object method. The native bind does not allow that. We can’t just omit the context and jump to arguments.
Fortunately, a function partial for binding only arguments can be easily implemented.
```javascript
  function partial(func, ...argsBound) {
    return function(...args) { // (*)
      return func.call(this, ...argsBound, ...args);
    }
  }
  // Usage:
  let user = {
    firstName: "John",
    say(time, phrase) {
      alert(`[${time}] ${this.firstName}: ${phrase}!`);
    }
  };
  // add a partial method with fixed time
  user.sayNow = partial(user.say, new Date().getHours() + ':' + new Date().getMinutes());
  user.sayNow("Hello");
  // Something like:
  // [10:00] John: Hello!
```

## F.Prototype - way of setting a [[Prototype]] for objects created via a constructor function.
If F is a constructor function and F.prototype is an object, then the new operator uses it to set [[Prototype]] for the new object. F.prototype here means a regular property named "prototype" on F. The value of F.prototype should be either an object or null: other values won’t work. The "prototype" property only has such a special effect when set on a constructor function, and invoked with new. On regular objects the prototype is nothing special
```javascript
  let user = {
  name: "John",
  prototype: "Bla-bla" // no magic at all
};
```

F.prototype property is only used when new F is called, it assigns [[Prototype]] of the new object. If, after the creation, F.prototype property changes ( F.prototype = <another object>), then new objects created by new F will have another object as [[Prototype]], but already existing objects keep the old one.
```javascript
  let animal = {
    eats: true
  };
  function Rabbit(name) {
    this.name = name;
  }
  Rabbit.prototype = animal;
  // Setting Rabbit.prototype = animal literally states the following: “When a new Rabbit is created, assign its [[Prototype]] to animal”.
  let rabbit = new Rabbit("White Rabbit"); // rabbit.__proto__ == animal
  alert( rabbit.eats ); // true
```
Every function has the "prototype" property even if we don’t supply it. The default "prototype" is an object with the only property constructor that points back to the function itself.
```javascript
  function Rabbit() {}
  /* default prototype
  Rabbit.prototype = { constructor: Rabbit };
  */
  alert( Rabbit.prototype.constructor == Rabbit ); // true

  let rabbit = new Rabbit(); // inherits from {constructor: Rabbit}
  alert(rabbit.constructor == Rabbit); // true (from prototype)

  // We can use constructor property to create a new object using the same constructor as the existing one.
  // That’s handy when we have an object, don’t know which constructor was used for it (e.g. it comes from a 3rd party library)
  // , and we need to create another one of the same kind.
  let rabbit2 = new rabbit.constructor("Black Rabbit");
```
JavaScript itself does not ensure the right "constructor" value. In particular, if we replace the default prototype as a whole, then there will be no "constructor" in it. So, to keep the right "constructor" we can choose to add/remove properties to the default "prototype" instead of overwriting it as a whole:
```javascript
  function Rabbit() {}
  Rabbit.prototype = {
    jumps: true
  };
  let rabbit = new Rabbit();
  alert(rabbit.constructor === Rabbit); // false
```

## Native prototypes - adding new capabilities to built-in objects
All built-in objects such as Array, Date, Function and others also keep methods in prototypes. All of the built-in prototypes have Object.prototype on the top. Please note that there is no more [[Prototype]] in the chain above Object.prototype. 

Some methods in prototypes may overlap, for instance, Array.prototype has its own toString that lists comma-delimited elements. Object.prototype has toString as well, but Array.prototype is closer in the chain, so the array variant is used. Chrome developer console also show inheritance ( console.dir may need to be used for built-in objects). Other built-in objects also work the same way. Even functions – they are objects of a built-in Function constructor, and their methods ( call/ apply and others) are taken from Function.prototype. Functions have their own toString too.

```javascript
  let arr = [1, 2, 3];
  // it inherits from Array.prototype?
  alert( arr.__proto__ === Array.prototype ); // true
  // then from Object.prototype?
  alert( arr.__proto__.__proto__ === Object.prototype ); // true
  // and null on the top.
  alert( arr.__proto__.__proto__.__proto__ ); // null

  // Changing native prototype
  String.prototype.show = function() {
    alert(this);
  };
  "BOOM!".show(); // BOOM!
```
Changing native prototypes - Native prototypes can be modified. For instance, if we add a method to String.prototype, it becomes available to all strings. But that is generally a bad idea. Prototypes are global, so it’s easy to get a conflict. If two libraries add a method String.prototype.show, then one of them will be overwriting the method of the other. In modern programming, there is only one case where modifying native prototypes is approved. That’s polyfilling. Polyfilling is a term for making a substitute for a method that exists in the JavaScript specification, but is not yet supported by a particular JavaScript engine
```javascript
  if (!String.prototype.repeat) { // if there's no such method
  // add it to the prototype
  String.prototype.repeat = function(n) {
    // repeat the string n times
    // actually, the code should be a little bit more complex than that
    // (the full algorithm is in the specification)
    // but even an imperfect polyfill is often considered good enough
    return new Array(n + 1).join(this);
    };
  }
  alert( "La".repeat(3) ); // LaLaLa
```

**Borrowing from prototypes**
Method borrowing means take a method from one object and copy it into another. Some methods of native prototypes are often borrowed. For instance, if we’re making an array-like object, we may want to copy some Array methods to it. Another possibility is to inherit by setting obj.__proto__ to Array.prototype, so all Array methods are automatically available in obj. But that’s impossible if obj already inherits from another object. Borrowing methods is flexible, it allows to mix functionalities from different objects if needed.
```javascript
    let obj = {
      0: "Hello",
      1: "world!",
      length: 2,
  };
  obj.join = Array.prototype.join; //It works because the internal algorithm of the built-in join method only cares about the correct indexes and the length
property. It doesn’t check if the object is indeed an array. Many built-in methods are like that.
  alert( obj.join(',') ); // Hello,world!
```
All built-in objects follow the same pattern:
1. The methods are stored in the prototype ( Array.prototype, Object.prototype, Date.prototype, etc.)
2. The object itself stores only the data (array items, object properties, the date)

## Variable scope, closure 
Read this(important) - https://javascript.info/closure 
JavaScript is a very function-oriented language. 

**Closure** - Usually, a function remembers where it was born(created) in the special property [[Environment]]. It references the Lexical Environment from where it’s created. 

**Function Creation**
When a function is created, it remembers the lexical environemtn it was created in and stores in internal property called [[Environment]]

**Function Runtime**
When a function is executing, before it executes, a lexical environment is created for it's execution. 
Lexical Env has 
1. Environment record - which contains local variables, this.
2. Pointer to Outer Lexical environment which it gets when it's created([[Environment]]). 

**For loop**
For generates a new lexical environment with it's own variable. So, function generated inside for loop in every iteration refrences it's own i, from that very iteration. (Remember this for closures)

## Currying
Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).Currying doesn’t call a function. It just transforms it.
**Use cases** - To create partially applied function
1. The result of curry(func) is a wrapper function(a).
2. When it is called like curriedSum(1), the argument is saved in the Lexical Environment, and a new wrapper is returned function(b).
Then this wrapper is called with 2 as an argument, and it passes the call to the original sum.

_.curry from lodash library return a wrapper that allows a function to be called both normally and partially. The currying requires the function to have a fixed number of arguments. A function that uses rest parameters, such as f(...args), can’t be curried this way.
```javascript
  function curry(func) {
    return function curried(...args) {
      if (args.length >= func.length) {
        return func.apply(this, args);
      } else {
        return function(...args2) {
        return curried.apply(this, args.concat(args2));
        }
      }
    };
}

//Example
function log(date, importance, message) {
  alert(`[${date.getHours()}:${date.getMinutes()}] [${importance}] ${message}`);
}
// logNow will be the partial of log with fixed first argument
let logNow = log(new Date());
// use it
logNow("INFO", "message"); // [HH:mm] INFO message
```

