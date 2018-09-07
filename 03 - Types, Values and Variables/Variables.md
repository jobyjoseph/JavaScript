When we need to store a value for future use, we use _variables_.

## Variable Declaration

Before you use a variable in a JavaScript program, you should declare it. Variables can be declared with `var`, `let` or `const` keyword. `var` creates a function scoped variable. `let` creates block scoped variables. `const` creates constant variables whose values cannot be changed. `let` and `const` were introduced in ES6.

```javascript
var name;
let age;
const DOB = "06/11/85";
```

We can combine variable declaration and initialization.

```javascript
var name = "Joby";
let age = 32;
const DOB = "06/11/85";
```

It is mandatory to assign the variable if we are using `const`. If we try to just declare a constant variable, it throws _Syntax Error_. The type of a variable in JavaScript is decided by the type of value it stores.

```javascript
const A; // Uncaught SyntaxError: Missing initializer in const declaration
```

### Default value of variable

Default value of a declared variable is `undefined` in case of `var` and `let`. This does not apply for `const` as constant variables needs to be initialized along with declaration.

```javascript
var a;
let b;
a; // undefined
b; // undefined
```

### Redeclaration of variables

If we try to redeclare a variable declared using `var`, JavaScript does NOT throw any error.

```javascript
var a;
var a; // Its fine
```

If we try to redeclare a variable declared using `let` or `const`, JavaScript throws error.

```javascript
let b;
let b; // Uncaught SyntaxError: Identifier 'b' has already been declared
const c = 1;
const c = 2; // Uncaught SyntaxError: Identifier 'c' has already been declared
```

### Working with undeclared variables

If we try to assign a value to an undeclared variable, it does not throw any error.
