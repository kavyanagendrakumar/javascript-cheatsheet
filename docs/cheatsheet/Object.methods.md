**JavaScript Object Cheatsheet: Everything You Need to Know**
Master JavaScript objects with this comprehensive cheatsheet! This comprehensive JavaScript object cheatsheet is the perfect resource for anyone who wants to learn everything there is to know about objects in JavaScript. Covering a wide range of topics, from basic object creation to advanced object methods, this cheatsheet has everything you need to start using objects effectively in your code.

**Restrictions in Naming Properties**
JavaScript object key names must adhere to some restrictions to be valid. Key names must either be strings or valid identifier or variable names (i.e. special characters such as - are not allowed in key names that are not strings).
```javascript
// Example of invalid key names
const trainSchedule = {
  platform num: 10, // Invalid because of the space between words.
  40 - 10 + 2: 30, // Expressions cannot be keys.
  +compartment: 'C' // The use of a + sign is invalid unless it is enclosed in quotations.
}
```
**Dot Notation for Accessing Object Properties**
Properties of a JavaScript object can be accessed using the dot notation in this manner: object.propertyName. Nested properties of an object can be accessed by chaining key names in the correct order.

```javascript
const apple = { 
  color: 'Green',
  price: {
    bulk: '$3/kg',
    smallQty: '$4/kg'
  }
};
console.log(apple.color); // 'Green'
console.log(apple.price.bulk); // '$3/kg'
```

## Objects
An object is a built-in data type for storing key-value pairs. Data inside objects are unordered, and the values can be of any type.

**Accessing non-existent JavaScript properties**
When trying to access a JavaScript object property that has not been defined yet, the value of undefined will be returned by default.
```javascript
const classElection = {
  date: 'January 12'
};


console.log(classElection.place); // undefined
```
**JavaScript Objects are Mutable**
JavaScript objects are mutable, meaning their contents can be changed, even when they are declared as const. New properties can be added, and existing property values can be changed or deleted.

It is the reference to the object, bound to the variable, that cannot be changed.
```javascript
const student = {
  name: 'Sheldon',
  score: 100,
  grade: 'A',
}


console.log(student)
// { name: 'Sheldon', score: 100, grade: 'A' }


delete student.score
student.grade = 'F'
console.log(student)
// { name: 'Sheldon', grade: 'F' }


student = {}
// TypeError: Assignment to constant variable.
```
**JavaScript for...in loop**
The JavaScript for...in loop can be used to iterate over the keys of an object. In each iteration, one of the properties from the object is assigned to the variable of that loop.
```javascript
let mobile = {
  brand: 'Samsung',
  model: 'Galaxy Note 9'
};


for (let key in mobile) {
  console.log(`${key}: ${mobile[key]}`);
}
```
**Properties and values of a JavaScript object**
A JavaScript object literal is enclosed with curly braces {}. Values are mapped to keys in the object with a colon (:), and the key-value pairs are separated by commas. All the keys are unique, but values are not.

Key-value pairs of an object are also referred to as properties.
```javascript
const classOf2018 = {
  students: 38,
  year: 2018
}
```
**Delete operator**
Once an object is created in JavaScript, it is possible to remove properties from the object using the delete operator. The delete keyword deletes both the value of the property and the property itself from the object. The delete operator only works on properties, not on variables or functions.
```javascript
const person = {
  firstName: "Matilda",
  age: 27,
  hobby: "knitting",
  goal: "learning JavaScript"
};


delete person.hobby; // or delete person[hobby];


console.log(person);
/*
{
  firstName: "Matilda"
  age: 27
  goal: "learning JavaScript"
}
*/
 
```
**javascript passing objects as arguments**
When JavaScript objects are passed as arguments to functions or methods, they are passed by reference, not by value. This means that the object itself (not a copy) is accessible and mutable (can be changed) inside that function.
```javascript
const origNum = 8;
const origObj = {color: 'blue'};


const changeItUp = (num, obj) => {
  num = 7;
  obj.color = 'red';
};


changeItUp(origNum, origObj);

// Will output 8 since integers are passed by value.
console.log(origNum);


// Will output 'red' since objects are passed 
// by reference and are therefore mutable.
console.log(origObj.color);
```
**JavaScript Object Methods**
JavaScript objects may have property values that are functions. These are referred to as object methods.

