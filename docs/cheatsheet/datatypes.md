There are 7 primitive types: string, number, bigint, boolean, symbol, null and undefined.

Objects are “heavier” than primitives. They require additional resources to support the internal machinery.

## Primitive as Object 
Here’s the paradox faced by the creator of JavaScript:
1. There are many things one would want to do with a primitive, like a string or a number. It would be great to access them using methods.
2. Primitives must be as fast and lightweight as possible.
   
The solution looks a little bit awkward, but here it is:
1. Primitives are still primitive. A single value, as desired.
2. The language allows access to methods and properties of strings, numbers, booleans and symbols.
3. In order for that to work, a special “object wrapper” that provides the extra functionality **is created, and then is destroyed.**

The “object wrappers” are different for each primitive type and are called: String, Number, Boolean, Symbol and BigInt. Thus, they provide different sets of methods. 
```javascript
  let str = "Hello";
  alert( str.toUpperCase() ); // HELLO
```

1. The string str is a primitive. So in the moment of accessing its property, a special object is created that knows the value of the string, and has useful methods, like toUpperCase().
2. That method runs and returns a new string (shown by alert).
3. The special object is destroyed, leaving the primitive str alone. So primitives can provide methods, but they still remain lightweight.

## Methods of Primitives 
Can I add a string property?
```javascript
  let str = "Hello";
  str.test = 5; // (*)
  alert(str.test);
```
Depending on whether you have use strict or not, the result may be:
1. undefined (no strict mode)
2. An error (strict mode).
Why? Let’s replay what’s happening at line (*):
1. When a property of str is accessed, a “wrapper object” is created.
2. In strict mode, writing into it is an error.
3. Otherwise, the operation with the property is carried on, the object gets the test property, but after that the “wrapper object” disappears, so in the last line str has no trace of the property.
This example clearly shows that primitives are not objects. They can’t store additional data.

Don't create primitives using Object wrappers
```javascript
   alert( typeof 0 ); // "number"
   alert( typeof new Number(0) ); // "object"!
   let num = Number("123"); // convert a string to number. without new is totally fine
```
