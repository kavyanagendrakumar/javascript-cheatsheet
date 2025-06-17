## Classes
Modern way of creating objects. Constructor functions is old way.

```javascript
  class MyClass {
  // class methods
  constructor() { ... } // The constructor() method is called automatically by new, so we can initialize the object there.
  method1() { ... }
  ...
}

class User {
  constructor(name) {
    this.name = name;
  }
  get name() { //Getters/setters - Just like literal objects, classes may include getters/setters, computed properties etc.
    return this._name;
  }
  set name(value) {
    if (value.length < 4) {
      alert("Name is too short.");
    return;
    }
    this._name = value;
  }
  sayHi() {
    alert(this.name);
  }
}
// Usage:
let user = new User("John");
user.sayHi();
```
When new User("John") is called:
1. A new object is created.
2. The constructor runs with the given argument and assigns it to this.name.

In JavaScript, a class is a kind of function. What class User {...} construct really does is:
1. Creates a function named User, that becomes the result of the class declaration. The function code is taken from the
constructor method (assumed empty if we don’t write such method).
2. Stores class methods, such as sayHi, in User.prototype.
   
```javascript
  class User {
    constructor(name) { this.name = name; }
    sayHi() { alert(this.name); }
  }
  // proof: User is a function
  alert(typeof User); // function
```

Classes differ from constructor function in following ways
1. First, a function created by class is labelled by a special internal property [[IsClassConstructor]]: true. So it’s not entirely the same as creating it manually. The language checks for that property in a variety of places. For example, unlike a regular function, it must be called with new.
2.  Class methods are non-enumerable. A class definition sets enumerable flag to false for all methods in the "prototype". That’s good, because if we for..in over an object, we usually don’t want its class methods.
3. Classes always use strict. All code inside the class construct is automatically in strict mode.

Similar to functions classes can be Class Expression or Named Class Expression or dynamically returned from function
```javascript
  let User = class {
  sayHi() {
    alert("Hello");
  }
};
// "Named Class Expression"
let User = class MyClass {
  sayHi() {
    alert(MyClass); // MyClass name is visible only inside the class
  }
};
new User().sayHi(); // works, shows MyClass definition
alert(MyClass); // error, MyClass name isn't visible outside of the class
//Dynamic class
function makeClass(phrase) {
  // declare a class and return it
  return class {
    sayHi() {
      alert(phrase);
    }
  };
}
```


