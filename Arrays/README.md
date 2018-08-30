An array is an ordered collection of values. Each value is called an _element_, and each element has a numeric position in the array, known as its _index_. JavaScript arrays are _untyped_: an array element may be of any type, and different elements of the same array may be of different types. JavaScript arrays are _zero-based_ and use 32-bit indexes

JavaScript arrays are a specialized form of JavaScript object, and array indexes are really little more than property names that happen to be integers.

## Creating Arrays

The easiest way to create an array is with an array literal.

```javascript
var empty = []; // An array with no elements
var primes = [2, 3, 5, 7, 11]; // An array with 5 numeric elements
var misc = [1.1, true, "a",]; // 3 elements of various types + trailing comma
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

## Reading and Writing Array Elements

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

## Array Length

Every array has a _length_ property, and it is this property that makes arrays different from regular JavaScript objects. For arrays that are dense (i.e., not sparse), the _length_ property specifies the number of elements in the array.

If you assign a value to an array element whose index `i` is greater than or equal to the array’s current length, the value of the length property is set to `i+1`. If you set the length property to a non-negative integer `n` smaller than its current value, any array elements whose index is greater than or equal to `n` are deleted from the array.

```javascript
a = [1, 2, 3, 4, 5]; // Start with a 5-element array.
a.length = 3; // a is now [1,2,3].
a.length = 0; // Delete all elements. a is [].
a.length = 5; // Length is 5, but no elements, like new Array(5)
```

## Adding and Deleting Array Elements

The simplest way to add elements to an array is to just assign values to new indexes.

```javascript
a = []; // Start with an empty array.
a[0] = "zero"; // And add elements to it.
a[1] = "one";
```

Another way to add an element is to use `push()` method.

```javascript
a = []; // Start with an empty array
a.push("zero"); // Add a value at the end. a = ["zero"]
a.push("one", "two"); // Add two more values. a = ["zero", "one", "two"]
```

You can use the `unshift()` method to insert a value at the beginning of an array, shifting the existing array elements to higher indexes.

```javascript
var a = ["Apple", "Banana"];
a.unshift("Orange", "Kiwi"); // ["Orange", "Kiwi", "Apple", "Banana"]
```

You can delete array elements with the `delete` operator, just as you can delete object properties.

```javascript
a = [1, 2, 3];
delete a[1]; // a now has no element at index 1
1 in a; // => false: no array index 1 is defined
a.length; // => 3: delete does not affect array length
```

If you delete an element from an array, the array becomes sparse.

Arrays have a `pop()` method (it works with `push()`) that reduces the length of an array by 1 but also returns the value of the deleted element.

```javascript
var a = ["Apple", "Banana", "Orange", "Kiwi"];
a.pop(); // "Kiwi"
a; // ["Apple", "Banana", "Orange"]
```

There is also a `shift()`method (which goes with `unshift()`) to remove an element from the beginning of an array. Unlike `delete`, the `shift()` method shifts all elements down to an index one lower than their current index.

```javascript
var a = ["Apple", "Banana", "Orange", "Kiwi"];
a.shift(); // "Apple"
a; // ["Banana", "Orange", "Kiwi"]
```

## Iterating Arrays

The most common way to loop through the elements of an array is with a `for` loop.

```javascript
for (var i = 0; i < arr.length; i++) {
  // loop body
}
```

Above code does array length lookup on each iteration. So we can optimize further by

```javascript
for (var i = 0, len = arr.length; i < len; i++) {
  // loop body remains the same
}
```

You can also use a `for/in` loop with sparse arrays.

```javascript
for (var index in sparseArray) {
  var value = sparseArray[index];
  // Now do something with index and value
}
```

A `for/in` loop can return the names of inherited properties, such as the names of methods that have been added to Array.prototype. For this reason you should not use a for/in loop on an array unless you include an additional test to filter out unwanted properties.

```javascript
Array.prototype.name = "Google";
var a = ["Apple", "Banana"];