Methods may be defined using anonymous arrow function expressions, or with shorthand method syntax.

Object methods are invoked with the syntax: objectName.methodName(arguments).
```javascript
const engine = {
  // method shorthand, with one argument
  start(adverb) {
    console.log(`The engine starts up ${adverb}...`);
  },  
  // anonymous arrow function expression with no arguments
  sputter: () => {
    console.log('The engine sputters...');
  },
};


engine.start('noisily');
engine.sputter();


/* Console output:
The engine starts up noisily...
The engine sputters...
*/
```
**JavaScript destructuring assignment shorthand syntax**
The JavaScript destructuring assignment is a shorthand syntax that allows object properties to be extracted into specific variable values.

It uses a pair of curly braces ({}) with property names on the left-hand side of an assignment to extract values from objects. The number of variables can be less than the total properties of an object.
```javascript
const rubiksCubeFacts = {
  possiblePermutations: '43,252,003,274,489,856,000',
  invented: '1974',
  largestCube: '17x17x17'
};
const {possiblePermutations, invented, largestCube} = rubiksCubeFacts;
console.log(possiblePermutations); // '43,252,003,274,489,856,000'
console.log(invented); // '1974'
console.log(largestCube); // '17x17x17'
```
**shorthand property name syntax for object creation**
The shorthand property name syntax in JavaScript allows creating objects without explicitly specifying the property names (ie. explicitly declaring the value after the key). In this process, an object is created where the property names of that object match variables which already exist in that context. Shorthand property names populate an object with a key matching the identifier and a value matching the identifier’s value.
```javascript
const activity = 'Surfing';
const beach = { activity };
console.log(beach); // { activity: 'Surfing' }
```
**this Keyword**
In objects - The value of this is the object “before dot”, the one used to call the method., and it can be used to access properties belonging to that object. The value of this is evaluated during the run-time, depending on the context. 

Here, using the this keyword inside the object function to refer to the cat object and access its name property.
```javascript
const cat = {
  name: 'Pipey',
  age: 8,
  whatName() {
    return this.name  
  }
};


console.log(cat.whatName()); 
// Output: Pipey

// Technically, it’s also possible to access the object without this, by referencing it via the outer variable. But such code is unreliable. If we decide to copy user to another variable, e.g. admin = user and overwrite user with something else, then it will access the wrong object.
let user = {
name: "John",
age: 30,
sayHi() {
alert( user.name ); // leads to an error
}
};
let admin = user;
user = null; // overwrite to make things obvious
```
javascript function this
Every JavaScript function or method has a this context. For a function defined inside of an object, this will refer to that object itself. For a function defined outside of an object, this will refer to the global object (window in a browser, global in Node.js) in non strict mode and undefined in strict mode.
```javascript
const restaurant = {
  numCustomers: 45,
  seatCapacity: 100,
  availableSeats() {
    // this refers to the restaurant object
    // and it's used to access its properties
    return this.seatCapacity - this.numCustomers;
  }
}
 
```
 

**JavaScript Arrow Function this Scope**
Arrow functions are special: they don’t have their “own” this. If we reference this from such a function, it’s taken from the outer “normal” function. it’s useful when we actually do not want to have a separate this, but rather to take it from the outer context.
```javascript
  let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};
user.sayHi(); // Ilya
```

Verify whether this statement is true - Thus, they are generally a poor choice for writing object methods.

Consider the example code:

loggerA is a property that uses arrow notation to define the function. Since data does not exist in the global context, accessing this.data returns undefined.

