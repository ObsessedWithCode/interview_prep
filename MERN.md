# JavaScript

## Contents
- [Q. How do JS closure works?](#q-how-do-js-closure-works)
- [Q. What is Prototypal Inheritance in JS?](#q-what-is-prototypal-inheritance-in-js)

## Q. How do JS closure works?
A closure in JavaScript is a powerful feature that allows a function to access variables from an outer function's scope even after the outer function has finished executing. This is possible because functions in JavaScript form closures around the scope in which they were declared.
```
function outerFunction() {
    let outerVariable = 'I am outside!';

    function innerFunction() {
        console.log(outerVariable); // Accesses outerVariable from outerFunction's scope
    }

    return innerFunction;
}

const myClosure = outerFunction();
myClosure(); // Logs: 'I am outside!'
```
### Advantages
1. **Data Privacy/Encapsulate:** They allow functions to have private variables, data and logic.
2. **Maintaining State:** Closures can maintain state across multiple function calls.

## Q. What is Prototypal Inheritance in JS?
In Js, prototypal inheritance allows objects to inherit properties and methods from other objects. Instead of using classes(like in traditional OOP), Js uses a prototypal chain for inheritance.
### Advantages
**1. Memory Efficiancy:** Shared methods on the prototype save memory compared to having duplicate methods on each instance.
**2. Flexible Inheritance:** You can directly inherit from any object, not just classes.
```
let abc = {};
console.log(abc.toString()); // Outputs: "[object Object]"
```
In this case, abc is an object that inherits the toString() method from Object.prototype.
## Q. What is a promise? How does it differ from async/await?
A promise in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises provide a way to handle asynchronous operations more gracefully than traditional callback functions.
```
let myPromise = new Promise((resolve, reject) => {
    let success = true; // Simulating an operation

    if (success) {
        resolve("Operation was successful!");
    } else {
        reject("Operation failed.");
    }
});

myPromise.then(result => {
    console.log(result); // Logs: "Operation was successful!"
}).catch(error => {
    console.log(error);
});
```
**async/await** is a syntax that makes working with promises easier to read by providing a more synchronous-looking way to write asynchronous code, essentially acting as a cleaner way to chain promise operations together

```
async function executeAsyncFunction() {
    try {
        let result = await myAsyncFunction();
        console.log(result); // Logs: "Operation was successful!"
    } catch (error) {
        console.log(error);
    }
}
```
### Key differences between promises and async/await:
**Syntax:** async/await provides a more readable and synchronous-looking syntax for handling asynchronous operations compared to the chaining syntax of promises.
**Error Handling:** With async/await, you can use try...catch blocks for error handling, which is more intuitive than using .catch() with promises.
**Readability:** async/await makes the code easier to read and maintain, especially when dealing with multiple asynchronous operations.

##Q. How does this keyword work in different contexts in js?
The this keyword in JavaScript can be a bit tricky because its value depends on the context in which it is used. Here are some common contexts:
1. **Global Context:** refers to the global object, window in the case of browser.
2. **Function Context:** refers to the global object and undefined in strict mode.
3. **Arrow Function:** Do not have thier own this context, instead the refers to the outer lexical function/object, where the arrow function is defined. 
4. **Event Handlers:** this refers to the element that received the element. 

## Q. Debounce and Throttle
**Debounce** delays the execution of a function/api until a specific time is passed since the last call. 
Use case: Search input, resize window
**Throttle** ensures that a function is getting called at most once in a specific period. 
Use Cases: Updating elements as the users scrolls. Preventing multiple clicks of a button in a short time.
##Q. What is currying in JS?
**Currying** in JavaScript is a technique where a function takes multiple arguments one at a time, returning a new function for each argument until all arguments are provided.
Use Case: We can create a function with present configuration,  making your code more modular and reusable. e.g. logging.
```
function configureLogger(level) {
    return function(message) {
        console.log(`[${level}] ${message}`);
    };
}

const infoLogger = configureLogger('INFO');
infoLogger('This is an info message'); // Outputs: [INFO] This is an info message
```
## Q. Explain how closures can lead to memory leaks?
A **closure** is a function that retains access to its lexical scope, even when the function is getting executed outside that scope.
### How Closures Can Cause Memory Leaks
**1. Unintended Retention of Variables:** Closures can unintentionally retain references to variables in their outer scope, preventing those variables from being garbage collected.
```
function createClosure() {
    let largeArray = new Array(1000000).fill('data');
    return function() {
        console.log(largeArray.length);
    };
}

const closure = createClosure();
// largeArray is still in memory because the closure retains a reference to it
```
**Solution:** Explicitly set references to null when they are no longer needed.
function createClosure() {
    let largeArray = new Array(1000000).fill('data');
    return function() {
        console.log(largeArray.length);
        largeArray = null; // Helps in garbage collection
    };
}
**2. Event Listeners:**If closures are used within event listeners and the listeners are not properly removed, they can cause memory leaks by holding references to DOM elements.
**3. Timers and Intervals:**Closures used in setTimeout or setInterval can cause memory leaks if not cleared properly.
```
function startTimer() {
    let count = 0;
    const intervalId = setInterval(function() {
        console.log(count++);
    }, 1000);
    // If intervalId is not cleared, the closure retains the reference to count
}

startTimer();
```
**Solution:** Clear timers when they are no longer needed.
```
function startTimer() {
    let count = 0;
    const intervalId = setInterval(function() {
        console.log(count++);
    }, 1000);
    // Clear the interval when done
    setTimeout(() => clearInterval(intervalId), 5000);
}

startTimer();
```
## Q. What is garbage collection in js, and how does it work?
Garbage collection in JavaScript is the process of automatically freeing up memory that is no longer in use by the program. This helps prevent memory leaks and ensures efficient memory usage.
Javascript uses **mark-and-sweep** algorithm, phases are explained below.
**1. Mark Phase:** The garbage collector starts from the root and marks all reachable objects.
**2. Sweep Phase:** It removes objects that are not marked as reachable and reclaims their memory.
## Q. How can you prevent memory leaks in js?
1. Remove event listeners when no longer needed.
2. Avoid global variables.
3. Clear references when no longer needed.
4. Use closures carefully.
## Q. Explain the concept of function composition in js?
Combine multiple functions into one, where the outputof the one function becomes the input of the next.
###Benefits:
**Modularity:** Breaks complex tasks into simpler functions.
**Readability:** Makes code easier to understand.
**Maintainability:** Easier to test and maintain.
```
const compose = (...functions) => (initialValue) =>
    functions.reduceRight((value, func) => func(value), initialValue);

const add = (x) => x + 1;
const multiply = (x) => x * 2;

const composedFunction = compose(multiply, add);

console.log(composedFunction(5)); // Outputs 12
```
## Q. shallow clone vs deep clone?
### Shallow Copy
1. Copies only the top-level structure; nested objects are referebced, not duplicated.
2. Changes to nested elements in the original object, affect to the copy.
```
const original = { a: 1, b: { c: 2 } };
const shallowClone = { ...original }; // Object.assign({}, old_object) is also used to create shallow copy

shallowClone.b.c = 3;
console.log(original.b.c); // Outputs 3
```
### Deep Copy
1. Recursively copies all the elements and create a fully independent objects.
2. Changes to the original do not affect to the copy.
```
const original = { a: 1, b: { c: 2 } };
const deepClone = JSON.parse(JSON.stringify(original)); // structuredClone() is also used to create a deep copy

deepClone.b.c = 3;
console.log(original.b.c); // Outputs 2
```
## Q. Diff b/w Array.foreach and Array.map?
**forEach:**
Executes a function for each element.
Does not return a new array.
Used for side effects.
**map:**
Executes a function for each element.
Returns a new array.
Used for transforming data.
## Q. Diff b/w map, reduce, filter, find?
**map:** Transforms each element and returns a new array.
**reduce:** Reduces the array to a single value.
**filter:** Filters elements based on a condition and returns a new array.
**find:** Finds and returns the first element that satisfies a condition.
## Q Diff b/w call, bind, apply?
**call:** Invokes a function with a specified this context and individual arguments.
**apply:** Invokes a function with a specified this context and arguments as an array.
**bind:** Creates a new function with a specified this context and optionally prepends arguments.
## Q. Explain hoisting in js?
Hoisting in JavaScript is a behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase. This means you can use variables and functions before they are declared in the code.

Variables declared with var are hoisted to the top of their function or global scope, but their initialization is not hoisted.
Variables declared with let and const are also hoisted but are not initialized. Accessing them before their declaration results in a ReferenceError due to the **temporal dead zone (TDZ)**.

Function declarations are fully hoisted, meaning both the function name and its definition are moved to the top of their scope.
## Q. generator function, IIFE?
A generator function can pause and resume execution using the yield keyword. Defined with function*.
```
function* generatorFunction() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = generatorFunction();
console.log(generator.next().value); // Outputs 1
```
An IIFE is a function that runs immediately after being defined, creating a new scope.
```
(function() {
    const message = 'Hello, World!';
    console.log(message);
})();
// Outputs: Hello, World!
```
## Q. Promise.all() vs Promise.allSettled() vs Promise.any() & Promise.race()?
**Promise.all():** Runs multiple promises in pararrel; fails fast if any promise rejects.
**Promise.allsettled:** Runs multiple promises in pararrel, and result includes both fulfilled & rejected.
**Promise.race():** Waits for the first promise to settle (either resolve or reject).
**Promise.any:** Resolves with the first fulfilled promise, ignoring rejections.
## Q. Explain Object.freeze()?
Object.freeze() is a method in JavaScript that prevents an object from being modified. This is useful for creating immutable objects. Although, Nested objects are not frozen.
## Q. How does js handle concurrency with single-threaded execution?
JavaScript handles concurrency using the **event loop** and **asynchronous programming**. Despite being single-threaded, it can manage multiple tasks efficiently. Here's how it works:
### Event Loop
The event loop is the core mechanism that allows JavaScript to perform non-blocking operations. It continuously checks the call stack and the task queue to determine what to execute next.
### Key Components:
1. **Call Stack**:
   - The call stack is where JavaScript keeps track of function calls. It operates on a Last In, First Out (LIFO) basis.
2. **Web APIs**:
   - Browser-provided APIs (like `setTimeout`, `fetch`, and DOM events) handle asynchronous operations. These APIs run outside the call stack.
3. **Task Queue**:
   - When an asynchronous operation completes, its callback is placed in the task queue. The event loop moves tasks from the queue to the call stack when the stack is empty.
### Example:
```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout');
}, 0);

console.log('End');
```

**Output**:
```
Start
End
Timeout
```
### Explanation:
1. **Start** and **End** are logged immediately because they are synchronous.
2. `setTimeout` is asynchronous and its callback is placed in the task queue.
3. The event loop waits for the call stack to be empty before executing the callback from the task queue.
### Promises and Microtasks:
Promises use a microtask queue, which has higher priority than the task queue. Microtasks are executed immediately after the current task completes, before any tasks from the task queue.
```
console.log('Start');

Promise.resolve().then(() => {
    console.log('Promise');
});

console.log('End');
```
**Output**:
```
Start
End
Promise
```
### Explanation:
1. **Start** and **End** are logged synchronously.
2. The promise's `.then` callback is placed in the microtask queue.
3. The microtask queue is processed before the task queue, so **Promise** is logged before any tasks.

JavaScript's event loop and asynchronous programming model allow it to handle concurrency efficiently, even with a single-threaded execution environment. If you have more questions or need further details, feel free to ask!

