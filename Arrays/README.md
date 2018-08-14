An array is an ordered collection of values. Each value is called an _element_, and each element has a numeric position in the array, known as its _index_. JavaScript arrays are _untyped_: an array element may be of any type, and different elements of the same array may be of different types. JavaScript arrays are _zero-based_ and use 32-bit indexes

JavaScript arrays are a specialized form of JavaScript object, and array indexes are really little more than property names that happen to be integers.

### Creating Arrays
The easiest way to create an array is with an array literal.
```javascript
var empty = [];                     // An array with no elements
var primes = [2, 3, 5, 7, 11];      // An array with 5 numeric elements
var misc = [ 1.1, true, "a", ];     // 3 elements of various types + trailing comma
```

If you omit a value from an array literal, the omitted element is given the value `undefined`.
```javascript
var count = [1,,3]; // An array with 3 elements, the middle one undefined. 
var undefs = [,,];  // An array with 2 elements, both undefined.
```
Array literal syntax allows an optional trailing comma, so `[,,]` has only two elements, not three.

Another way to create an array is with the `Array()` constructor. You can invoke this constructor in three distinct ways:
* Call it with no arguments:
```javascript
var a = new Array(); // Equivalent to var a = []
```
* Call it with a single numeric argument, which specifies a length:
```javascript
var a = new Array(10); // Creates an array with specified length
```
* Explicitly specify two or more array elements or a single non-numeric element for the array:
```javascript
var a = new Array(5, 4, 3, 2, 1, "testing, testing"); // Arguments are now elements of array
```