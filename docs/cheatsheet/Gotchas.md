# 🤯 5 JavaScript Gotchas (Explained Simply)

---

## 1. **`this` Keyword Confusion**

In JavaScript, `this` depends on **how** a function is called, not *where* it is written.

```javascript
const obj = {
  name: 'JS',
  say() {
    console.log(this.name);
  }
};

const sayFunc = obj.say;
sayFunc(); // undefined 😱
```

**Why?**  
- `sayFunc` is **called standalone**, so `this` becomes `undefined` (in strict mode) or `window` (in sloppy mode).
- In Java/C#, `this` always refers to the class instance — not so in JS!

✅ **Fix**: Use arrow functions or bind explicitly.

---

## 2. **Hoisting**

JavaScript **moves declarations** (not initializations) to the top of their scope.

```javascript
console.log(a); // undefined, not error!
var a = 5;
```

**Why?**  
- `var a` is hoisted and initialized as `undefined` at the top.
- `let` and `const` are hoisted too, but stay in a *"temporal dead zone"* where accessing them throws an error.

✅ **Tip**: Prefer `let` and `const` to avoid hoisting surprises.

---

## 3. **Loose Equality `==` vs Strict Equality `===`**

`==` does **type coercion** before comparing.

```javascript
0 == false;       // true 😱
'0' == 0;          // true 😱
null == undefined; // true
```

**Why?**  
- JavaScript tries to "helpfully" convert types.
- Leads to unpredictable behavior.

✅ **Tip**: Always use `===` unless you have a *very* good reason.

---

## 4. **Array Holes (Sparse Arrays)**

Arrays can have "empty" slots — and behave strangely.

```javascript
const arr = [1, , 3];
console.log(arr.length); // 3
console.log(arr[1]);     // undefined
console.log(arr.map(x => x * 2)); // [2, , 6] (the hole remains)
```

**Why?**  
- JavaScript treats missing elements differently from `undefined`.
- Some array methods skip empty slots.

✅ **Tip**: Be careful when creating or manipulating sparse arrays.

---

## 5. **Floating Point Math Issues**

Because of how numbers are stored in memory (IEEE-754 floating-point standard), math isn't always exact.

```javascript
console.log(0.1 + 0.2 === 0.3); // false 😱
console.log(0.1 + 0.2);         // 0.30000000000000004
```

**Why?**  
- Floating point rounding errors happen internally.

✅ **Tip**: Use rounding when comparing decimals.

```javascript
function almostEqual(a, b) {
  return Math.abs(a - b) < Number.EPSILON;
}
```

---

# 🎯 Quick Summary Table

| Gotcha              | Why It Happens                 | How To Deal With It              |
|---------------------|---------------------------------|----------------------------------|
| `this` confusion     | Call context matters            | Use arrow functions, bind        |
| Hoisting             | Declarations move               | Use `let`/`const`                |
| `==` vs `===`        | Type coercion                   | Always use `===`                 |
| Array holes          | Sparse arrays                   | Validate arrays carefully        |
| Floating point math  | Binary rounding errors          | Round or approximate             |

---

## Function bind
this is set to the object when function is bound. Even if the object changes values later, the original value of object is bound to the function
```javascript
let user = {
firstName: "John",
sayHi() {
console.log(`Hello, ${this.firstName}!`);
}
};
let sayHi = user.sayHi.bind(user); // (*)
// can run it without an object
sayHi(); // Hello, John!
setTimeout(() => {
sayHi() // Hello, Joen!
}, 1000); // Hello, John!
// even if the value of user changes within 1 second
// sayHi uses the pre-bound value which is reference to the old user object
user = {
sayHi() { alert("Another user in setTimeout!"); }
};
sayHi(); // Hello, John!
console.log(user.firstName) // undefined
```

## Static methods
Static properties/methods are used when we’d like to store class-level data, also not bound to an instance. 
Static methods are inherited between classes.
Subclasses can call or override them.
They are not accessible on instances — only on constructors.

Ex: why obj.toString() can't be static - 
It’s designed to be overridden per object.

It needs access to instance data via this.

JS allows custom representations by modifying the prototype, not the constructor.

Static methods are ideal for utility functions that don't require access to instance-specific data.

Prototype methods are designed for operations that need to interact with or modify the instance's data.

The placement of a method (static vs. prototype) is determined by whether it needs access to the instance (this) or can function independently.

If same method name exists in prototype chain and constructor chain - They don't conflict because 
Animal.speak() calls the static method.

a.speak() (where a is an instance) calls the instance method on the prototype chain.

They don’t conflict because:

Static methods are on the constructor (Animal)

Prototype methods are on Animal.prototype — used by instances
