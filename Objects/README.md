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

## Querying and Setting Properties

To obtain the value of a property, use the dot (.) or square bracket ([]) operators. If using the dot operator, the right-hand must be a simple identifier that names the property. If using square brackets, the value within the brackets must be an expression that evaluates to a string that contains the desired property name.

```javascript
var author = book.author; // Get the "author" property of the book.
var name = author.surname; // Get the "surname" property of the author.
var title = book["main title"]; // Get the "main title" property of the book.
```

In ECMAScript 3, the identifier that follows the dot operator cannot be a reserved word: you cannot write `o.for` or `o.class`. If an object has properties whose name is a reserved word, you must use square bracket notation to access them: `o["for"]` and `o["class"]`. ECMAScript 5 relaxes this restriction (as do some implementations of ECMAScript 3) and allows reserved words to follow the dot.

When using square bracket notation, the expression inside the square brackets must evaluate to a string or a value that can be converted to a string.

## Prototypes

Every JavaScript object has a second JavaScript object (or `null`, but this is rare) associated with it. This second object is known as a prototype, and the first object inherits properties from the prototype.

All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as `Object.prototype`. Objects created using the `new` keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. So the object created by `new Object()` inherits from `Object.prototype` just as the object created by `{}` does. Similarly, the object created by `new Array()` uses `Array.prototype` as its prototype, and the object created by `new Date()` uses `Date.prototype` as its prototype.

`Object.prototype` is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype.

## Inheritance

JavaScript objects have a set of “own properties,” and they also inherit a set of properties from their prototype object.

Suppose you query the property `x` in the object `o`. If `o` does not have an own property with that name, the prototype object of `o` is queried for the property `x`.

## Deleting properties

The `delete` operator removes a property from an object. Its single operand should be a property access expression. Surprisingly, delete does not operate on the value of the property but on the property itself:

```javascript
delete book.author; // The book object now has no author property.
delete book["main title"]; // Now it doesn't have "main title", either.
```

The `delete` operator only deletes own properties, not inherited ones.

A `delete` expression evaluates to true if the delete succeeded or if the delete had no effect (such as deleting a nonexistent property). `delete` also evaluates to true when used (meaninglessly) with an expression that is not a property access expression:

```javascript
o = { x: 1 }; // o has own property x and inherits property toString
delete o.x; // Delete x, and return true
delete o.x; // Do nothing (x doesn't exist), and return true
delete o.toString; // Do nothing (toString isn't an own property), return true
delete 1; // Nonsense, but evaluates to true
```

`delete` does not remove properties that have a configurable attribute of `false`.

## Testing Properties

To check whether an object has a property with a given name, we can use:

- `in` operator
- `hasOwnProperty()`
- `propertyIsEnumerable()`
- simply query the object

### `in` operator

The `in` operator expects a property name (as a string) on its left side and an object on its right. It returns `true` if the object has an own property or an inherited property by that name:

```javascript
var o = { x: 1 };
"x" in o; // true: o has an own property "x"
"y" in o; // false: o doesn't have a property "y"
"toString" in o; // true: o inherits a toString property
```

### `hasOwnProperty()`

The hasOwnProperty() method of an object tests whether that object has an own property with the given name. It returns `false` for inherited properties:

```javascript
var o = { x: 1 };
o.hasOwnProperty("x"); // true: o has an own property x
o.hasOwnProperty("y"); // false: o doesn't have a property y
o.hasOwnProperty("toString"); // false: toString is an inherited property
```

### `propertyIsEnumerable()`

`propertyIsEnumerable()` returns `true` only if the named property is an own property and its _enumerable_ attribute is `true`. Certain built-in properties are not enumerable. Properties created by normal JavaScript code are enumerable unless you’ve used one of the ECMAScript 5 methods shown later to make them nonenumerable.

```javascript
var o = inherit({ y: 2 });
o.x = 1;
o.propertyIsEnumerable("x"); // true: o has an own enumerable property x
o.propertyIsEnumerable("y"); // false: y is inherited, not own
Object.prototype.propertyIsEnumerable("toString"); // false: not enumerable
```

### Query the Property

It is often sufficient to simply query the property and use `!==` to make sure it is not `undefined`.

## Enumerating Properties

`for/in` loop runs the body of the loop once for each enumerable property (own or inherited) of the specified object, assigning the name of the property to the loop variable.

```javascript
var o = { x: 1, y: 2, z: 3 };
for (p in o) console.log(p); // Prints x, y, and z, but not toString
```

In addition to the `for/in` loop, ECMAScript 5 defines two functions that enumerate property names. The first is `Object.keys()`, which returns an array of the names of the enumerable own properties of an object.

The second ECMAScript 5 property enumeration function is `Object.getOwnPropertyNames()`. It works like `Object.keys()` but returns the names of all the own properties of the specified object, not just the enumerable properties. There is no way to write this function in ECMAScript 3, because ECMAScript 3 does not provide a way to obtain the nonenumerable properties of an object.