loggerB uses method syntax. Since this refers to the enclosing object, the value of the data property is accessed as expected, returning "abc".
```javascript
const myObj = {
    data: 'abc',
    loggerA: () => { console.log(this.data); },
    loggerB() { console.log(this.data); },
};


myObj.loggerA();    // undefined
myObj.loggerB();    // 'abc'
```
**getters and setters intercept property access**
There are two kinds of object properties. The first kind is data properties. The second type of property is something new. It’s an accessor property. They are essentially functions that execute on getting and setting a value, but look like regular properties to an external code. JavaScript getter and setter methods are helpful in part because they offer a way to intercept property access and assignment, and allow for additional actions to be performed before these changes go into effect.
```javascript
const myCat = {
  _name: 'Snickers',
  get name(){
    return this._name
  },
  set name(newName){
    //Verify that newName is a non-empty string before setting as name property
    if (typeof newName === 'string' && newName.length > 0){
      this._name = newName; 
    } else {
      console.log("ERROR: name must be a non-empty string"); 
    }
  },
  get fullName() {
    return `${this.name} ${this.surname}`;
  }
}
```
**Accessor descriptors**
For accessor properties, there is no value or writable, but instead there are get and set functions.
That is, an accessor descriptor may have:
1. get – a function without arguments, that works when a property is read,
2. set – a function with one argument, that is called when the property is set,
3. enumerable – same as for data properties,
4. configurable – same as for data properties.
For instance, to create an accessor fullName with defineProperty, we can pass a descriptor with get and set. If we try to supply both get and value in the same descriptor, there will be an error:
```javascript
  let user = {
    name: "John",
    surname: "Smith"
  };
  Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`
  ;
  },
  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
  });
  alert(user.fullName); // John Smith
  for(let key in user) alert(key); // name, surname
```

**javascript factory functions** Refer Constructor, operator "new" for more info. There is more info you need to now than these notes- https://javascript.info/constructor-new 
A JavaScript function that returns an object is known as a factory function/constructor function. Factory functions often accept parameters in order to customize the returned object. That’s the main purpose of constructors – to implement reusable object creation code. Technically, any function (except arrow functions, as they don’t have this) can be used as a constructor. It can be run with new, and it will execute the algorithm below. The “capital letter first” is a common agreement, to make it clear that a function is to be run with new.

Constructor functions technically are regular functions. There are two conventions though:
1. They are named with capital letter first.
2. They should be executed only with "new" operator.

When a function is executed with new, it does the following steps:
1. A new empty object is created and assigned to this.
2. The function body executes. Usually it modifies this, adds new properties to it.
3. The value of this is returned.
   
```javascript
function User(name) {
// this = {}; (implicitly)
// add properties to this
this.name = name;
this.isAdmin = false;
// return this; (implicitly)
}
//So let user = new User("Jack") gives the same result as:
let user = {
name: "Jack",
isAdmin: false
};


// create a function and immediately call it with new
let user = new function() {
this.name = "John";
this.isAdmin = false;
// ...other code for user creation
// maybe complex logic and statements
// local variables etc
};
This constructor can’t be called again, because it is not saved anywhere, just created and called. So this trick aims to
encapsulate the code that constructs the single object, without future reuse.

 Advanced stuff
The syntax from this section is rarely used, skip it unless you want to know everything.
Inside a function, we can check whether it was called with new or without it, using a special new.target property.
It is undefined for regular calls and equals the function if called with new:
That can be used inside the function to know whether it was called with new, “in constructor mode”, or without it, “in regular
mode”.
We can also make both new and regular calls to do the same, like this:
Constructor mode test: new.target
this.name = name;
this.isAdmin = false;
// return this; (implicitly)
}
 
```
**javascript getters and setters restricted**
JavaScript object properties are not private or protected. Since JavaScript objects are passed by reference, there is no way to fully prevent incorrect interactions with object properties.

One way to implement more restricted interactions with object properties is to use getter and setter methods.

Typically, the internal value is stored as a property with an identifier that matches the getter and setter method names, but begins with an underscore (_).
```javascript
const myCat = {
  _name: 'Dottie',
  get name() {
    return this._name;  
  },
  set name(newName) {
    this._name = newName;  
  }
};


