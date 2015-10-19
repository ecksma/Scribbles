

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