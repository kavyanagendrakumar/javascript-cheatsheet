---
title: Javascript String Formatting - Javascript Cheatsheet
description: In JavaScript, string formatting can be achieved in several ways. One common method is using template literals.
---

<base-title :title="frontmatter.title" :description="frontmatter.description">
Javascript String Formatting
</base-title>

## Template Literals

**Template literals** (also known as template strings) are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were introduced in ECMAScript 6.

<base-disclaimer>
  <base-disclaimer-title>
    From the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals" target="_blank">MDN Web Docs</a>
  </base-disclaimer-title>
  <base-disclaimer-content>
    Template literals are literals delimited with backtick (`) characters, allowing for multi-line strings, string interpolation with embedded expressions, and special constructs called tagged templates.
  </base-disclaimer-content>
</base-disclaimer>

Template literals can contain placeholders, indicated by the dollar sign and curly braces (`${expression}`). The expressions in the placeholders and the text between them get passed to a function.

```javascript
let name = "John";
let age = 30;
let greeting = `Hello, my name is ${name} and I am ${age} years old.`;

console.log(greeting); // Outputs: "Hello, my name is John and I am 30 years old."
```

Here, `name` and `age` are variables. The template literal is defined using backticks, and the variables are embedded in the string using `${}` syntax. The resulting string is stored in the `greeting` variable and then logged to the console.

## Accessing characters
Accessing characters
To get a character at position pos , use square brackets [pos] or call the method str.at(pos)  . The first character starts
from the zero position:
```javascript
let str = `Hello`;
// the first character
alert( str[0] ); // H
alert( str.at(0) ); // H
// the last character
alert( str[str.length - 1] ); // o
alert( str.at(-1) );
```
As you can see, the .at(pos) method has a benefit of allowing negative position. If pos is negative, then it’s counted from
the end of the string.
So .at(-1) means the last character, and .at(-2) is the one before it, etc.
The square brackets always return undefined for negative indexes, for instance:
```javascript
let str = `Hello`;
alert( str[-2] ); // undefined
alert( str.at(-2) ); // l
```
We can also iterate over characters using for..of :
```javascript
for (let char of "Hello") {
alert(char); // H,e,l,l,o (char becomes "H", then "e", then "l" etc)
}
```
Strings are immutable
Strings can’t be changed in JavaScript. It is impossible to change a character.
Let’s try it to show that it doesn’t work:
```javascript
let str = 'Hi';
str[0] = 'h'; // error
alert( str[0] ); // doesn't work
```
The usual workaround is to create a whole new string and assign it to str instead of the old one.
For instance:
```javascript
let str = 'Hi';
str = 'h' + str[1]; // replace the string
alert( str ); // hi
```

## String Concatenation

String concatenation is the operation of joining two or more strings together. This can be achieved using the `+` operator or the `concat` method.

### Using the `+` Operator

Here's an example of string concatenation using the `+` operator:

```javascript
let str1 = "Hello, ";
let str2 = "World!";
let result = str1 + str2;

console.log(result); // Outputs: "Hello, World!"
```

`str1` and `str2` are strings. The `+` operator is used to concatenate `str1` and `str2` together. The resulting string is stored in the `result` variable and then logged to the console.

### Using the `concat` Method

Here's an example of string concatenation using the `concat` method:

```javascript
let str1 = "Hello, ";
let str2 = "World!";
let result = str1.concat(str2);

console.log(result); // Outputs: "Hello, World!"
```

`str1` and `str2` are strings. The `concat` method is called on `str1` with `str2` as the argument, concatenating `str1` and `str2` together. The resulting string is stored in the `result` variable and then logged to the console.

## The recommended way

The recommended way to format strings in JavaScript is by using Template Literals (Template Strings) introduced in ECMAScript 6 (ES6). Template literals allow you to embed expressions, create multi-line strings, and use string interpolation features, making them a powerful tool for string formatting.

<base-title :title="frontmatter.title" :description="frontmatter.description">
Javascript String Manipulation
</base-title>

<base-disclaimer>
  <base-disclaimer-title>
    Manipulating Strings
  </base-disclaimer-title>
  <base-disclaimer-content>
    String manipulation refers to the process of changing, parsing, slicing, or analyzing strings in various ways.
  </base-disclaimer-content>
</base-disclaimer>

## Concat

The `concat` method is used to join two or more strings together. This method does not change the existing strings, but returns a new string containing the text of the joined strings.

```javascript
let str1 = "Hello, ";
let str2 = "World!";
let result = str1.concat(str2);

console.log(result); // Outputs: "Hello, World!"
```

`str1` and `str2` are two strings. The `concat` method is called on `str1` with `str2` as the argument, resulting in a new string that is the concatenation of `str1` and `str2`. The new string is stored in the `result` variable.

## CharAt

`charAt` method is used to get the character at a specific index in a string. The index of the first character is 0, the second character is 1, and so on.

```javascript
let str = "Hello, World!";
let char = str.charAt(7);

console.log(char); // Outputs: "W"
```

Here, `str` is a string. The `charAt` method is called on `str` with 7 as the argument, which corresponds to the 8th character in the string (since the index is 0-based). The character at this index is "W", so "W" is stored in the `char` variable and then logged to the console.

## Includes

The `includes` method is used to determine whether one string can be found within another string, returning true or false as appropriate. It performs a case-sensitive search.

```javascript
let str = "Hello, World!";
let result = str.includes("World");

console.log(result); // Outputs: true
```

`str` is a string. The `includes` method is called on `str` with "World" as the argument. Since "World" is a substring of `str`, the `includes` method returns true, which is stored in the `result` variable and then logged to the console.

## IndexOf

`indexOf` method is used to determine the first occurrence of a specified value in a string. It returns the index of the value if found, or -1 if the value is not found. The search is case-sensitive.

```javascript
let str = "Hello, World!";
let index = str.indexOf("World");

console.log(index); // Outputs: 7
```

`str` is a string. The `indexOf` method is called on `str` with "World" as the argument. Since "World" is a substring of `str` and starts at index 7, the `indexOf` method returns 7, which is stored in the `index` variable and then logged to the console.

## Slice

The `slice` method is used to extract a section of a string and returns it as a new string, without modifying the original string. The method takes two parameters: the start index (inclusive), and the end index (exclusive).

```javascript
let str = "Hello, World!";
let slicedStr = str.slice(7, 12);

console.log(slicedStr); // Outputs: "World"
```

Here, `str` is a string. The `slice` method is called on `str` with 7 as the start index and 12 as the end index. This extracts the substring starting from the 8th character up to (but not including) the 13th character. The resulting substring "World" is stored in the `slicedStr` variable and then logged to the console.

## Split

The `split` method is used to divide a string into an array of substrings. It takes a separator as an argument, which specifies the character(s) to use for separating the string. If the separator is not provided, the entire string will be returned as a single element in an array.

```javascript
let str = "Hello, World!";
let array = str.split(", ");

console.log(array); // Outputs: ["Hello", "World!"]
```

`str` is a string. The `split` method is called on `str` with ", " as the separator. This divides the string into two substrings "Hello" and "World!", which are returned as elements in an array. The array is stored in the `array` variable and then logged to the console.

## Replace

The `replace` method is used to replace a specified value with another value in a string. It returns a new string with some or all matches of a pattern replaced by a replacement. The original string is not modified.

```javascript
let str = "Hello, World!";
let newStr = str.replace("World", "Universe");

console.log(newStr); // Outputs: "Hello, Universe!"
```

`str` is a string. The `replace` method is called on `str` with "World" as the pattern to be replaced and "Universe" as the replacement. This results in a new string "Hello, Universe!", which is stored in the `newStr` variable and then logged to the console.

## ToLowerCase

The `toLowerCase` method is used to convert a string to lowercase letters. This method does not change the original string, but returns a new string where all the uppercase characters are converted to lowercase.

```javascript
let str = "Hello, World!";
let lowerCaseStr = str.toLowerCase();

console.log(lowerCaseStr); // Outputs: "hello, world!"
```

`str` is a string. The `toLowerCase` method is called on `str`, resulting in a new string where all the uppercase characters are converted to lowercase. The new string is stored in the `lowerCaseStr` variable and then logged to the console.

## ToUpperCase

The `toUpperCase` method is used to convert a string to uppercase letters. This method does not change the original string, but returns a new string where all the lowercase characters are converted to uppercase.

Here's an example of how to use the `toUpperCase` method:

```javascript
let str = "Hello, World!";
let upperCaseStr = str.toUpperCase();

console.log(upperCaseStr); // Outputs: "HELLO, WORLD!"
```

`str` is a string. The `toUpperCase` method is called on `str`, resulting in a new string where all the lowercase characters are converted to uppercase. The new string is stored in the `upperCaseStr` variable and then logged to the console.

## Trim

The `trim` method is used to remove whitespace from both ends of a string. This method does not change the original string, but returns a new string with the whitespace removed.

```javascript
let str = "   Hello, World!   ";
let trimmedStr = str.trim();

console.log(trimmedStr); // Outputs: "Hello, World!"
```

`str` is a string with leading and trailing whitespace. The `trim` method is called on `str`, resulting in a new string where the whitespace at both ends is removed. The new string is stored in the `trimmedStr` variable and then logged to the console.

## TrimLeft and TrimRight

`trimLeft` and `trimRight` methods are used to remove whitespace from the beginning and end of a string respectively. These methods do not change the original string, but return a new string with the whitespace removed.

```javascript
let str = "   Hello, World!   ";
let trimmedLeftStr = str.trimLeft();
let trimmedRightStr = str.trimRight();

console.log(trimmedLeftStr); // Outputs: "Hello, World!   "
console.log(trimmedRightStr); // Outputs: "   Hello, World!"
```

In this example, `str` is a string with leading and trailing whitespace. The `trimLeft` method is called on `str`, resulting in a new string where the whitespace at the beginning is removed. Similarly, the `trimRight` method is called on `str`, resulting in a new string where the whitespace at the end is removed. The new strings are stored in the `trimmedLeftStr` and `trimmedRightStr` variables and then logged to the console.

## toLocaleString()
the toLocaleString() method is used to format dates, numbers, and other objects according to the user's locale settings.
** Syntax
```javascript
toLocaleString()
toLocaleString(locales)
toLocaleString(locales, options)
```
** Number
```javascript
  const number = 123456.789;

  // Default formatting (based on user's locale)
  console.log(number.toLocaleString()); // "123,456.789" (in US English locale)

  // Specific locale
  console.log(number.toLocaleString('de-DE')); // "123.456,789" (in German locale)

  // Customize formatting options
  console.log(number.toLocaleString('en-US', { style: 'currency', currency: 'USD' })); // "$123,456.79"
```
** Date
```javascript
  const date = new Date();

  // Default formatting (based on user's locale)
  console.log(date.toLocaleString()); // "1/30/2025, 9:25:19 AM" (in US English locale)

  // Specific locale
  console.log(date.toLocaleString('fr-FR')); // "30/01/2025 09:25:19" (in French locale)

  // Customize formatting options
  console.log(date.toLocaleString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })); // "Thursday, January 30, 2025"
