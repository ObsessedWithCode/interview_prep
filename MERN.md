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
1. ** Data Privacy/Encapsulate: **They allow functions to have private variables, data and logic.
2. ** Maintaining State: **Closures can maintain state across multiple function calls.