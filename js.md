# JavaScript interview questions

## 1. What is Javascript? What is the role of Javascript engine?

Javascript is a programming language that is used to make web pages dynamic and interactive.

Javascript engine is a program that executes the javascript code (V8 in Chrome and Node.js, SpiderMonkey in Firefox, JavascriptCore in Safari...)

## 2. What are Client side and Server side?

Client side is the part of the code that runs on the user's computer. Server side is executed on the server.

## 3. What is the difference var, let, const?

- `var` create a function-scoped variable.
- `let` create a block-scoped variable.
- `const` create a block-scoped variable that cannot be reassigned.

## 4. What are data types in Javascript?

- Primitive:
  - `string`: A sequence of characters.
  - `number`: A sequence of numbers.
  - `boolean`: A sequence of true or false values.
  - `null`: A special value that represents an empty value, it's type is object.
  - `undefined`: A special value that represents an uninitialized variable.
- Non-primitive:
  - `object`: A sequence of key-value pairs.
  - `array`: A sequence of values.s
  - `function`: A sequence of instructions that perform a specific task.

## 5. What are opeartors in Javascript?

- Arithmetic operators:
  - `+`: Addition.
  - `-`: Subtraction.
  - `*`: Multiplication.
  - `/`: Division.
  - `%`: Modulus.
- Asignment operators:
  - `=`: Assignment.
  - `+=`: Addition and assignment.
- Comparison operators:
  - `>`: Greater than.
  - `<`: Less than.
  - `>=`: Greater than or equal to.
  - `<=`: Less than or equal to.
  - `==`: Equal to.
  - `===`: Equal to, including type.
  - `!==`: Not equal to, including type.
- Logical operators:
  - `&&`: And.
  - `||`: Or.
  - `?`: Ternary operator.
  - `!`: Negation.
- String operators:
  - `+`: Concatenation.

## 6. What are the different types of conditions statements in Javascript?

- `if/else`: If-else statement.
- `switch`: Switch statement.
- `? :`: Ternary operator.

## 8. What are the types of loops in Javascript?

- `for`: For loop.
- `while`: While loop.
- `do/while`: Do/while loop.
- `for..in`: For/in loop.
- `for..of`: For/of loop.

## 9. What is DOM?

DOM (Docuemnt Object Model) is the tree like represeantation of the web page.

## 10. What are the types of functions is Javascript?

- Named: function name() {}
- Anonymous: function() {}
- Arrow: () => {}
- IIFE: (() => {})()

## 11. What is Scope?

- Global
- Function
- Local (block-scope)

```js
let globalVariable = 'global';
someFunction();
function someFunction() {
  let functionVariable = 'functicon';
  if (true) {
    let localVariable = 'local';
    console.log(globalVariable);
    console.log(functionVariable);
    console.log(localVariable);
  }
}
console.log(globalVariable);
```

## 12. What is Hoisting?

Hoisting is the process of moving `var` and `function` declarations to the top of their scope.

## 13. What is the difference between primitive and non-primitive data types?

- Primitive
  - They can only hold a single value
  - They are immutable: meaning their value once assigned, cannot be changed (When you assign a new value to a primitive, it creates a new variable with the new value)
- Non-primitive:
  - Can hold multiple values
  - They are mutable

## 14. What is type coercion?

Type coercion is the process of converting a value from one data type to another during certain operations or comparison.

- String coercion: When a string is concatenated with non-string values, the result is a string.
- Number coercion: JS will try string/boolean to number conversion when performing mathematical operations (+, -, \*, /, %, \*\*)
- Boolean coercion: When a boolean is converted to a number, it will be 1 or 0.

## 15. What is short-ciruit evaluation in Javascript?

```js
// with AND
const result = 'hello' && 'world';

// wiht OR
const result = 1 + 2 || 3;
```

## 16. What is the difference between == and ===?

- `==`: Compare two values after performing type coersion.
- `===`: Compare two values without performing type coersion.

## 17. What is the difference between Spread and Rest?

- Spread: is used to expand an array or object into individual elements.
  - Copying: [...array], {...object}
  - Merging: [...array1, ...array2], {...object1, ...object2}
  - Passing arguments: function(...args) {}
- Rest: is used in functions to collect multiple arguments into an array.
  - function(a, b, c, ...restArgs) {}

## 18. What is Array/Object desctructuring?

Desctructuring is exctracting values from an array or object, it was introduced in ES6.

```js
const [a, b, c] = [1, 2, 3];
const { d, e, f } = { d: 1, e: 2, f: 3 };
```

## 19. What are array-like objects?

Array-like objects are objects that have indexed elemetns and length properties but they may not have all the methods of an array.

- Arguments keyword: function f() { console.log(arguments) }
- Strings: str.length
- HTML collections: const elements = document.getElementsByTagName('p');

