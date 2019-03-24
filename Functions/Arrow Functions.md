## Arrow Function returning empty object
Can you find any mistake in below code? I am trying to return an empty object from an arrow function.
```
const f = () => {};
```
Even though above line is syntactically correct, it will return `undefined`. It treats the `{}` as body of function. If we need to return an empty object, wrap `{}` with `()`. Here is the updated code.
```
const f = () => ({});
```
