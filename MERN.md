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

