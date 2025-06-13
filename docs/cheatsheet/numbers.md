
# 📘 JavaScript Numbers – Summary with Examples

## 1. **Number Literals and Notation**

### a. **Scientific Notation (`e`)**
Scientific notation allows for concise representation of large or small numbers

```javascript
let billion = 1e9; // 1 * 10^9 = 1000000000
let microsecond = 1e-6; // 1 / 10^6 = 0.000001
```


### b. **Underscore `_` as a Digit Separator**
Improves readability of numeric literals

```javascript
let billion = 1_000_000_000; // Same as 1000000000
```


### c. **Hexadecimal, Binary, and Octal Notation**
JavaScript supports different numeral systems using prefixes

```javascript
let hex = 0xFF; // 255 in hexadecimal
let binary = 0b11111111; // 255 in binary
let octal = 0o377; // 255 in octal
```


## 2. **Number Conversion**

### a. **`Number()` Function**
Converts various types to numbers

```javascript
Number("123"); // 123
Number("123abc"); // NaN
```


### b. **`parseInt()` and `parseFloat()`**
Parses a string and returns an integer or floating-point number, respectively

```javascript
parseInt("100px"); // 100
parseFloat("12.5em"); // 12.5
```

Both functions parse up to the first non-numeric character

### c. **`isNaN()` and `isFinite()`**
Checks for NaN and finite numbers. You cannot compared Nan to Nan because The value NaN is unique in that it does not equal anything, including itself:

```javascript
isNaN(NaN); // true
isFinite("15"); // true
isFinite("str"); // false
```

## 3. **Number Methods**

### a. **`toString(base)`**
Converts a number to a string in the specified base (2 to 36)

```javascript
let num = 255;
num.toString(16); // "ff"
num.toString(2); // "11111111"
```


### b. **`toFixed(n)`**
Formats a number using fixed-point notation

```javascript
let num = 12.3456;
num.toFixed(2); // "12.35"
```


### c. **`toPrecision(n)`**
Formats a number to the specified length

```javascript
let num = 12.3456;
num.toPrecision(4); // "12.35"
```


## 4. **Handling Rounding Errors**
Due to binary floating-point representation, some decimal fractions cannot be represented exactly

```javascript
0.1 + 0.2 === 0.3; // false
```

To mitigate this, use rounding functions

```javascript
+(0.1 + 0.2).toFixed(10); // 0.3
```


## 5. **Math Object**
Provides mathematical constants and functions

```javascript
Math.floor(3.7); // 3
Math.ceil(3.2); // 4
Math.round(3.5); // 4
Math.trunc(3.9); // 3
Math.random(); // Random number between 0 and 1
Math.max(1, 2, 3); // 3
Math.min(1, 2, 3); // 1
Math.pow(2, 3); // 8
```


## 6. **`readNumber()` Function**
Prompts the user for a number until a valid numeric value is entered. Returns `null` if the input is empty or canceled

```javascript
function readNumber() {
  let num;
  do {
    num = prompt("Enter a number:", 0);
  } while (!isFinite(num));

  if (num === null || num === '') return null;
  return +num;
}
```


---

Refer https://javascript.info/number for more methods and details 