// Reference invokes the getter
console.log(myCat.name);


// Assignment invokes the setter
myCat.name = 'Yankee';
 ```

**Object.assign()**
shallow copies both string and Symbol properties from one or more source objects to target object. If target already has the key, then value gets overwritten. nested objects are copied by reference. Can't do deep copy. Another way to copy objects is by iterating through all properties using for in and copying to destination object. If a property value is an object, then reference is copied
 
```javascript
// example
Object.assign({ a: 1, b: 2 }, { c: 3 }, { d: 4 }) // { a: 1, b: 2, c: 3, d: 4 }
let clone = Object.assign({}, user); // Copy user to empty object
// syntax
Object.assign(target, ...sources)
```
**structuredClone()**
The call structuredClone(object) clones the object with all nested properties. The structuredClone method can clone most data types, such as objects, arrays, primitive values.
It also supports circular references, when an object property references the object itself (directly or via a chain or references). Function properties aren’t supported.
To handle such complex cases we may need to use a combination of cloning methods, write custom code or, to not reinvent
the wheel, take an existing implementation, for instance _.cloneDeep(obj)  from the JavaScript library lodash .
 
```javascript
// example
let user = {};
// let's create a circular reference:
// user.me references the user itself
user.me = user;
let clone = structuredClone(user);
alert(clone.me === clone); // true.As you can see clone.me references the clone, not the user! So the circular reference was cloned correctly as well.

// Functional property
// error
structuredClone({
f: function() {}
});
```
**Object.defineProperties()**
defines new or modifies existing properties.

Object properties, besides a value, have three special attributes (so-called “flags”). When we create a property “the usual way”, all of them are true. But we also can change them anytime.
1. writable – if true, the value can be changed, otherwise it’s read-only.
2. enumerable – if true, then listed in loops, otherwise not listed. We can change writable: true to false for a non-configurable property, thus preventing its value modification (to add another layer of protection). Not the other way around though.
3. configurable – if true, the property can be deleted and these attributes can be modified, otherwise not. Making a property non-configurable is a one-way road. We cannot change it back with defineProperty. Please note: configurable: false prevents changes of property flags and its deletion, while allowing to change its value.

Now let’s add a custom toString to user. Normally, a built-in toString for objects is non-enumerable, it does not show up in for..in. But if we add a toString of our own, then by default it shows up in for..in
 
```javascript
// example
Object.defineProperties({ a: 1, b: 2 }, { a: {
  value: 3,
  writable: true,
}}) // { a: 3, b: 2 }
// syntax
Object.defineProperties(obj, props)

Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});

