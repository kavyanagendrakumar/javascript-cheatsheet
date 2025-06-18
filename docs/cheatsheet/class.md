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
  age = '35' // Class field - set on individual objects, not User.prototype
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
1. Creates a function named User, that becomes the result of the class declaration. The function code is taken from the constructor method (assumed empty if we don’t write such method).
2. Stores class methods, getters, setters such as sayHi, in User.prototype.

| Field Type        | Location            | Shared? | Created When?      | On Prototype? |
| ----------------- | ------------------- | ------- | ------------------ | ------------- |
| Class Field       | Outside constructor | ❌ No    | Before constructor | ❌ No          |
| Constructor Field | Inside constructor  | ❌ No    | During constructor | ❌ No          |

   
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
**Making bound methods with class fields**
If an object method is passed around and called in another context, this won’t be a reference to its object any more
There are two approaches to fixing it, as discussed in the chapter Function binding:
1. Pass a wrapper-function, such as setTimeout(() => button.click(), 1000).
2. Bind the method to object, e.g. in the constructor.
3.** Using arrow function. The class field click = () => {...} is created on a per-object basis. with 'this' inside it referencing that object.**

```javascript
  class Button {
    constructor(value) {
      this.value = value;
    }
    click = () => {
      alert(this.value);
    }
  }
  let button = new Button("hello");
  setTimeout(button.click, 1000); // hello //'this' inside click refers to the Button instance
```

## Class Inheritance
Class inheritance is a way for one class to extend another class. Internally, extends keyword works using the good old prototype mechanics. 

1. It sets Rabbit.prototype. [[Prototype]] to Animal.prototype. So, if a method is not found in Rabbit.prototype, JavaScript takes it from Animal.prototype.
2. Class fields are created per instance

```javascript
  class Rabbit extends Animal {
    // if a class extends another class and has no constructor, then the following “empty” constructor is generated.
    constructor(...args) {
      super(...args);
    }
  // Constructors in inheriting classes must call super(...), and (!) do it before using this.
    constructor(name, earLength) {
      super(name);  // call parent constructor
      this.speed = 0;
      this.earLength = earLength;
    }
    hide() {
      alert(`${this.name} hides!`);
    }
    stop() {
      super.stop(); // call parent stop
      this.hide(); // and then hide
    }
  }
let rabbit = new Rabbit("White Rabbit");
```
**Overriding a method**
Usually, however, we don’t want to totally replace a parent method, but rather to build on top of it to tweak or extend its functionality. We do something in our method, but call the parent method before/after it or in the process. Classes provide "super" keyword for that.
1. super.method(...) to call a parent method. Arrow functions have no super. As was mentioned in the chapter Arrow functions revisited, arrow functions do not have super. If accessed, it’s taken from the outer function. 
2. super(...) to call a parent constructor (inside our constructor only).

**Overriding constructor**
According to the specification, if a class extends another class and has no constructor, then the following “empty” constructor is generated.
In JavaScript, there’s a distinction between a constructor function of an inheriting class (so-called “derived constructor”) and other functions. A derived constructor has a special internal property [[**ConstructorKind**]]:"derived". That’s a special internal label.
That label affects its behavior with new.
1. When a regular function is executed with new, it creates an empty object and assigns it to this.
2. But when a derived constructor runs, it doesn’t do this. It expects the parent constructor to do this job.
So a derived constructor must call super in order to execute its parent (base) constructor, otherwise the object for this won’t be created. And we’ll get an error.

**Overriding class fields** - read again https://javascript.info/class-inheritance 

## Static properties and methods
Static properties are used when we’d like to store class-level data, also not bound to an instance. In a class declaration, they are prepended by static keyword, like this.  That actually does the same as assigning it as a property directly to the class. The value of this in User.staticMethod() call is the class constructor User itself (the “object before dot” rule). Usually, static methods are used to implement functions that belong to the class as a whole, but not to any particular object of it.

Static methods are also used in database-related classes to search/save/remove entries from the database, like this. Static methods aren’t available for individual objects
```javascript
  class Article {
    static staticMethod() {
      alert(this === Article);
    }
    static compare(articleA, articleB) {
      return articleA.date - articleB.date;
    }
  }
  Article.staticMethod(); // true
  // usage
  let articles = [
    new Article("HTML", new Date(2019, 1, 1)),
    new Article("CSS", new Date(2019, 0, 1)),
    new Article("JavaScript", new Date(2019, 11, 1))
  ];
articles.sort(Article.compare);
  // static method to remove the article by id:
  Article.remove({id: 12345});
```

**Static properties**
That is the same as a direct assignment to Article:
```javascript
  class Article {
    static publisher = "Ilya Kantor";
  }
  alert( Article.publisher ); // Ilya Kantor
```

**Inheritance of static properties and methods**
Static properties and methods are inherited.
For instance, Animal.compare and Animal.planet in the code below are inherited and accessible as Rabbit.compare and Rabbit.planet:
So, Rabbit extends Animal creates two [[Prototype]] references:
1. Rabbit function prototypally inherits from Animal function.
2. Rabbit.prototype prototypally inherits from Animal.prototype.
As a result, inheritance works both for regular and static methods. Check https://javascript.info/static-properties-methods for diagram
```javascript
  class Animal {}
  class Rabbit extends Animal {}
  // for statics
  alert(Rabbit.__proto__ === Animal); // true
  // for regular methods
  alert(Rabbit.prototype.__proto__ === Animal.prototype); // true
```
For class B extends A the prototype of the class B itself points to A: B.[[Prototype]] = A. So if a field is not found in B, the search continues in A.

