An array is an ordered collection of values. Each value is called an _element_, and each element has a numeric position in the array, known as its _index_. JavaScript arrays are _untyped_: an array element may be of any type, and different elements of the same array may be of different types. JavaScript arrays are _zero-based_ and use 32-bit indexes

JavaScript arrays are a specialized form of JavaScript object, and array indexes are really little more than property names that happen to be integers.

### Creating Arrays
The easiest way to create an array is with an array literal.
```javascript
var empty = [];                     // An array with no elements
var primes = [2, 3, 5, 7, 11];      // An array with 5 numeric elements
var misc = [ 1.1, true, "a", ];     // 3 elements of various types + trailing comma
```