for (var i in a) {
  if (!a.hasOwnProperty(i)) continue; // Skip inherited properties
  console.log(a[i]); // Will not print "Google"
}
```

`for/in` loop does not guarantee the order in which elements are iterated.

## Array Methods

ECMAScript 3 defines a number of useful array manipulation functions on Array.prototype, which means that they are available as methods of any array. ES5 has added more methods.

### join()

The `Array.join()` method converts all the elements of an array to strings and concat- enates them, returning the resulting string. You can specify an optional string that separates the elements in the resulting string. If no separator string is specified, a comma is used.

```javascript
var a = [1, 2, 3]; // Create a new array with these three elements
a.join(); // => "1,2,3"
a.join(" "); // => "1 2 3"
a.join(""); // => "123"
var b = new Array(10); // An array of length 10 with no elements
b.join("-"); // => '---------': a string of 9 hyphens
```

### reverse()

The `Array.reverse()` method reverses the order of the elements of an array and returns the reversed array. It does this in place; in other words, it doesn’t create a new array with the elements rearranged but instead rearranges them in the already existing array.

```javascript
var a = [1, 2, 3];
a.reverse().join(); // => "3,2,1" and a is now [3,2,1]
```

### sort()

`Array.sort()` sorts the elements of an array in place and returns the sorted array. When `sort()` is called with no arguments, it sorts the array elements in alphabetical order (temporarily converting them to strings to perform the comparison, if necessary).

```javascript
var a = new Array("banana", "cherry", "apple");
a.sort();
var s = a.join(", "); // s == "apple, banana, cherry"
```

If an array contains `undefined` elements, they are sorted to the end of the array. To sort an array into some order other than alphabetical, you must pass a comparison function as an argument to `sort()`.

### concat()

The `Array.concat()` method creates and returns a new array that contains the elements of the original array on which `concat()` was invoked, followed by each of the arguments to concat(). If any of these arguments is itself an array, then it is the array elements that are concatenated, not the array itself. Note, however, that `concat()` does not recursively flatten arrays of arrays. `concat()` does not modify the array on which it is invoked.

```javascript
var a = [1, 2, 3];
a.concat(4, 5); // Returns [1,2,3,4,5]
a.concat([4, 5]); // Returns [1,2,3,4,5]
a.concat([4, 5], [6, 7]); // Returns [1,2,3,4,5,6,7]
a.concat(4, [5, [6, 7]]); // Returns [1,2,3,4,5,[6,7]]
```

### slice()

The `Array.slice()` method returns a slice, or subarray, of the specified array. Its two arguments specify the start and end of the slice to be returned. The returned array contains the element specified by the first argument and all subsequent elements up to, but not including, the element specified by the second argument. If only one argu- ment is specified, the returned array contains all elements from the start position to the end of the array. If either argument is negative, it specifies an array element relative to the last element in the array. An argument of -1, for example, specifies the last element in the array, and an argument of -3 specifies the third from last element of the array. Note that slice() does not modify the array on which it is invoked.

```javascript
var a = [1, 2, 3, 4, 5];
a.slice(0, 3); // Returns [1,2,3]
a.slice(3); // Returns [4,5]
a.slice(1, -1); // Returns [2,3,4]
a.slice(-3, -2); // Returns [3]
```

### splice()

The `Array.splice()` method is a general-purpose method for inserting or removing elements from an array. Unlike `slice()` and `concat()`, `splice()` modifies the array on which it is invoked. Note that `splice()` and `slice()` have very similar names but per- form substantially different operations.

`splice()` can delete elements from an array, insert new elements into an array, or perform both operations at the same time. Elements of the array that come after the insertion or deletion point have their indexes increased or decreased as necessary so that they remain contiguous with the rest of the array. The first argument to `splice()` specifies the array position at which the insertion and/or deletion is to begin. The second argument specifies the number of elements that should be deleted from (spliced out of) the array. If this second argument is omitted, all array elements from the start element to the end of the array are removed. `splice()` returns an array of the deleted elements, or an empty array if no elements were deleted. For example:

```javascript
var a = [1, 2, 3, 4, 5, 6, 7, 8];
a.splice(4); // Returns [5,6,7,8]; a is [1,2,3,4]
a.splice(1, 2); // Returns [2,3]; a is [1,4]
a.splice(1, 1); // Returns [4]; a is [1]
```

The first two arguments to `splice()` specify which array elements are to be deleted. These arguments may be followed by any number of additional arguments that specify elements to be inserted into the array, starting at the position specified by the first argument. For example:

```javascript
var a = [1, 2, 3, 4, 5];
a.splice(2, 0, "a", "b"); // Returns []; a is [1,2,'a','b',3,4,5]
a.splice(2, 2, [1, 2], 3); // Returns ['a','b']; a is [1,2,[1,2],3,3,4,5]
```

Note that, unlike `concat()`, `splice()` inserts arrays themselves, not the elements of those arrays.

### push() and pop()

The `push()` and `pop()` methods allow you to work with arrays as if they were stacks. The `push()` method appends one or more new elements to the end of an array and returns the new length of the array. The `pop()` method does the reverse: it deletes the last element of an array, decrements the array length, and returns the value that it removed. Note that both methods modify the array in place rather than produce a modified copy of the array. The combination of `push()` and `pop()` allows you to use a JavaScript array to implement a first-in, last-out stack. For example:

```javascript
var stack = []; // stack: []
stack.push(1, 2); // stack: [1,2] Returns 2
stack.pop(); // stack: [1] Returns 2
stack.push(3); // stack: [1,3] Returns 2
stack.pop(); // stack: [1] Returns 3
stack.push([4, 5]); // stack: [1,[4,5]] Returns 2
stack.pop(); // stack: [1] Returns [4,5]
stack.pop(); // stack: [] Returns 1
```

### unshift() and shift()

The `unshift()` and `shift()` methods behave much like `push()` and `pop()`, except that they insert and remove elements from the beginning of an array rather than from the end. `unshift()` adds an element or elements to the beginning of the array, shifts the existing array elements up to higher indexes to make room, and returns the new length of the array. `shift()` removes and returns the first element of the array, shifting all subsequent elements down one place to occupy the newly vacant space at the start of the array. For example:

```javascript
var a = []; // a:[]
a.unshift(1); // a:[1]            Returns: 1
a.unshift(22); // a:[22,1]         Returns: 2
a.shift(); // a:[1]            Returns: 22
a.unshift(3, [4, 5]); // a:[3,[4,5],1]    Returns: 3
a.shift(); // a:[[4,5],1]      Returns: 3
a.shift(); // a:[1]            Returns: [4,5]
a.shift(); // a:[]             Returns: 1
```

Note the possibly surprising behavior of `unshift()` when it's invoked with multiple arguments. Instead of being inserted into the array one at a time, arguments are inserted all at once (as with the `splice()` method). This means that they appear in the resulting array in the same order in which they appeared in the argument list. Had the elements been inserted one at a time, their order would have been reversed.

### toString() and toLocaleString()

For an array, `toString()` method converts each of its elements to a string (calling the `toString()` methods of its elements, if necessary) and outputs a comma-separated list of those strings. Note that the output does not include square brackets or any other sort of delimiter around the array value.

```javascript
[1, 2, 3]
  .toString() // Yields '1,2,3'
  [("a", "b", "c")].toString() // Yields 'a,b,c'
  [(1, [2, "c"])].toString(); // Yields '1,2,c'