```
** Array
```javascript
  const array = [1, 2, 3];

  console.log(array.toLocaleString()); // "1,2,3"
```
# String Methods Cheat Sheet

```javascript
const str = 'HeLlo';
const stringObj = new String('grace');
```

| Methods       | Code Example                | Result                    | Return Type |
| ------------- | --------------------------- | ------------------------- | ----------- |
| indexOf       | str.indexOf('L')            | 2                         | number      |
| indexOf()     | 'hello'.indexOf('l')        | 2                         | number      |
| indexOf()     | str.indexOf('L')            | 2                         | number      |
| lastIndexOf() | 'hello'.lastIndexOf('l')    | 3                         | number      |
| search()      | str.search(/[a-z]/g)        | 1                         | number      |
| endsWith()    | str.endsWith('z')           | FALSE                     | boolean     |
| endsWith()    | str.endsWith('o', 6)        | TRUE                      | boolean     |
| includes()    | str.includes('a')           | FALSE                     | boolean     |
| startsWith()  | str.startsWith('H', 1)      | FALSE                     | boolean     |
| startsWith()  | str.startsWith('H')         | TRUE                      | boolean     |
| charAt()      | str.charAt(1)               | e                         | string      |
| concat()      | str.concat(' grace')        | HeLlo grace               | string      |
| padEnd()      | str.padEnd(10, '!')         | HeLlo!!!!!                | string      |
| padStart()    | str.padStart(10, '!')       | !!!!!HeLlo                | string      |
| repeat()      | str.repeat(3))              | HeLloHeLloHeLlo           | string      |
| replace()     | str.replace('L', 'l')       | Hello                     | string      |
| replaceAll()  | hello'.replaceAll('l', 'z') | hezzo                     | string      |
| slice()       | str.slice(1, 3)             | eL                        | string      |
| slice()       | str.slice(2)                | Llo                       | string      |
| substring()   | str.substring(2)            | Llo                       | string      |
| substring()   | str.substring(1, 3)         | eL                        | string      |
| toLowerCase() | str.toLowerCase()           | hello                     | string      |
| toUpperCase() | str.toUpperCase()           | HELLO                     | string      |
| trim()        | ' hello '.trim()            | 'hello'                   | string      |
| trimEnd()     | ' hello '.trimEnd()         | ' hello'                  | string      |
| trimStart()   | ' hello '.trimStart()       | 'hello '                  | string      |
| valueOf()     | stringObj.valueOf()         | grace                     | string      |
| match()       | str.match(/[A-Z]/g)         | ["H", "L"]                | array       |
| split()       | str.split()                 | ["HeLlo"]                 | array       |
| split()       | str.split('')               | ["H", "e", "L", "l", "o"] | array       |

