## Reverse String
Write the definition for `reverse()` function which accepts a string and return a new string with the reversed order of characters. Example:
```javascript
reverse('apple')        //'leppa'
reverse('hello')        //'olleh'
reverse('Greetings!')   //'!sgniteerG'
```
#### Solution 1
```javascript
function reverse(str) {
    return str.split('').reverse().join('');
}
```

#### Solution 2
```javascript
function reverse(str) {
    var reversedString = '';
    for(let character of str) {
        reversedString = character + reversedString
    }
    return reversedString;
}
```
`for..of` was introduced in ES6 to loop over iterable objects, including: built-in String, Array, Array-like objects (e.g., arguments or NodeList), TypedArray, Map, Set, and user-defined iterables.

#### Solution 3
```javascript
function reverse(str) {
    return str.split('').reduce((reversed, character) => character + reversed, '')
}
```

## Palindrome
Write a function which returns true if input string is a palindrome, or else return false. Palindromes are strings that form the same word if it is reversed. _akka_, _malayalam_ are examples of palindrome.

#### Solution 1
```javascript
function palindrome(str) {
    return str.split('').reverse().join('') === str
}
```

### Solution 2
```javascript
function palindrome(str) {
    return str.split('').every(function(character){
        return character === str[str.length - 1]
    });
}
```
`every()` returns true if for all the elements the callback function returns true.