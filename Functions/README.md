A _function_ is a block of JavaScript code that is defined once but may be executed, or invoked, any number of times.

## Defining Functions

Functions are defined with the `function` keyword, which can be used in a function definition expression or in a function declaration statement.

```javascript
// Function declaration statement
function sum(a, b) {
  return a + b;
}

// Function definition expression
var sum = function(a, b) {
  return a + b;
};
```

The function name is a required part of _function declaration statements_: it is used as the name of a variable, and the newly defined function object is assigned to the variable. For function definition expressions, the name is optional: if present, the name refers to the function object only within the body of the function itself.

Function declaration statements are _hoisted_ to the top of the enclosing script or the enclosing function, so that functions declared in this way may be invoked from code that appears before they are defined. This is not true for functions defined as expressions, however: in order to invoke a function, you must be able to refer to it, and you can’t refer to a function defined as an expression until it is assigned to a variable. Variable declarations are hoisted, but assignments to those variables are not hoisted, so functions defined with expressions cannot be invoked before they are defined.

The `return` statement causes the function to stop executing and to return the value of its expression (if any) to the caller. If the `return` statement does not have an associated expression, it returns the undefined value. If a function does not contain a `return` statement, it simply executes each statement in the function body and returns the undefined value to the caller.

## Invoking Functions

JavaScript functions can be invoked in four ways:

- as functions
- as methods
- as constructors
- indirectly through their call() and apply() methods

### Function Invocation

Functions are invoked with an invocation expression.

```javascript
// Function invocation example
sum(2, 3);
```

For function invocation in ECMAScript 3 and nonstrict ECMAScript 5, the invocation context (the `this` value) is the global object. In _strict mode_, however, the invocation context is `undefined`.

Functions written to be invoked as functions do not typically use the this keyword at all. It can be used, however, to determine whether strict mode is in effect:

```javascript
// Define and invoke a function to determine if we're in strict mode.
var strict = (function() {
  return !this;
})();
```

### Method Invocation

A method is nothing more than a JavaScript function that is stored in a property of an object.

```javascript
// Method invocation example
obj.show();
```

Method invocations differ from function invocations in one important way, however: the invocation context. Property access expressions consist of two parts: an object (in this case o) and a property name (m). In a method invocation expression like this, the object o becomes the invocation context, and the function body can refer to that object by using the keyword this. Here is a concrete example:

```javascript
var calculator = {
  // An object literal
  operand1: 1,
  operand2: 1,
  add: function() {
    // Note the use of the this keyword to refer to this object.
    this.result = this.operand1 + this.operand2;
  }
};
calculator.add(); // A method invocation to compute 1+1.
calculator.result; // => 2
```

Note that `this` is a keyword, not a variable or property name. JavaScript syntax does not allow you to assign a value to `this`. Unlike variables, the `this` keyword does not have a scope, and nested functions do not inherit the `this` value of their caller.

### Constructor Invocation

If a function or method invocation is preceded by the keyword `new`, then it is a constructor invocation. If a constructor has no parameters, then JavaScript constructor invocation syntax allows the argument list and parentheses to be omitted entirely.

```javascript
// Both statements are same
var o = new Object();
var o = new Object();
```

A constructor invocation creates a new, empty object that inherits from the prototype property of the constructor. Constructor functions are intended to initialize objects and this newly created object is used as the invocation context, so the constructor function can refer to it with the `this` keyword. Note that the new object is used as the invocation context even if the constructor invocation looks like a method invocation. That is, in the expression `new o.m()`, `o` is not used as the invocation context.

Constructor functions do not normally use the `return` keyword. They typically initialize the new object and then return implicitly when they reach the end of their body. In this case, the new object is the value of the constructor invocation expression. If, however, a constructor explicitly used the `return` statement to return an object, then that object becomes the value of the invocation expression. If the constructor uses `return` with no value, or if it returns a primitive value, that return value is ignored and the new object is used as the value of the invocation.

### Indirect Invocation

JavaScript functions are objects and like all JavaScript objects, they have methods. Two of these methods, `call()` and `apply()`, invoke the function indirectly. Both methods allow you to explicitly specify the `this` value for the invocation, which means you can invoke any function as a method of any object, even if it is not actually a method of that object. Both methods also allow you to specify the arguments for the invocation. The `call()` method uses its own argument list as arguments to the function and the `apply()` method expects an array of values to be used as arguments.

## Function Arguments and Parameters

### Optional Parameters

When a function is invoked with fewer arguments than declared parameters, the additional parameters are set to the `undefined` value.

The programmer who calls your function cannot omit the first argument and pass the second: she would have to explicitly pass `undefined` the first argument.

### Variable-Length Argument Lists: The Arguments Object

Within the body of a function, the identifier `arguments` refers to the Arguments object for that invocation. The Arguments object is an array-like object that allows the argument values passed to the function to be retrieved by number, rather than by name.
