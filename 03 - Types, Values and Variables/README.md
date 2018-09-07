The kinds of values that can be represented and manipulated in a programming language are known as _types_, and one of the most fundamental characteristics of a programming language is the set of types it supports.

JavaScript types can be divided into two categories:

- primitive types
- object types

### Primitive Types

Primitive types include:

- number
- string
- boolean

### object Type

Any JavaScript value that is not a number, a string, a boolean, or `null` or `undefined` is an object.

## Number

All numbers in JavaScript are represented as 64 bit floating-point values. When a number appears directly in a JavaScript program, it’s called a _numeric literal_.

```javascript
// Eg: Numeric literals
2;
3.14;
```

Any numeric literal can be preceded by a minus sign (-) to make the number negative.

## String

strings are used for representing text.

### String Literals

To include a string literally in a JavaScript program, simply enclose the characters of the string within a matched pair of single or double quotes (' or "). Double-quote characters may be contained within strings delimited by single-quote characters, and single-quote characters may be contained within strings delimited by double quotes.

```javascript
// Eg: string literals
""; // Empty string
"false";
"1000";
'"Batman" returns';
"'Batman' returns";
'That\'s ok'; // Escaping string
```

## Boolean

There are only two possible values in this type, `true` and `false`. Boolean values are generally the result of comparisons you make in your JavaScript programs.

Any JavaScript value can be converted to a boolean value. Thefollowing values convert to, and therefore work like, `false`:

```javascript
undefined;
null;
0 - 0;
NaN;
(""); // the empty string
```

## `null`

`null` is a special value in JavaScript which belongs to its own type.

## `undefined`

`undefined` is also a special value in JavaScript, just like `null`. All variables in JavaScript which are not initialized will be having the value `undefined`. Trying to read the value of a non-existent property of an object or array returns `undefined`. Functions that have no return value, by default returns `undefined`. If you apply the `typeof` operator to the undefined value, it returns _“undefined”_.

Using . or [] to access a property or method of these values causes a _TypeError_.
