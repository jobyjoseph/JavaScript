JavaScript’s fundamental datatype is the _object_. An object is an unordered collection of _properties_, each of which has a name and a value. Property names are strings, so we can say that objects map strings to values.

## Creating Objects

### Object Literals
An _object literal_ is a comma-separated list of colon-separated name:value pairs, en- closed within curly braces. A property name is a JavaScript identifier or a string literal (the empty string is allowed). A property value is any JavaScript expression; the value of the expression (it may be a primitive value or an object value) becomes the value of the property. Here are some examples:
```javascript
var empty = {};                             // An object with no properties
var point = { x:0, y:0 };                   // Two properties
var point2 = { x:point.x, y:point.y+1 };    // More complex values
var book = {
    "main title": "JavaScript",             // Property names include spaces,
    'sub-title': "The Definitive Guide",    // and hyphens, so use string literals
    "for": "all audiences",                 // for is a reserved word, so quote
    author: {                               // The value of this property is
        firstname: "David",                 // itself an object. Note that
        surname: "Flanagan"                 // these property names are unquoted.
    }
};
```

In ECMAScript 5 (and some ECMAScript 3 implementations), reserved words may be used as property names without quoting. In general, however, property names that are reserved words must be quoted in ECMAScript 3. In ECMAScript 5, a trailing comma following the last property in an object literal is ignored. Trailing commas are ignored in most ECMAScript 3 implementations, but IE considers them an error.

### Creating Objects with `new`
The new operator creates and initializes a new object. The `new` keyword must be followed by a function invocation. A function used in this way is called a constructor and serves to initialize a newly created object.