```

`toLocaleString()` is the localized version of `toString()`. It converts each array element to a string by calling the `toLocaleString()` method of the element, and then it concat- enates the resulting strings using a locale-specific (and implementation-defined) sepa- rator string.

## ECMAScript 5 Array Methods

There are few points common to ES5 Array methods. First, most of the methods accept a function as their first argument and invoke that function once for each element (or some elements) of the array. If the array is sparse, the function you pass is not invoked for nonexistent elements. In most cases, the function you supply is invoked with three arguments: the value of the array element, the index of the array element, and the array itself. None of the ECMAScript 5 array methods modify the array on which they are invoked.

### forEach()

The `forEach()` method iterates through an array, invoking a function you specify for each element.

```javascript
var a = [2, 4, 6, 8, 10];
var sum = 0;
a.forEach(function(value) {
  sum += value;
});
console.log(sum); // 30
```

Note that `forEach()` does not provide a way to terminate iteration before all elements have been passed to the function. That is, there is no equivalent of the break statement you can use with a regular for loop. If you need to terminate early, you must throw an exception, and place the call to `forEach()` within a try block.

### map()

The `map()` method passes each element of the array on which it is invoked to the function you specify, and returns an array containing the values returned by that function.

```javascript
a = [1, 2, 3];
b = a.map(function(x) {
  return x * x;
}); // b is [1, 4, 9]
```

The function you pass to `map()` is invoked in the same way as a function passed to `forEach()`. For the `map()` method, however, the function you pass should return a value. Note that `map()` returns a new array: it does not modify the array it is invoked on. If that array is sparse, the returned array will be sparse in the same way: it will have the same length and the same missing elements.

### filter()

The `filter()` method returns an array containing a subset of the elements of the array on which it is invoked. The function you pass to it should be predicate: a function that returns `true` or `false`. If the return value is `true`, or a value that converts to `true`, then the element passed to the predicate is a member of the subset and is added to the array that will become the return value.

```javascript
// Original Array
var arr = [1, 2, 3, 4, 5, 6, 7];
// Function to be passed to filter method
var filterFunction = function(value) {
  return value % 2 == 0;
};
// Create an array with only even numbers
var evenArr = arr.filter(filterFunction);
console.log(evenArr); // [2, 4, 6]
```

Note that `filter()` skips missing elements in sparse arrays, and that its return value is always dense. To close the gaps in a sparse array, you can do this:

```javascript
var dense = sparse.filter(function() {
  return true;
});
```

### every() and some()

The `every()` and `some()` methods are array predicates: they apply a predicate function you specify to the elements of the array, and then return true or false. `every()` method returns true if and only if your predicate function returns true for all elements in the array:

```javascript
a = [1, 2, 3, 4, 5];
a.every(function(x) {
  return x < 10;
}); // => true: all values < 10.
a.every(function(x) {
  return x % 2 === 0;
}); // => false: not all values even.
```

`each()` method returns `true` if there exists at least one element in the array for which the predicate returns `true`, and returns `false` if and only if the predicate returns `false` for all elements of the array.

```javascript
a = [1, 2, 3, 4, 5];
a.some(function(x) {
  return x % 2 === 0;
}); // => true a has some even numbers.
a.some(isNaN); // => false: a has no non-numbers.
```

### reduce(), reduceRight()

The `reduce()` and `reduceRight()` methods combine the elements of an array, using the function you specify, to produce a single value.

```javascript
var a = [1, 2, 3, 4, 5];
var sum = a.reduce(function(x, y) {
  return x + y;
}, 0); // Sum of values
```

`reduce()` takes two arguments. The first is the function that performs the reduction operation. The task of this reduction function is to somehow combine or reduce two values into a single value, and to return that reduced value. The second (optional) argument is an initial value to pass to the function

Functions used with `reduce()` are different than the functions used with `forEach()` and `map()`. The familiar value, index, and array values are passed as the second, third, and fourth arguments. The first argument is the accumulated result of the reduction so far. On the first call to the function, this first argument is the initial value you passed as the second argument to `reduce()`. On subsequent calls, it is the value returned by the previous invocation of the function.

When you invoke `reduce()` with no initial value, it uses the first element of the array as the initial value. This means that the first call to the reduction function will have the first and second array elements as its first and second arguments.

Calling `reduce()` on an empty array with no initial value argument causes a TypeError. If you call it with only one value—either an array with one element and no initial value or an empty array and an initial value—it simply returns that one value without ever calling the reduction function.

`reduceRight()` works just like reduce(), except that it processes the array from highest index to lowest (right-to-left), rather than from lowest to highest.

### indexOf() and lastIndexOf()

`indexOf()` and `lastIndexOf()` search an array for an element with a specified value, and return the index of the first such element found, or –1 if none is found. `indexOf()` searches the array from beginning to end, and `lastIndexOf()` searches from end to beginning.

```javascript
a = [0, 1, 2, 1, 0];
a.indexOf(1); // => 1: a[1] is 1
a.lastIndexOf(1); // => 3: a[3] is 1
a.indexOf(3); // => -1: no element has value 3
```

Note that strings have `indexOf()` and `lastIndexOf()` methods that work like these array

## Array Type

Given an unknown object, it is often useful to be able to determine whether it is an array or not. In ECMAScript 5, you can do this with the `Array.isArray()` function:

```javascript
Array.isArray([]); // => true
Array.isArray({}); // => false
```

## Strings As Arrays

Instead of accessing individual characters with the charAt() method, you can use square brackets:

```javascript
var s = test; // => "t" s[1]
s.charAt(0); // => "e"
```

The fact that strings behave like arrays also means, however, that we can apply generic array methods to them. For example:

```javascript
s = "JavaScript";
Array.prototype.join.call(s, " "); // => "J a v a S c r i p t"
```

Keep in mind that strings are immutable values, so when they are treated as arrays, they are read-only arrays. Array methods like `push()`, `sort()`, `reverse()`, and `splice()` modify an array in place and do not work on strings. Attempting to modify a string using an array method does not, however, cause an error: it simply fails silently.
