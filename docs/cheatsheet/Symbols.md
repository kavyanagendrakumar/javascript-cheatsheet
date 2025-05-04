**JavaScript Symbol Cheatsheet: Everything You Need to Know**
# JavaScript System Symbols with Examples

| **Symbol**                  | **What it Does**                                          |
|----------------------------|-----------------------------------------------------------|
| `Symbol.iterator`          | Makes an object iterable (`for...of`)                     |
| `Symbol.toPrimitive`       | Custom primitive conversion (`+obj`, `String(obj)`, etc.) |
| `Symbol.toStringTag`       | Custom `[object XYZ]` output for debugging or logs        |
| `Symbol.asyncIterator`     | Enables async iteration (`for await...of`)                |
| `Symbol.hasInstance`       | Customize behavior of `instanceof`                        |
| `Symbol.species`           | Control constructor returned in subclassed objects        |
| `Symbol.match`             | Used by `String.prototype.match()`                        |
| `Symbol.replace`           | Used by `String.prototype.replace()`                      |
| `Symbol.search`            | Used by `String.prototype.search()`                       |
| `Symbol.split`             | Used by `String.prototype.split()`                        |
| `Symbol.isConcatSpreadable`| Controls behavior in `Array.prototype.concat()`           |
| `Symbol.unscopables`       | Hides properties from `with` statements                   |

```javascipt
// Example
const obj = {
  [Symbol.toStringTag]: "MyObject"
};

console.log(Object.prototype.toString.call(obj)); // [object MyObject]
```

## `Symbol.iterator` — Makes an object iterable (`for...of`)
Read Iterables (Important) - https://javascript.info/iterable

Youtube - https://www.youtube.com/watch?v=6D7XOGXbyfs&ab_channel=AndrewBurgess 
```javascript
const obj = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
  }
};

for (const val of obj) console.log(val); // 1, 2
```

## Symbol.toPrimitive — Custom primitive conversion
Read Object to primitive conversion (Important) - https://javascript.info/object-toprimitive 
```javascript
const obj = {
  [Symbol.toPrimitive](hint) {
    return hint === 'number' ? 42 : 'hello';
  }
};

console.log(+obj);     // 42
console.log(`${obj}`); // 'hello'

```

## Symbol.toStringTag — Custom [object XYZ] output
```javascript
const obj = {
  [Symbol.toStringTag]: 'CustomObj'
};

console.log(Object.prototype.toString.call(obj)); // [object CustomObj]

```

## Symbol.asyncIterator — Enables async iteration
```javascript
const obj = {
  async *[Symbol.asyncIterator]() {
    yield 'a';
    yield 'b';
  }
};

(async () => {
  for await (const val of obj) console.log(val);
})();

```

## Symbol.hasInstance — Customize instanceof
```javascript
class MyClass {
  static [Symbol.hasInstance](instance) {
    return typeof instance === 'string';
  }
}

console.log('hello' instanceof MyClass); // true

```

## Symbol.species — Control constructor returned in subclassing
```javascript
class MyArray extends Array {
  static get [Symbol.species]() {
    return Array;
  }
}

const a = new MyArray(1, 2, 3);
const b = a.map(x => x * 2);

console.log(b instanceof MyArray); // false
console.log(b instanceof Array);   // true
```

## Symbol.match — Used by .match()
```javascript
const matcher = {
  [Symbol.match](str) {
    return str.includes('ok') ? ['ok'] : null;
  }
};

console.log('are you ok?'.match(matcher)); // ['ok']
```

## Symbol.replace — Used by .replace()
```javascript
const replacer = {
  [Symbol.replace](str, replacement) {
    return str.split(' ').join(replacement);
  }
};

console.log('hello world'.replace(replacer, '-')); // 'hello-world'
```

## Symbol.search — Used by .search()
```javascript
const searcher = {
  [Symbol.search](str) {
    return str.indexOf('yes');
  }
};

console.log('say yes please'.search(searcher)); // 4
```

## Symbol.split — Used by .split()
```javascript
const splitter = {
  [Symbol.split](str) {
    return str.split('').reverse();
  }
};

console.log('abc'.split(splitter)); // ['c', 'b', 'a']

```

## Symbol.isConcatSpreadable — Spread in .concat()
```javascript
const arr = [1, 2];
const obj = {
  0: 'a',
  1: 'b',
  length: 2,
  [Symbol.isConcatSpreadable]: true
};

console.log(arr.concat(obj)); // [1, 2, 'a', 'b']

```

## Symbol.unscopables — Hide properties in with blocks
```javascript
const obj = {
  a: 1,
  b: 2,
  [Symbol.unscopables]: { b: true }
};

with (obj) {
  console.log(a);        // 1
  console.log(typeof b); // 'undefined'
}

```
Instance-level symbols customize how instances behave.

Static-level symbols customize how classes (constructors) behave.
