Lexical structure is a set of basic rules that tell how to write a program.

## Character Set

JavaScript programs are written using the _Unicode_ character set. Unicode is a superset of ASCII and Latin-1 and supports virtually every written language currently used on the planet.

```javascript
// Print unicode
console.log("\u0D1C\u0D4B\u0D2C\u0D3F"); // "ജോബി" My name in malayalam language

// Use unicode as object property
const obj = {
  ജോബി: "Ernakulam" // ജോബി: "Ernakulam"
};
```

### Case Sensitivity

JavaScript is a case-sensitive language. Which means variable `name` and `Name` are different.

### Comments

JavaScript supports two styles of comments.

```javascript
// This is an inline comment

/* This is a 
   multi-line comment */
```

### Identifiers

In JavaScript, identifiers are used to name variables and functions. It is just a name. The name should follow certain rules:

- Can contain only letters, digits, underscore (\_), or dollar sign ($)
- First character cannot be a digit

```javascript
// Legal identifiers
a;
_;
$;
a1;
_name;
$div;
ജോബി; // non english
```

JavaScript reserves a number of identifiers as the keywords of the language itself. You cannot use these words as identifiers in your programs.

## Separator(;)

JavaScript uses the semicolon (;) to separate statements from each other. You can omit semicolon between two statements if they are written in separate lines. There are exceptions:

### `return`, `break` and `continue`

These 3 statements can be used alone or followed by an identifier or expression. If a line break appears after any of these keywords, JavaScript will always treat that line break as semicolon.

```javascript
return;
true; // is return; true; for JavaScript
```

### `++` and `--` operators

This code:

```javascript
x;
++y;
```

is treated as `x; ++y;`, not `x++;, y;`
