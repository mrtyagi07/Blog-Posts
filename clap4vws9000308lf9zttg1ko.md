# Hoisting in JavaScript

Hoisting is the default behavior of javascript where all the variable and function declarations are moved on top. This means that irrespective of where the variables and functions are declared, **they are moved on top of the scope**. The scope can be both local and global.

![hoisting.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668933481166/oO8lU9XQa.png align="left")

*Being able to use a variable's value in its scope before the line it is declared. ("Value hoisting")*

```
hoistedVariable = 3;

console.log(hoistedVariable); 
// outputs 3 even when the variable is declared after it is initialized	

var hoistedVariable;
``` 

```
hoistedFunction();  
// Outputs " Hello world! " even when the function is declared after calling

function hoistedFunction(){ 
  console.log(" Hello world! ");
} ``` 

*Being able to reference a variable in its scope before the line it is declared, without throwing a ReferenceError, but the value is always undefined. ("Declaration hoisting")*

**Note - Variable initializations are not hoisted, only variable declarations are hoisted**


```
var x;
console.log(x);
 // Outputs "undefined" since the initialization of "x" is not hoisted
x = 23;``` 

*let, const, and class as non-hoisting, because the **temporal dead zone** strictly forbids any use of the variable before its declaration.  However, the temporal dead zone can cause other observable changes in its scope, which suggests there's some form of hoisting:* 


```
const x = 1;

{
  console.log(x);  // ReferenceError
//The top statement reads the x from the const x = 2 declaration instead (const x=1), which is not initialized. This causes a ReferenceError.
  const x = 2;
}
``` 

**Follow me on Twitter for updates on my progress and to chat with me about anything and everything.** 😇🙂

[Twitter Profile](https://twitter.com/mrtyagi07)