let user = {
  name: "John",
  toString() {
    return this.name;
  }
};
// By default, both our properties are listed:
for (let key in user) alert(key); // name, toString
```
**Object.defineProperty()**
defines new or modifies existing property. If the property exists, defineProperty updates its flags. Otherwise, it creates the property with the given value and flags; in that case, if a flag is not supplied, it is assumed false. Compare it with “normally created” user.name above: now all flags are falsy.
 
```javascript
// example
Object.defineProperty({ a: 1, b: 2 }, 'a', {
  value: 3,
  writable: true
}); // { a: 3, b: 2 }
// syntax
Object.defineProperty(obj, prop, descriptor)
```
**Object.entries()**
returns array of object's [key, value] pairs
 
```javascript
// example
Object.entries({ a: 1, b: 2 }) // [ ["a", 1], ["b", 2] ]
// syntax
Object.entries(obj)
```
**Object.freeze()**
freezes an object, which then can no longer be changed
 
```javascript
// example
const obj = { a: 1 }
Object.freeze(obj)
obj.prop = 2 // error in strict mode
console.log(obj.prop) // 1
// syntax
Object.freeze(obj)
```
**Object.fromEntries()**
transforms a list of key-value pairs into an object
 
```javascript
// example
Object.fromEntries([['a', 1], ['b', 2]]) // { a: 1, b: 2 }
// syntax
Object.fromEntries(iterable)
```
**Object.getOwnPropertyDescriptor()**
returns a property descriptor for an own property
 
```javascript
// example
const obj = { a: 1 }
Object.getOwnPropertyDescriptor(obj, 'a') // { value: 1, writable: true, enumerable: true, configurable: true }
// syntax
Object.getOwnPropertyDescriptor(obj, prop)
```
**Object.getOwnPropertyDescriptors()**
returns all own property descriptors including symbolic and non-enumerable ones. Together with Object.defineProperties it can be used as a “flags-aware” way of cloning an object:
 
```javascript
// example
const obj = { a: 1 }
Object.getOwnPropertyDescriptors(obj, 'a') // { a: { value: 1, writable: true, enumerable: true, configurable: true } }
// syntax
Object.getOwnPropertyDescriptor(obj, prop)
```
**Object.getOwnPropertyNames()**
returns array of all properties
 
```javascript
// example
Object.getOwnPropertyNames({ a: 1, b: 2 }) // [ "a", "b" ]
// syntax
Object.getOwnPropertyNames(obj)
```
**Object.getOwnPropertySymbols()**
returns array of all symbol properties
 
```javascript
// example
const obj = { a: 1 }
const b = Symbol('b')
obj[b] = 'someSymbol' // obj = { a: 1, Symbol(b): "symbol" }
Object.getOwnPropertySymbols(obj) // [ Symbol(b) ]
// syntax
Object.getOwnPropertySymbols(obj)
```
**Object.is()**
determines whether two values are the same value
 
```javascript
// example
const objA = { a: 1 }
const objB = { a: 1 }
Object.is(objA, objA) // true
Object.is(objA, objB) // false
Object.is('a', 'a') // true
// syntax
Object.is(value1, value2)
```

**Sealing an object globally**
Property descriptors work at the level of individual properties. There are also methods that limit access to the whole object like below

**Object.isExtensible()**
determines wether an object can have new properties added to it
 
```javascript
// example
const obj = {}
Object.isExtensible(obj) // true
Object.preventExtensions(obj)
Object.isExtensible(obj) // false
// syntax
Object.isExtensible(obj)
```
**Object.isFrozen()**
determines if an object is frozen
 
```javascript
// example
const obj = {}
Object.isFrozen(obj) // false
Object.freeze(obj)
Object.isFrozen(obj) // true
// syntax
Object.isFrozen(obj)
```
**Object.isSealed()**
determines if an object is sealed
 
```javascript
// example
const obj = {}
Object.isSealed(obj) // false
Object.seal(obj)
Object.isSealed(obj) // true
// syntax
Object.isSealed(obj)
```
**Object.keys()**
returns array of object's enumerable property names. Object.keys/values/entries ignore symbolic properties
 
```javascript
// example
Object.keys({ a: 1, b: 2 }) // [ "a", "b" ]
// syntax
Object.keys(obj)
```
**Object.preventExtensions()**
prevents new properties from being added to an object
 
```javascript
// example
const obj = { a: 1 }
Object.preventExtensions(obj)
Object.defineProperty(obj, 'b', { value: 2 }) // Error: Can't define property "b": Object is not extensible
// syntax
Object.preventExtensions(obj)
```
**Object.seal()**
prevents new properties from being added and marks all existing properties as non-configurable
 
```javascript
// example
const obj = { a: 1 }
Object.seal(obj)
obj.a = 2 // { a: 2 }
obj.b = 3 // error in strict mode
delete obj.a // error in strict mode
// syntax
Object.seal(obj)
```
**Object.values()**
returns array of object's own enumerable property values
 
```javascript
// example
Object.values({ a: 1, b: 'a'}) // [ 1, "a" ]
// syntax
Object.values(obj)
```

## Prototype
In programming, we often want to take something and extend it. Not copy/reimplement its methods, just build a new object on top of it. Prototypal inheritance is a language feature that helps in that.
**[[Prototype]]** - In JavaScript, objects have a special hidden property [[Prototype]] (as named in the specification), that is either null or references another object. That object is called “a prototype”. When we read a property from object, and it’s missing, JavaScript automatically takes it from the prototype. In programming, this is called “prototypal inheritance”.  

There are only two limitations:
1. The references can’t go in circles. JavaScript will throw an error if we try to assign __proto__ in a circle.
2. The value of __proto__ can be either an object or null. Other types are ignored.
Also it may be obvious, but still: there can be only one [[Prototype]]. An object may not inherit from two others.

The property [[Prototype]] is internal and hidden, but there are many ways to set it. 
1. One of them is to use the special name __proto__, like this. Please note that __proto__ is not the same as the internal [[Prototype]] property. It’s a getter/setter for [[Prototype]]. This way is a bit outdated
2. Object.getPrototypeOf/Object.setPrototypeOf

```javascript
  let animal = {
    eats: true,
    walk() {
    /* this method won't be used by rabbit */
    }
  };
  let rabbit = {
    jumps: true
  };
  rabbit.__proto__ = animal; // (*)

  //Or
  let rabbit = {
    jumps: true,
    __proto__: animal
  };
  // we can find both properties in rabbit now:
  alert( rabbit.eats ); // true (**)
  alert( rabbit.jumps ); // true

  // The prototype is only used for reading properties. Write/delete operations work directly with the object.
  rabbit.walk = function() {
    alert("Rabbit! Bounce-bounce!");
  };
  rabbit.walk(); // Rabbit! Bounce-bounce!
