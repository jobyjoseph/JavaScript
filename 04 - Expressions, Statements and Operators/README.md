An _expression_ is a phrase of JavaScript that evaluates to a value.

## Variable as expression

A variable in JavaScript is a primary expression. Primary expressions can stand alone, in other words they do not include any simpler expressions. When any _identifier_ appears by itself in a program, JavaScript assumes it is a _variable_ and looks up its value. An attempt to evaluate a nonexistent variable throws a _ReferenceError_ instead.

```javascript
// Evaluating undeclared, uninitialized variable
console.log(a); // Uncaught ReferenceError: a is not defined
```

## Sparse Arrays

In an array literal, elements can be skipped by simply inserting commas(,)

```javascript
const a = [2, , , 8];
console.log(a); // [2, emptyx2, 8]
```

Note that _empty_ does not mean `undefined`. It means `a` is a _sparse_ array. In a sparse array, the index of elements is not continous.
