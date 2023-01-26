# Javascript : Promise, Await, And Async
Git repository for understanding asynchronous execution code. It begins with an explanation of 'await new Promise()'.

- base on...
- setTimeout, setInterval : Examples of asynchronous
- await new Promise()
- async, await chains
- What is Promise?
- What is Async and Await?

## base on...
1. Understanding Functions
a function is a block of code that can be defined, named, and reused throughout a program. Functions are a fundamental building block of the language and are used to perform specific tasks. Functions are defined using the function keyword, followed by the name of the function and a set of parentheses. The code inside the function is enclosed within curly braces.
2. Understanding Class
In JavaScript, a class is a special type of object that is used as a blueprint for creating new objects. It is a template for an object, and it defines the properties and methods that the object will have. Classes in JavaScript are defined using the class keyword, and they can have a constructor method and other methods and properties. Classes are typically used to create objects that have similar characteristics and behavior, and they can be used to organize and structure code in a more modular and reusable way.
3. Understanding Asynchrony : The main topic we will learn this time.
Asynchrony is a programming paradigm where multiple operations can occur independently of each other, without blocking the execution of the program. This allows the program to continue running and responding to other events while waiting for a long-running operation to complete. JavaScript allows for asynchrony through the use of callback functions, Promises, and async/await.

## setTimeout, setInterval

## await new Promise()
First, I will introduce the usage and the order of operation.
```
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
3. codeC and codeD are executed at the same time (multitasking)

For example,
```
(async function(){
    console.log(1);
    await new Promise(function(resolve,reject){ // It takes 1 second to go to the next line.
        setTimeout(function(){
            resolve();
        },1000);
    });
    console.log(2);
    await new Promise(function(resolve,reject){ // It takes 0.5 second to go to the next line.
        setTimeout(function(){
            resolve();
        },500);
    });
    console.log(3);
    await new Promise(function(resolve,reject){ // It takes 0.4 second to go to the next line.
        setTimeout(function(){
            resolve();
        },400);
    });
    console.log(4);
    await new Promise(function(resolve,reject){ // It takes 0.3 second to go to the next line.
        setTimeout(function(){
            resolve();
        },300);
    });
    console.log(5);
    await new Promise(function(resolve,reject){ // It takes 0.2 second to go to the next line.
        setTimeout(function(){
            resolve();
        },200);
    });
    console.log(6);
    await new Promise(function(resolve,reject){ // It takes 0.1 second to go to the next line.
        setTimeout(function(){
            resolve();
        },100);
    });
    console.log(7);
})()
```
