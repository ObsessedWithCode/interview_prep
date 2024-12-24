# JavaScript
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
**async/await** is a syntax that makes working with promises easier to read by providing a more synchronous-looking way to write asynchronous code, essentially acting as a cleaner way to chain promise operations together.

```async function executeAsyncFunction() {
    try {
        let result = await myAsyncFunction();
        console.log(result); // Logs: "Operation was successful!"
    } catch (error) {
        console.log(error);
    }
}```
###Key differences between promises and async/await:
**Syntax:** async/await provides a more readable and synchronous-looking syntax for handling asynchronous operations compared to the chaining syntax of promises.
**Error Handling:** With async/await, you can use try...catch blocks for error handling, which is more intuitive than using .catch() with promises.
**Readability:** async/await makes the code easier to read and maintain, especially when dealing with multiple asynchronous operations.

##Q. How does this keyword work in different contexts in js?
##Q. debounce and throttle uses
##Q. What is currying in JS?
##Q. Explain how closures can lead to memory leaks?
##Q. What is garbage collection in js, and how does it work?
##Q. How can you prevent memory leaks in js?
##Q. Explain the concept of function composition in js?
##Q. shallow clone vs deep clone?
##Q. How does js handle concurrency with single-threaded execution?
##Q. diff b/w Array.foreach and Array.map?
##Q. diff b/w map, reduce, filter, find?
##Q diff b/w call, bind, apply?
##Q. Explain event loop in js?
##Q. Explain hoisting in js?
##Q. generator function, IIFE?
##Q. Promise.all() vs Promise.allSettled() vs Promise.any() & Promise.race()?
##Q. Explain Object.freeze()?