## Encapsulation - Private and protected properties and methods
One of the most important principles of object oriented programming – delimiting internal interface from the external one.
In object-oriented programming, properties and methods are split into two groups:
1. Internal interface – methods and properties, accessible from other methods of the class, but not from the outside.
2. External interface – methods and properties, accessible also from outside the class.

In JavaScript, there are two types of object fields (properties and methods):
1.Public: accessible from anywhere. They comprise the external interface. Until now we were only using public properties and methods.
2.Private: accessible only from inside the class. These are for the internal interface.

Javascript does not have protected fields so they are emulated.. “protected” fields: accessible only from inside the class and those extending it (like private, but plus access from inheriting classes)
**Protected** properties are usually prefixed with an underscore _. If we inherit class MegaMachine extends CoffeeMachine, then nothing prevents us from accessing this._waterAmount or this._power from the methods of the new class. **So protected fields are naturally inheritable. **
```javascript 
  class CoffeeMachine {
  _waterAmount = 0; //Protected
    set waterAmount(value) {
      if (value < 0) {
      value = 0;
    }
    this._waterAmount = value;
    }
    get waterAmount() {
      return this._waterAmount;
    }
    constructor(power) {
      this._power = power; //Protected and Readonly because there is no setter
    }
    get power() {
      return this._power;
    }
  }
  // create the coffee machine
  let coffeeMachine = new CoffeeMachine(100);
  // add water
  coffeeMachine.waterAmount = -10; // _waterAmount will become 0, not -10
  coffeeMachine.power = 25; // Error (no setter)
```
**Read-only “power”**
For power property, let’s make it read-only. It sometimes happens that a property must be set at creation time only, and then never modified.

**Private** “#waterLimit”
This is a recent addition to the language. Not supported in JavaScript engines, or supported partially yet, requires polyfilling. 
1. Privates should start with #.
2. They are only accessible from inside the class. We can’t access it from outside or from inheriting classes.
3. Private fields do not conflict with public ones. We can have both private #waterAmount and public waterAmount fields at the same time.
4. Unlike protected ones, private fields are enforced by the language itself.
5. With private fields: this['#waterLimit'] doesn’t work. That’s a syntax limitation to ensure privacy.
```javascript
  class CoffeeMachine {
  #waterLimit = 200;
  #fixWaterAmount(value) {
    if (value < 0) return 0;
    if (value > this.#waterLimit) return this.#waterLimit;
  }
  setWaterAmount(value) {
    this.#waterLimit = this.#fixWaterAmount(value);
  }
  }
  let coffeeMachine = new CoffeeMachine();
  // can't access privates from outside of the class
  coffeeMachine.#fixWaterAmount(123); // Error
  coffeeMachine.#waterLimit = 1000; // Error
```
To hide an internal interface we use either protected or private properties:
1.  Protected fields start with _. That’s a well-known convention, not enforced at the language level. Programmers should only access a field starting with _ from its class and classes inheriting from it.
2. Private fields start with #. JavaScript makes sure we can only access those from inside the class.

## Extending built-in classes
Built-in classes like Array, Map and others are extendable also.
```javascript
  // add one more method to it (can do more)
  class PowerArray extends Array {
    isEmpty() {
      return this.length === 0;
    }
  }
  let arr = new PowerArray(1, 2, 5, 10, 50);
  alert(arr.isEmpty()); // false
  let filteredArr = arr.filter(item => item >= 10);
  alert(filteredArr); // 10, 50
  alert(filteredArr.isEmpty()); // false

  arr.constructor === PowerArray // Check below for how proptotype chain works
```
Built-in methods like filter, map and others – return new objects of exactly the inherited type PowerArray. Their internal implementation uses the object’s constructor property for that. When arr.filter() is called, it internally creates the new array of results using exactly arr.constructor, not basic Array. 
When you access arr.constructor, JavaScript does the following:

1.Look for constructor directly on arr

2. arr.hasOwnProperty('constructor') → false
3. 
4. Not found? Then go to arr.__proto__
5. 
6. This is PowerArray.prototype
7. 
8. Check PowerArray.prototype.constructor
9. 
Found! It points to PowerArray

We can add a special static getter **Symbol.species** to the class. If it exists, it should return the constructor that JavaScript will use internally to create new entities in map, filter and so on. If we’d like built-in methods like map or filter to return regular arrays, we can return Array in Symbol.species. Other collections, such as Map and Set, work alike. They also use Symbol.species.
```javascript
  class PowerArray extends Array {
    isEmpty() {
      return this.length === 0;
    }
    // built-in methods will use this as the constructor
    static get [Symbol.species]() {
      return Array;
    }
  }
  let arr = new PowerArray(1, 2, 5, 10, 50);
  alert(arr.isEmpty()); // false
  // filter creates new array using arr.constructor[Symbol.species] as constructor
  let filteredArr = arr.filter(item => item >= 10);
  // filteredArr is not PowerArray, but Array
  alert(filteredArr.isEmpty()); // Error: filteredArr.isEmpty is not a function
```
**No static inheritance in built-ins**
Built-in objects have their own static methods, for instance Object.keys, Array.isArray etc. But built-in classes are an exception. **They don’t inherit statics from each other.**
For example, both Array and Date inherit from Object, so their instances have methods from Object.prototype. But Array.[[Prototype]] does not reference Object, so there’s no, for instance, Array.keys() (or Date.keys()) static method. there’s no link between Date and Object. They are independent, only Date.prototype inherits from Object.prototype. That’s an important difference of inheritance between built-in objects compared to what we get with extends.

## Class checking: "instanceof"
The instanceof operator allows to check whether an object belongs to a certain class. It also takes inheritance into account. Such a check may be necessary in many cases. For example, it can be used for building a **polymorphic function**, the one that treats arguments differently depending on their type.