```
![Uploading Screenshot 2025-06-17 at 8.55.21 AM.png…]()

1. 'this' is not affected by prototypes at all. No matter where the method is found: in an object or its prototype. In a method call, this is always the object before the dot.
2. methods are shared, but the object state is not
3. The for..in loop iterates over inherited properties too.
4. key/value-getting methods, such as Object.keys, Object.values and so on ignore inherited properties.
5. Methods defined inside the object are stored in the object itself not in prototype. Only methods inside __proto__ are in prototype.
6. prototype-less objects, created with Object.create(null) or {__proto__: null}. These objects are used as dictionaries, to store any (possibly user-generated) keys including __proto__ as regular property name and not as get/set for [[Prototype]]

**Object.create()**
creates new object, using an existing object as the prototype. shallow-copy with all descriptors
 
```javascript
// example
Object.create({ a: 1 }) // <prototype>: Object { a: 1 }
// syntax
Object.create(proto, [propertiesObject])

let animal = {
  eats: true
};
// create a new object with animal as a prototype
let rabbit = Object.create(animal); // same as {__proto__: animal}
alert(rabbit.eats); // true
alert(Object.getPrototypeOf(rabbit) === animal); // true
Object.setPrototypeOf(rabbit, {}); // change the prototype of rabbit to {}

