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

Functions that can accept any number of arguments are called _variadic functions_, _variable arity functions_, or _varargs_ functions.

The Arguments object has one very unusual feature. In _non-strict_ mode, when a function has named parameters, the array elements of the Arguments object are aliases for the parameters that hold the function arguments. The numbered elements of the Arguments object and the parameter names are like two different names for the same variable. Changing the value of an argument with an argument name changes the value that is retrieved through the `arguments[]` array. Conversely, changing the value of an argument through the `arguments[]` array changes the value that is retrieved by the argument name. Here is an example that clarifies this:

```javascript
function f(x) {
  console.log(x); // Displays the initial value of the argument
  arguments[0] = null; // Changing the array element also changes x!
  console.log(x); // Now displays "null"
}
```

This special behavior of the Arguments object has been removed in the _strict_ mode of ECMAScript 5. There are other strict-mode differences as well. In non-strict functions, `arguments` is just an identifier. In _strict_ mode, it is effectively a reserved word. Strict mode functions cannot use arguments as a parameter name or as a local variable name, and they cannot assign values to arguments.

## Functions As Namespaces

It is sometimes useful to define a function simply to act as a temporary namespace in which you can define variables without polluting the global namespace.

```javascript
(function() {
  // Module code goes here.
})();
```

The open parenthesis before function is required because without it, the JavaScript interpreter tries to parse the function keyword as a function declaration statement. With the parenthesis, the interpreter correctly recognizes this as a function definition expression. It is idiomatic to use the parentheses, even when they are not required, around a function that is to be invoked immediately after being defined.

## Closures

Like most modern programming languages, JavaScript uses lexical scoping. This means that functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked. In order to implement lexical scoping, the internal state of a JavaScript function object must include not only the code of the function but also a reference to the current scope chain. This combination of a function object and a scope (a set of variable bindings) in which the function’s variables are resolved is called a closure in the computer science literature.

Technically, all JavaScript functions are closures: they are objects, and they have a scope chain associated with them. Most functions are invoked using the same scope chain that was in effect when the function was defined, and it doesn’t really matter that there is a closure involved. Closures become interesting when they are invoked under a different scope chain than the one that was in effect when they were defined. This happens most commonly when a nested function object is returned from the function within which it was defined.

The first step to understanding closures is to review the lexical scoping rules for nested functions.

```javascript
var scope = "global scope"; // A global variable
function checkscope() {
  var scope = "local scope"; // A local variable
  function f() {
    return scope; // Return the value in scope here
  }
  return f();
}
checkscope(); // => "local scope"
```

Now let’s change the code just slightly.

```javascript
var scope = "global scope";
function checkscope() {
  var scope = "local scope";
  function f() {
    return scope;
  }
  return f;
}
checkscope()();
```

In this code, a pair of parentheses has moved from inside checkscope() to outside of it. Instead of invoking the nested function and returning its result, checkscope() now just returns the nested function object itself.

Remember the fundamental rule of lexical scoping: JavaScript functions are executed using the scope chain that was in effect when they were defined. The nested function `f()` was defined under a scope chain in which the variable scope was bound to the value _local scope_. That binding is still in effect when `f` is executed, wherever it is executed from. So the last line of code above returns `local scope`, not `global scope`. This, in a nutshell, is the surprising and powerful nature of closures: they capture the local variable (and parameter) bindings of the outer function within which they are defined.

## Function Properties, Methods, and Constructor

### The `length` Property
The `length` property of a function returns the arity of the function—the number of parameters it declares in its parameter list, which is usually the number of arguments that the function expects.

### The `prototype` Property
Every function has a prototype property that refers to an object known as the _prototype object_. Every function has a different prototype object. When a function is used as a constructor, the newly created object inherits properties from the prototype object.

### The `call()` and `apply()` Methods
`call()` and `apply()` allow you to indirectly invoke a function as if it were a method of some other object. The first argument to both `call()` and `apply()` is the object on which the function is to be invoked; this argument is the invocation context and becomes the value of the `this` keyword within the body of the function. To invoke the function f() as a method of the object `o` (passing no arguments), you could use either `call()` or `apply()`:
```javascript
f.call(o); 
f.apply(o);
```
In ECMAScript 5 strict mode the first argument to `call()` or `apply()` becomes the value of `this`, even if it is a primitive value or `null` or `undefined`. In ECMAScript 3 and non-strict mode, a value of `null` or `undefined` is replaced with the global object and a primitive value is replaced with the corresponding wrapper object.

### The `bind()` method
The `bind()` method was added in ECMAScript 5, but it is easy to simulate in ECMAScript 3. As its name implies, the primary purpose of `bind()` is to bind a function to an object. When you invoke the `bind()` method on a function `f` and pass an object `o`, the method returns a new function. Invoking the new function (as a function) invokes the original function `f` as a method of `o`. Any arguments you pass to the new function are passed to the original function. For example:
```javascript
function f(y) { return this.x + y; }  // This function needs to be bound
var o = { x : 1 };                    // An object we'll bind to
var g = f.bind(o);                    // Calling g(x) invokes o.f(x)
g(2)                                  // => 3
```
The ECMAScript 5 `bind()` method does more than just bind a function to an object. It also performs partial application: any arguments you pass to `bind()` after the first are bound along with the this value. Partial application is a common technique in functional programming and is sometimes called _currying_. 