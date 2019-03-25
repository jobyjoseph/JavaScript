## Arrow function is compact
Do both the code snippets below log the same output in console?
```
const sum = function(a, b) {
  return a + b;
}
console.log(sum(2, 3));
```
and
```
const sum = (a, b) => a + b;
console.log(sum(2, 3));
```
Yes. Both the snippets logs same output. Arrow functions are syntactically compact alternative to function expressions.

## Arrow function returning empty object
Can you find any mistake in below code? I am trying to return an empty object from an arrow function.
```
const f = () => {};
```
Even though above line is syntactically correct, it will return `undefined`. It treats the `{}` as body of function. If we need to return an empty object, wrap `{}` with `()`. Here is the updated code.
```
const f = () => ({});
```