## 20. What is a HOF?

A Higher-order function is a function that takes one or more functions are arugments and returns a function as a result.

## 21. What is the difference between a arguments and a parameters?

- Arguements: are the placeholders defined in the function declaration.
- Parameters: are the actual values passed to the function.

## 22. What are First-class functions?

A progrmaming language is said to have First-class functions if it treats functions as other varibles.

```js
// Assign a function to a variable
const f0 = function () {
  console.log('Hello');
};

// Passing a function as an argument
function f1(g) {
  g();
}

// Returning a function from a function
function f2() {
  return function () {
    console.log('Hello');
  };
}
```

## 23. What is function currying?

Currying is a technique in which a function with multiple arguments into a series of functions that each accept a single argument.

```js
function multiply(a, b) {
  return a * b;
}

function curriedMultiply(a) {
  return function (b) {
    return a * b;
  };
}

const double = curriedMultiply(2);
const triple = curriedMultiply(3);
```

## 24. What are call, apply, bind?

- `call`: The call method is used to call a function with a given this value and arguments provided individually.
- `apply`: Same as call, but the arguments are provided as an array.
- `bind`: The bind method is used to create a new function with a given this value.

```js
const user = { name: 'John' };
function sayHello(message) {
  console.log(message + ' ' + this.name);
}

sayHello.call(user, 'Hello'); // Hello John
sayHello.apply(user, ['Hello']); // Hello John
const sayHelloBound = sayHello.bind(user);
sayHelloBound('Hello'); // Hello John
```

## 25. What are Pure and Impure functions?

- Pure functions are functions that always produce the same output given the same input.
- Impure functions return different output, may modify the state, or have side effects.

```js
// Pure function
function add(a, b) {
  return a + b;
}

// Impure function
let total = 0;
function addToTotal(num) {
  total += num;
  return total;
}
```

## 26. What is the Set Object?

A Set is a collection of unique values.

```js
const mySet = new Set([1, 2, 3, 4, 5, 5, 5]);
mySet.add(6);
mySet.delete(2);
console.log(mySet.has(5)); // true
console.log(mySet.size); // 5
console.log(mySet.values()); // [1, 3, 4, 5, 6]

// Remove duplicates from an array
const arr = [1, 2, 3, 4, 5, 5, 5];
const uniqueArr = [...new Set(arr)];
console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

## 27. What is the Map Object?

Map is a collection of key-value pairs, where the keys can be of any type (objects, strings, functions, etc.). Map maintains the order of the key-value pairs as they are added.

```js
const myMap = new Map([
  ['name', 'John'],
  ['age', 25],
  ['city', 'New York'],
]);
myMap.set('country', 'USA');
console.log(myMap.get('name')); // John
console.log(myMap.has('country')); // true
console.log(myMap.size); // 4
console.log(myMap.values()); // [ 'John', 25, 'New York', 'USA' ]
console.log(myMap.keys()); // [ 'name', 'age', 'city', 'country' ]
console.log(myMap.entries()); // [ [ 'name', 'John' ], [  'age', 25  ], [  'city',  'New York'  ],  [  'country',  'USA'  ]
```

## 28. What is Event Capturing and Event Bubbling?

- Event Capturing: When an event occurs on an element it is first captured by the highest element in the DOM tree and moving down to the target element.
- Event Bubbling: Is the opposite of event capturing.

```js
// Even Bubbling: (Default)
div.addEventListener('click', handleClick);

// Event Capturing
div.addEventListener('click', handleClick, true);
```

## 29. What is Lexical scoping?

The concept of Lexical scoping ensures that variables decalred in an outer scope are accesible in nested fucntions.

## 30. What is Closure?

Closure is a combination of a function and the lexical environment it was declared in.

benefits:

- Data modification with data privacy(encapsulation)
- Persistent data and state
- Code reusability

```js
function outerFunction() {
  let outerVariable = 'Outer Variable';
  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

const closureFunction = outerFunction();
closureFunction(); // 'Outer Variable'
```

## 31. What are the techniques for achieving Asynchronous opperations in Javascript?

### 31.1. setTimeout and setInterval

setTimeout and setInterval are used to schedule a function to be called after a delay.

### 31.2. Promises

A promise represent a value in the future. Promises can be in three states:

- Pending: Initial state.
- Resolved: Success state.
- Rejected: Failure state.

```js
const promise = new Promise((resolve, reject) => {
    // do some async work
    if (/* condition */) {
        resolve('Success');
    } else {
        reject('Failure');
    }
});

```

### 31.3. Async/Await

Async/Await use promises to handle asynchronous operation but with try/catch instea of then/catch.

```js
async function asyncFunction() {
  try {
    const result = await promise;
    // do something with result
  } catch (error) {
    // handle error
  }
}
```
