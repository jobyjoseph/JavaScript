JavaScript’s fundamental datatype is the _object_. An object is an unordered collection of _properties_, each of which has a name and a value. Property names are strings, so we can say that objects map strings to values.

## Creating Objects

### Object Literals

An _object literal_ is a comma-separated list of colon-separated name:value pairs, en- closed within curly braces. A property name is a JavaScript identifier or a string literal (the empty string is allowed). A property value is any JavaScript expression; the value of the expression (it may be a primitive value or an object value) becomes the value of the property. Here are some examples:

```javascript
var empty = {}; // An object with no properties
var point = { x: 0, y: 0 }; // Two properties
var point2 = { x: point.x, y: point.y + 1 }; // More complex values
var book = {
  "main title": "JavaScript", // Property names include spaces,
  "sub-title": "The Definitive Guide", // and hyphens, so use string literals
  for: "all audiences", // for is a reserved word, so quote
  author: {
    // The value of this property is
    firstname: "David", // itself an object. Note that
    surname: "Flanagan" // these property names are unquoted.
  }
};
```

In ECMAScript 5 (and some ECMAScript 3 implementations), reserved words may be used as property names without quoting. In general, however, property names that are reserved words must be quoted in ECMAScript 3. In ECMAScript 5, a trailing comma following the last property in an object literal is ignored. Trailing commas are ignored in most ECMAScript 3 implementations, but IE considers them an error.

### Creating Objects with `new`

The new operator creates and initializes a new object. The `new` keyword must be followed by a function invocation. A function used in this way is called a constructor and serves to initialize a newly created object.

### Object.create()

ECMAScript 5 defines a method, `Object.create()`, that creates a new object, using its first argument as the prototype of that object. `Object.create()` also takes an optional second argument that describes the properties of the new object.

If you want to create an ordinary empty object (like the object returned by {} or new Object()), pass Object.prototype:

```javascript
var o3 = Object.create(Object.prototype); // o3 is like {} or new Object().
```

## Prototypes

Every JavaScript object has a second JavaScript object (or `null`, but this is rare) associated with it. This second object is known as a prototype, and the first object inherits properties from the prototype.

All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as `Object.prototype`. Objects created using the `new` keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. So the object created by `new Object()` inherits from `Object.prototype` just as the object created by `{}` does. Similarly, the object created by `new Array()` uses `Array.prototype` as its prototype, and the object created by `new Date()` uses `Date.prototype` as its prototype.

`Object.prototype` is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype.

## Querying and Setting Properties

To obtain the value of a property, use the dot (.) or square bracket ([]) operators. If using the dot operator, the right-hand must be a simple identifier that names the property. If using square brackets, the value within the brackets must be an expression that evaluates to a string that contains the desired property name.

```javascript
var author = book.author; // Get the "author" property of the book.
var name = author.surname; // Get the "surname" property of the author.
var title = book["main title"]; // Get the "main title" property of the book.
```

In ECMAScript 3, the identifier that follows the dot operator cannot be a reserved word: you cannot write `o.for` or `o.class`. If an object has properties whose name is a reserved word, you must use square bracket notation to access them: `o["for"]` and `o["class"]`. ECMAScript 5 relaxes this restriction (as do some implementations of ECMAScript 3) and allows reserved words to follow the dot.

When using square bracket notation, the expression inside the square brackets must evaluate to a string or a value that can be converted to a string.
