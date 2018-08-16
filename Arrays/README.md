An array is an ordered collection of values. Each value is called an _element_, and each element has a numeric position in the array, known as its _index_. JavaScript arrays are _untyped_: an array element may be of any type, and different elements of the same array may be of different types. JavaScript arrays are _zero-based_ and use 32-bit indexes

JavaScript arrays are a specialized form of JavaScript object, and array indexes are really little more than property names that happen to be integers.

### Creating Arrays

The easiest way to create an array is with an array literal.

```javascript
var empty = []; // An array with no elements
var primes = [2, 3, 5, 7, 11]; // An array with 5 numeric elements
var misc = [1.1, true, "a"]; // 3 elements of various types + trailing comma
```

If you omit a value from an array literal, the omitted element is given the value `undefined`.

```javascript
var count = [1, , 3]; // An array with 3 elements, the middle one undefined.
var undefs = [, ,]; // An array with 2 elements, both undefined.
```

Array literal syntax allows an optional trailing comma, so `[,,]` has only two elements, not three.

Another way to create an array is with the `Array()` constructor. You can invoke this constructor in three distinct ways:

- Call it with no arguments:

```javascript
var a = new Array(); // Equivalent to var a = []
```

- Call it with a single numeric argument, which specifies a length:

```javascript
var a = new Array(10); // Creates an array with specified length
```

- Explicitly specify two or more array elements or a single non-numeric element for the array:

```javascript
var a = new Array(5, 4, 3, 2, 1, "testing, testing"); // Arguments are now elements of array
```

### Reading and Writing Array Elements

You access an element of an array using the `[]` operator. A reference to the array should appear to the left of the brackets. An arbitrary expression that has a non-negative integer value should be inside the brackets. You can use this syntax to both read and write the value of an element of an array.

```javascript
var a = ["Apple", "Banana"];
a[0]; // Read first element
a[2] = "Kiwi"; // Write third element
```

Remember that arrays are a specialized kind of object. The square brackets used to access array elements work just like the square brackets used to access object properties. JavaScript converts the numeric array index you specify to a string—the index 1 becomes the string "1"—then uses that string as a property name.

```javascript
var a = ["Apple", "Banana"];
a["1"] = "Orange"; // Banana is replaced by Orange.
```

The fact that array indexes are simply a special type of object property name means that JavaScript arrays have no notion of an _out of bounds_ error.

```javascript
a = [true, false]; // This array has elements at indexes 0 and 1
a[2]; // => undefined. No element at this index.
a[-1]; // => undefined. No property with this name.
```

### Array Length

Every array has a _length_ property, and it is this property that makes arrays different from regular JavaScript objects. For arrays that are dense (i.e., not sparse), the _length_ property specifies the number of elements in the array.

If you assign a value to an array element whose index `i` is greater than or equal to the array’s current length, the value of the length property is set to `i+1`. If you set the length property to a non-negative integer `n` smaller than its current value, any array elements whose index is greater than or equal to `n` are deleted from the array.

```javascript
a = [1, 2, 3, 4, 5]; // Start with a 5-element array.
a.length = 3; // a is now [1,2,3].
a.length = 0; // Delete all elements. a is [].
a.length = 5; // Length is 5, but no elements, like new Array(5)
```

### Adding and Deleting Array Elements

The simplest way to add elements to an array is to just assign values to new indexes.
```javascript
a = []          // Start with an empty array. 
a[0] = "zero";  // And add elements to it. 
a[1] = "one";
```

Another way to add an element is to use `push()` method.
```javascript
a = [];                 // Start with an empty array
a.push("zero")          // Add a value at the end. a = ["zero"] 
a.push("one", "two")    // Add two more values. a = ["zero", "one", "two"]
```

You can use the `unshift()` method to insert a value at the beginning of an array, shifting the existing array elements to higher indexes.
```javascript
var a = ["Apple", "Banana"];
a.unshift("Orange", "Kiwi"); // ["Orange", "Kiwi", "Apple", "Banana"]
```

You can delete array elements with the `delete` operator, just as you can delete object properties.
```javascript
a = [1,2,3]; 
delete a[1];    // a now has no element at index 1
1 in a          // => false: no array index 1 is defined
a.length        // => 3: delete does not affect array length
```
If you delete an element from an array, the array becomes sparse.

Arrays have a `pop()` method (it works with `push()`) that reduces the length of an array by 1 but also returns the value of the deleted element.
```javascript
var a = ["Apple", "Banana", "Orange", "Kiwi"];
a.pop()     // "Kiwi"
a           // ["Apple", "Banana", "Orange"] 
```

 There is also a `shift()`method (which goes with `unshift()`) to remove an element from the beginning of an array. Unlike `delete`, the `shift()` method shifts all elements down to an index one lower than their current index.
 ```javascript
var a = ["Apple", "Banana", "Orange", "Kiwi"];
a.shift()   // "Apple"
a           // ["Banana", "Orange", "Kiwi"]
 ```