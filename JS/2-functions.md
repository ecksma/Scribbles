

Functions in JS
=======
>A function is a concrete implementation of an algorithm in a computer language. It is a "subprogram" that encapsulates a specific behavior.


**Declaration**

```javascript
  function foo() {
  }
```

####Benefits of Using Functions

* **Encapsulation** - Keeping code for the same purpose in the same place makes finding it and updating it easier.
* **Code Reuse** - "Don't Repeat Yourself" is a principle of coding - keep your programs **DRY**! Reusing code makes it easier to change how your program works, since you only have to make updates in one place. 

#### Scope

Scope represents the area of your program where a variable is defined. JavaScript has two scopes: **global scope** and **local scope**.

You can think of scope as a rule: *a new function introduces a new scope.*

```js
// global scope
var x = 1;

var changeNum = function (x) {
  // local scope
  x = 2;
}

changeNum(x);

console.log(x)
// logs what? (1)

```

####Some Functions to get the idea

> `getMax` function that finds the maximum number in an array
```javascript
var getMax = function(arr) {
  var max = 0;
  for (var i = 0; i < arr.length; i += 1) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
};

getMax([65, 234, 99, 0, 12, 450]);
```

> function that counts the number of times each letter occurs in a given string

```javascript
var letterCount = function(word) {
  // trim removes spaces
  var letters = word.toLowerCase().trim();
  var result = {};

  for (i = 0; i < letters.length; i += 1) {
    if (result[letters[i]]) {
      result[letters[i]] += 1;
    }
    else {
      result[letters[i]] = 1;
    }
  }
  return result;
};

var myWord = "BANANAS";
console.log(letterCount(myWord));
```

>function primes that will return an array of all prime numbers up to, but not exceeding a max number

```javascript
var isPrime = function(num) {
  if (num < 2) {
    return false;
  }
  for (var i = 2; i < num; i += 1) {
    if (num % i === 0) {
      return false;
    }
  }
  return true;
};

var primes = function(max) {
  for (var i = 2; i <= max; i += 1) {
    if (isPrime(i) === true) {
      console.log(i);
    }
  }
};

primes(100);
```
#### Further Reading

* [Functions - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
* [Functions - Eloquent JavaScript](http://eloquentjavascript.net/03_functions.html)
* [Demystifying JavaScript Variable Scope and Hoisting](http://www.sitepoint.com/demystifying-javascript-variable-scope-hoisting)