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

2. **`this` keyword**: In regular functions, the `this` keyword represents the object that called the function. In arrow functions, `this` is lexically bound. It means that it uses `this` from the code that contains the arrow function. For example:

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
    ```

3. **Arguments object**: Regular functions have an "arguments" object which contains all the arguments passed to the function. It is an array-like iterable object not arrays. Arrow functions do not have an "arguments" object. If you need to access arguments with an arrow function, you can use rest parameters instead.

4. **Constructors and prototypes**: Regular functions, when used with the `new` keyword, can act as constructors. Arrow functions, however, do not have a `prototype` property and cannot act as constructors, so they can't be used with `new`.

5. **Method definitions**: If you're defining a method in an object literal, a method definition or a regular function is often preferable, because it's shorter than an arrow function and it keeps the correct `this` context.