// Object clone - This call makes a truly exact copy of obj, including all properties: enumerable and non-enumerable, data properties and
// setters/getters – everything, and with the right [[Prototype]].
let clone = Object.create(
  Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj)
);
```

**Object.getPrototypeOf()**
returns the [[Prototype]] of obj
 
```javascript
// example
const proto = { a: 1 }
const obj = Object.create(proto)
obj.b = 2 // obj = { b: 2 }
Object.getPrototypeOf(obj) // { a: 1 }
// syntax
Object.getPrototypeOf(obj)
```

**Object.prototype.hasOwnProperty()**
returns boolean indicating whether object has the specified property. excludes inherited properties
 
```javascript
// example
const obj = { a: 1 }
obj.hasOwnProperty('a') // true
obj.hasOwnProperty('b') // false
// syntax
obj.hasOwnProperty(prop)
```
**Object.prototype.isPrototypeOf()**
checks if object exists in another object's prototype chain
 
```javascript
// example
const proto = { a: 1 }
const obj = Object.create(proto)
proto.isPrototypeOf(obj) // true
// syntax
prototypeObj.isPrototypeOf(object)
```
**Object.prototype.propertyIsEnumerable()**
checks whether the specified property is enumerable and is the object's own property
 
```javascript
// example
const obj = { a: 1 } const arr = ['a']
obj.propertyIsEnumerable('a') // true
arr.propertyIsEnumerable(0) // true
arr.propertyIsEnumerable('length') // false
// syntax
obj.propertyIsEnumerable(prop)
```
**Object.prototype.toString()**
returns a string representing the object
 
```javascript
// example
const obj = {}
obj.toString() // "[object Object]"
const arr = ['a', 'b']
arr.toString() // "a,b"
// syntax
obj.toString()
```

**Creating**
```javascript
const objectName = {};
```
**Adding**
1. Using . dot notation:
```javascript
objectName.name = "Rabah";
objectName.age = 18;
```
2. Using [] bracket notation:
 ```javascript
objectName["name"] = "Rabah";
objectName["age"] = 18;

// another way with variables
const newProp = 'location';
objectName[newProp] = 'FL'

/*
objectName = {
  name: "Rabah",
  age: 18,
  location: "FL"
}
*/
```
**Accessing**
```javascript
// dot notation
objectName.name; // "Rabah"

// bracket notation
objectName["name"]; // "Rabah"

// extra variation
const propName = "location";
objectName[propName] // "FL"
```
**Manipulating**
```javascript
objectName.age = 25;

objectName["age"] = 25 // 25
```
**Looping**
```javascript
for (let property in objectName) {
  if (property === ...) {
    // Do things here
  } else {
  // do something otherwise
  }
}
```
**Cloning keys**
```javascript
const objectKeys = [];

for (let property in objectName) {
  objectKeys.push(property);
}

console.log(objectKeys) // ["name", "age", "location"]

// alternatively
const keys = Object.keys(objectName); 
console.log(keys) // ["name", "age", "location"]
```
**Cloning values**
```javascript
const objectValues = [];

for (let property in objectName) {
  objectValues.push(objectName[property]);
}

console.log(objectValues) // ["Rabah", 25, "FL"]

// alternatively
const values = Object.values(objectName);
console.log(values) // ["Rabah", 25, "FL"]
```
**in operator**
```javascript
if ("favoriteColor" in objectName) { // if the property favoriteColor exists in objectName
  // do something if true
} else {
  // do something otherwise
}
```
**Defining methods**
```javascript
// The same way we add properties
objectName.sayBonjour = function(name) {
  console.log(`Bonjour ${name}.`);
}
```
**Using methods**
```javascript
objectName.sayBonjour("Peggy"); // "Bonjour Peggy."
```
**this keyword**
```javascript
  // Let's add a new method
  objectName.sayMyAge = function() {
    this.sayBonjour('Mathieu');
    console.log(`You're ${this.age} years old.`);
  }
Explanation:
// Now our object looks like this
objectName = {
  name: "Rabah",
  age: 25,
  location: "FL",
  sayBonjour: function(name) {
    console.log(`Bonjour ${name}.`);
  },
  sayMyAge: function() {
  
    this.sayBonjour('Mathieu');
    // Since the method 'sayBonjour' it's outside of this method scope, 
    // which is inside the objectName. so to refer to it and use it by calling it, we have to use the 'this' keyword.
    // Using the 'this.sayBonjour()' keyword is the same thing as saying:
    // objectName.sayBonjour()
     
    console.log(`You're ${this.age} years old.`);
    // The same thing happening here. We're saying '`I'm ${objectName.age} years old.'
    
  }
}  
objectName.sayMyAge();   // "Bonjour Mathieu."
                        //  "I'm 25 years old."
```

## Proxy
A Proxy object wraps another object and intercepts operations, like reading/writing properties and others, optionally handling them on its own, or transparently allowing the object to handle them.
```javascript
  
```
