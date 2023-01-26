# Javascript : Promise, Await, And Async
Git repository for understanding asynchronous execution code.  

1. base on...
2. setTimeout, setInterval : Examples of asynchronous
3. new Promise(), await, async
4. What is Promise?
5. What is Async and Await?  
  
  
  
## base on...
1. Understanding Functions  
a function is a block of code that can be defined, named, and reused throughout a program. Functions are a fundamental building block of the language and are used to perform specific tasks. Functions are defined using the function keyword, followed by the name of the function and a set of parentheses. The code inside the function is enclosed within curly braces.  

2. Understanding Class  
In JavaScript, a class is a special type of object that is used as a blueprint for creating new objects. It is a template for an object, and it defines the properties and methods that the object will have. Classes in JavaScript are defined using the class keyword, and they can have a constructor method and other methods and properties. Classes are typically used to create objects that have similar characteristics and behavior, and they can be used to organize and structure code in a more modular and reusable way.

3. Understanding Asynchrony  
The main topic we will learn this time.
Asynchrony is a programming paradigm where multiple operations can occur independently of each other, without blocking the execution of the program. This allows the program to continue running and responding to other events while waiting for a long-running operation to complete. JavaScript allows for asynchrony through the use of callback functions, Promises, and async/await.  
  
  
  
  
  
## setTimeout, setInterval  
**setTimeout Function**
```JavaScript
// codeA
setTimeout(function(){
  // codeB
}, time);
// codeC
```
1. codeA is executed.
2. codeC is executed.
3. Code B will start executing after Code C has been running for time milliseconds.
(If Code C has not completed after time milliseconds, Code B will execute along with Code C)  

For example
```JavaScript
let a = 3;
setTimeout(() => {
    console.log(a); // 4
}, 1000);
console.log(3); // 3
a = 4;

> 3
> 4
```
It is executed as if the setTimeout function is ignored, and then the function entered as the argument of the setTimeout function is executed after 1 second.  
  
  
  
  
  
  
**setInterval Function (+ clearInterval Function)**
```JavaScript
// codeA
let value1 = setInterval(function(){ // return the executing function's id.
  // codeB
}, time1);
// codeC
setTimeout(()=>{
  clearInterval(value1), // stop setInterval to execute.
}, time2);
```
1. codeA and codeC are executed as if the setTimeout function is executed, ignoring the setInterval function.
2. However, unlike the setTimeout function, the setInterval function repeats codeB at regular intervals.
codeA -> codeC -> codeB -> codeB -> codeB -> ... (Repeat approximately time2/time1 times)  
  
  
  
  
  
  
  
  
  
## new Promise(), await, async  
First, there are rules to avoid errors.
- Put a function that takes two arguments into the constructor unconditionally. : new Promise( **function(a,b){}** )
- Put the await keyword in front of an async function. : **await** new Promise(function(a,b){})
- To use the await keyword, be sure to add the async keyword to the out-of-scope function. : **async** function(){**await** new Promise(function(a,b){})}
If you follow this rule, you will rarely get an error.  
  
  
Next, I will introduce the usage and the order of operation.
```JavaScript
// codeA
await new Promise(func(resolveFunction,rejectFunction){
  // codeB
  resolveFunction(valueToReturn);
  // codeC
})
// codeD
```
1. codeA is executed.
2. codeB is executed.
3. codeC and codeD start running at the same time. (multitasking)  
  
  
  
  
For example,
```JavaScript
(async function(){
    console.log(1); // 1. Promise-codeA
    
    await new Promise(function(resolve,reject){
        console.log('2-1'); // 2-1. Promise-codeB, setTimeout-codeA 
        setTimeout(function(){
            resolve(); // 2-3. Promise-codeB, setTimeout-codeB
            console.log('2-3');
        },1000);
        console.log('2-2'); // 2-2. Promise-codeB, setTimeout-codeC
    });
    
    console.log(3); // 3. Promise-codeC
})()
```
