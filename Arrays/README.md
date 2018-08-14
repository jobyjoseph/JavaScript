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

### Reading and Writing Array Elements
You access an element of an array using the `[]` operator. A reference to the array should appear to the left of the brackets. An arbitrary expression that has a non-negative integer value should be inside the brackets. You can use this syntax to both read and write the value of an element of an array.
```javascript
var a = ["Apple", "Banana"];
a[0] // Read first element
a[2] = "Kiwi" // Write third element
```

Remember that arrays are a specialized kind of object. The square brackets used to access array elements work just like the square brackets used to access object properties. JavaScript converts the numeric array index you specify to a string—the index 1 becomes the string "1"—then uses that string as a property name.
```javascript
var a = ["Apple", "Banana"];
a["1"] = "Orange"; // Banana is replaced by Orange.
```

The fact that array indexes are simply a special type of object property name means that JavaScript arrays have no notion of an _out of bounds_ error.
```javascript
a = [true, false];  // This array has elements at indexes 0 and 1
a[2]                // => undefined. No element at this index.
a[-1]               // => undefined. No property with this name.
```