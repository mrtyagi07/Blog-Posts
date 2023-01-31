# Promises in Javascript

## Why do we need promises?

Promises are a language feature in JavaScript that provides a way to manage asynchronous operations. Asynchronous operations are operations that do not happen immediately but are executed in the background and completed at some point in the future. For example, making an HTTP request to a server is an asynchronous operation, because the request is sent in the background and the response is received at a later time.

Asynchronous operations are important in JavaScript because they allow the program to continue executing while the operation is being performed. Without asynchronous operations, the program would have to wait for the operation to complete before moving on to the next step, which could cause the user interface to freeze or become unresponsive.

However, managing asynchronous operations can be tricky, because the code that relies on the results of these operations needs to be executed in a different order than it is written in. This can lead to callback hell, where the code becomes difficult to read and maintain due to a large number of nested callback functions.

%[https://twitter.com/mrtyagi07/status/1599737130716377088?s=20&t=bht2AnHQZIqB1s5INNcskQ] 

Promises provide a solution to this problem by allowing a program to make a promise to do something and to attach callback functions that will be executed when the promise is fulfilled or rejected. This makes it possible to write code that is more modular and easier to read, and that is easier to debug and maintain. As a result, promises are an essential tool for managing asynchronous operations in JavaScript.

## The Promise Lifecycle

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670244793556/4hfEzhSob.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670253277673/HGZJheekE.png align="left")

### Consuming Promise

Consuming a promise means using the promise to perform some action when it resolves. This is typically done using the then() method, which is called on the promise and takes a callback function as its argument. The callback function is executed when the promise resolves, and it is passed the resolved value of the promise as an argument.

```javascript
const request = fetch('https://restcountries.com/v2/name/usa');
console.log(request)//Promise {<pending>}
```

In this code, the fetch() function is used to make a network request to the provided URL. The fetch() function returns a promise, which represents the eventual result of the network request.

When you log the request variable to the console, you will see the promise object itself, not the result of the network request. The result of the network request will not be available until the promise resolves, at which point you can consume the promise to access the result.

Here is an example of how you might consume the promise to get the result of the network request:

```javascript
const request = fetch('https://restcountries.com/v2/name/usa');
request.then(response => {
 // The response is a promise that contains the response data
  // Use the json() method to extract the data as JSON
 return response.json();
//json will also return promise to handle that promise we have to use again next()
})
.then(data => {
// The data is the parsed JSON response from the server
console.log(data);
})
.catch(error => {
 // If the promise is rejected, this callback function will be executed
 console.error(error);
 });
```

In this example, the then() method is used to consume the initial promise returned by fetch(). The first then() method extracts the response data from the promise and parses it as JSON. The second then() method consumes the promise that contains the parsed JSON data, and logs it to the console. The catch() method is used to handle any errors that may occur during the asynchronous operations.

### Chaining Promises

Promises can be chained together to perform multiple asynchronous operations in sequence. This is done by returning a new promise from the callback function passed to a then() method.

```javascript
const getCountryData = function (country) {
fetch(`https://restcountries.com/v2/name/${country}`)
.then(response => response.json())
 .then(data => {
renderCountry(data[0]);
const neighbour = data[0].borders?.[0];
  if (!neighbour) return;
  return fetch(`https://restcountries.com/v2/alpha/${neighbour}`);
})
  .then(response => response.json())
.then(data => renderCountry(data, 'neighbour'));
};
getCountryData('bharat');
```

The getCountryData function uses the fetch API to make two requests to the https://restcountries.com website. The first request is made to the https://restcountries.com/v2/name/{country} endpoint to get information about the specified country. The second request is made to the https://restcountries.com/v2/alpha/{neighbour} endpoint to get information about a neighbouring country of the original country.

These requests are made using the then method, which allows us to chain promises together. The then method is called on the initial fetch call, and it takes a callback function as an argument. This callback function is called when the initial promise is fulfilled, and it returns a new promise that makes a request to the https://restcountries.com/v2/alpha/{neighbour} endpoint.

The second then method is called on the new promise returned by the first then method, and it takes another callback function as an argument. This callback function is called when the second promise is fulfilled, and it parses the response as JSON and passes the data to the renderCountry function.

In this way, the code uses promise chaining to make two requests in sequence and handle the responses from these requests. This allows the code to make one request, wait for the response, and then make another request based on the data from the first response.

%[https://codepen.io/mrtyagi07/pen/eYKbEyq] 

## Handling Rejected Promise

If a promise is rejected, that means that it was unable to fulfill the specified request or operation. In that case, you can use the catch method to handle the rejection. This method takes a single argument, which is a callback function that will be executed when the promise is rejected. The callback function should generally include some code to handle the error or failure and to let the user know that the promise was not fulfilled.

Here's an example of how you might use the catch method to handle a rejected promise:

```javascript
promise
.then(result => {
// Do something with the successful result
})
.catch(error => {
// Handle the error or failure
 console.log(error);
 });
```

In this example, the catch method is used to handle any errors or failures that occur when the promise is executed. If the promise is fulfilled successfully, the then method will be executed and the result will be passed to the callback function as an argument. If the promise is rejected, however, the catch method will be executed and the error will be passed to the callback function as an argument.

### **How does *finally* work in relation to rejected promises? (Refer to Promise Lifecycle)**

The finally method is used to execute a piece of code after a promise has been settled, whether it was fulfilled successfully or rejected. This can be useful for performing cleanup operations, such as closing a loading spinner or removing a loading message from the screen.

Here's an example of how you might use the finally method:

```javascript
promise
.then(result => {
 // Do something with the successful result
  })
 .catch(error => {
 // Handle the error or failure
 })
.finally(() => {
 // Perform some cleanup operations
 });
```

In this example, the finally method is used to execute a callback function after the promise has been settled. If the promise is fulfilled successfully, the then method will be executed and the result will be passed to the callback function as an argument. If the promise is rejected, the catch method will be executed and the error will be passed to the callback function as an argument. In either case, the finally method will be executed after the promise has been settled, allowing you to perform any necessary cleanup operations.

### Throwing errors manually

Throwing errors manually in promises can be useful for a few reasons. First, it allows you to reject a promise with a specific error or failure message, rather than using a generic error. This can make it easier to debug your code and understand what went wrong when the promise is rejected.

Second, throwing errors manually in promises can also help you enforce preconditions or constraints on your code. For example, you might throw an error if a certain condition is not met, such as if a required parameter is missing or if a value is not within a certain range. This can help prevent errors or bugs in your code by ensuring that the conditions required for the promise to be fulfilled are always met.

Here's an example of how you might throw an error in a promise:

```javascript
promise
 .then(result => {
 if (result.length === 0) {
throw new Error("No results found!");
}
 // Do something with the successful result
})
 .catch(error => {
// Handle the error or failure
console.log(error.message);
});
```

In this example, the then method is used to check the length of the result and throw an error if it is equal to zero. If the result has a length of zero, the promise will be rejected and the catch method will be executed, logging the error message to the console. If the result has a non-zero length, the then method will be executed and the result will be used as normal.

**As we did in our previous pen, let's look at an actual API example**

> The fetch method returns a promise that is fulfilled with the response object when the request is successful, or rejected with an error when the request fails.
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670344427063/5p0qDn_5K.png align="left")

`To manually throw an error, we can use the ok property of the response object For error(4XX) it will be false and for success(2XX) it will be true.`

Here is a pen where clicking on the button will cause an error due to input. Please check the code for more information. As a result, I use catch, finally, and throw in the code below to manage the code error. Play with it.

%[https://codepen.io/mrtyagi07/pen/oNymbYX] 

## HOW ASYNCHRONOUS JAVASCRIPT WORKS BEHIND THE SCENES

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670427391890/8yFlqPR3O.png align="center")

Asynchronous JavaScript is a programming technique that allows a program to perform multiple tasks at the same time, rather than waiting for one task to be completed before starting another. This is accomplished by using an event loop, which is a continuous loop that listens for events, such as user input or network requests, and then triggers a callback function to handle the event when it occurs.

The event loop works by checking the callback queue for any pending events that need to be processed. When an event is detected, the event loop will pause the execution of the current task and trigger the callback function associated with that event. The callback function will then be executed, and once it completes, the event loop will continue its loop and check for any additional events that may have occurred in the meantime.

### **Here's a step-by-step explanation of how this process works:**

*   The JavaScript code calls a web API, such as fetch() or setTimeout().
    
*   The event loop adds a task to the queue that represents the call to the web API.
    
*   The event loop finds an available event handler to process the task.
    
*   The event handler executes the code to make the call to the web API.
    
*   The web API performs its intended function, such as making an HTTP request or manipulating the DOM.
    
*   When the web API has completed its task, it notifies the event loop.
    
*   The event loop adds a callback function to the callback queue that will be executed when the call stack is empty.
    
*   The call stack is a data structure that tracks the execution of functions in JavaScript. It is "last-in, first-out," which means that when a function is called, it is added to the top of the stack, and when a function returns, it is removed from the top of the stack.
    
*   When the call stack is empty, the event loop checks the callback queue to see if there are any callback functions that need to be executed.
    
*   If there are callback functions in the callback queue, the event loop will add a task to the queue to execute the first callback function in the queue.
    
*   The event loop finds an available event handler to process the task, and the event handler executes the callback function.
    
*   When the callback function has completed its task, it returns, and the task is removed from the call stack.
    
*   This process continues until all callback functions in the callback queue have been executed.
    
*   The event loop continues to check for new tasks that have been added to the queue, and the process repeats.
    
    ### Microtasks queue
    
    ![Let's spin the event loop - Exploration of event loop concept of javascript  and its different pieces like macro and micro tasks | Medium | JavaScript  in Plain English](https://miro.medium.com/max/1400/1*Noox731-OSUBmhWvLRbgJA.png align="left")
    
    In JavaScript, a microtasks queue is a queue of tasks that are executed one after the other, in the order in which they were added to the queue. This is different from the normal task queue, which is used to execute tasks that occur at a later time, such as user-generated events or asynchronous I/O operations.
    
    A microtasks queue is typically used for tasks that need to be executed as soon as possible, but cannot be executed immediately because the JavaScript runtime is currently executing some other code. Examples of such tasks include resolving Promises, running async/await functions, and updating the state of React components.
    
    **To give a more concrete example, imagine that you have some code that looks like this:**
    
    ```javascript
    async function foo() {
     // Do some work...
     await bar();
    // Do some more work...
    }
    ```
    
    When the foo function is executed, the JavaScript runtime will first execute the code inside the function until it reaches the await statement. At this point, the runtime will pause the execution of the foo function and add a task to the microtasks queue to resolve the bar Promise. The runtime will then continue to execute any other tasks that are currently in the microtasks queue, until the queue is empty. Once the microtasks queue is empty, the runtime will resume the execution of the foo function and run the code after the await statement.
    
    In this way, the microtasks queue provides a way for the JavaScript runtime to execute certain tasks as soon as possible, without interrupting the execution of other code. This can help to improve the overall performance and responsiveness of your JavaScript applications.
    
    **Let's take one more example**
    
    ```javascript
    console.log('Test Start');
    setTimeout(() => console.log('0 sec timer'), 0);
    
    Promise.resolve('Resolved promise 1').then(response => console.log(response));
    
    Promise.resolve('Resolved prmise 2').then(response => {
    for (let i = 0; i < 1000000000; i++) {}
      console.log(response);
    });
    
    console.log('Test End!');
    ```
    
    ```javascript
    //If you were to run this code, the output would be:
    Test Start
    Test End!
    Resolved promise 1
    Resolved promise 2
    0 sec timer
    ```
    
*   The code starts by logging the string "Test Start" to the console.
    
*   The setTimeout function is called with a callback that logs the string "0 sec timer" to the console. However, the timeout is set to 0, so the callback will not be executed immediately. Instead, it will be added to the callback queue and will be executed at a later time.
    
*   The Promise.resolve function is called with the string "Resolved promise 1" as its argument. This creates a new Promise that is immediately resolved with the given value. The then method is called on the Promise, with a callback that logs the response to the console. This callback is added to the microtasks queue.
    
*   The second Promise.resolve function is called with the string "Resolved promise 2" as its argument. This creates another Promise that is immediately resolved with the given value. The then method is called on this Promise, with a callback that logs the response to the console. This callback also contains a loop that iterates a billion times, which will take a long time to complete. This callback is also added to the microtasks queue.
    
*   The code logs the string "Test end" to the console.
    
    <mark>At this point, the JavaScript runtime will start to execute the tasks in the microtasks queue. Since the microtasks queue has a higher priority than the callback queue, the runtime will execute the tasks in the microtasks queue before it executes the tasks in the callback queue.</mark>
    
    1.  First, the runtime will execute the callback for the first Promise.resolve call, which logs the string "Resolved promise 1" to the console.
        
    2.  Next, the runtime will execute the callback for the second Promise.resolve call. This callback contains a loop that iterates a billion times, so it will take a long time to complete. While this callback is executing, the runtime will not be able to execute any other tasks in the microtasks queue or the callback queue.
        
    3.  Once the loop in the second callback has finished executing, the runtime will log the string "Resolved promise 2" to the console. At this point, the microtasks queue will be empty, so the runtime will start to execute the tasks in the callback queue.
        
    4.  Since the only task in the callback queue is the callback for the setTimeout function, the runtime will execute this callback and log the string "0 sec timer" to the console.
        

This is why the output of the code is "Test Start", "Test end", "Resolved promise 1", "Resolved promise 2", "0 sec timer".

> The time specified in the setTimeout function only determines when the callback for that function will be added to the callback queue. It does not affect the execution of tasks in the microtasks queue.
> As long as there are tasks in the microtasks queue, the JavaScript runtime will always execute those tasks before it executes any tasks in the callback queue, regardless of the timeouts specified for the callback queue tasks.

**Let's examine the difference between a callback queue and a microtasks queue**

The difference between the callback queue and the microtasks queue is that the callback queue is used to execute tasks that occur at a later time, such as user-generated events or asynchronous I/O operations, while the microtasks queue is used to execute tasks that need to be executed as soon as possible.

In other words, the callback queue is used to queue tasks that are triggered by external events, such as a user clicking on a button or a network request completing, while the microtasks queue is used to queue tasks that are generated internally by the JavaScript runtime, such as resolving Promises or running async/await functions.


As a result, tasks in the callback queue are typically executed after the current code has finished executing, while tasks in the microtasks queue are executed before the current code has finished executing. **This means that tasks in the microtasks queue have a higher priority and are executed sooner than tasks in the callback queue.**


<mark>But wait, if that's the case, it will cause starvation, right?</mark>


If the microtasks queue is constantly being filled with tasks and the tasks in the queue are always being executed before the tasks in the callback queue, then it is possible for the callback queue to become "starved" or "depleted" of tasks.

This can happen if the microtasks queue contains a large number of tasks that take a long time to execute, or if the microtasks queue is constantly being refilled with new tasks. In either case, the callback queue may not have an opportunity to execute any of its tasks, which can lead to poor performance or other issues in your JavaScript application.


*To avoid this problem*, it is important to ensure that the microtasks queue is not overused and that it is only used for tasks that truly need to be executed as soon as possible. This can help to ensure that the callback queue has an opportunity to execute its tasks and that your application runs smoothly.


## Let's Build a Simple Promise

```javascript
const myPromise = new Promise((resolve, reject) => {
// Do some work (e.g. a network request)
if (workSuccessful) {
// If the work is successful, call the resolve function
 resolve('Success!');
 } else {
// If the work is not successful, call the reject function
reject('Error: Work failed');
}
});
```

In this example, the myPromise variable references a new Promise object that is created using the Promise constructor. The constructor takes a function as its argument, which is called the "executor" function.

The executor function receives two arguments, resolve and reject, which are functions that can be used to signal the success or failure of the Promise. In this example, the executor function does some work (e.g. a network request), and then calls the resolve function if the work is successful, or the reject function if the work is not successful.

Once the Promise has been created, you can use its then and catch methods to handle the success or failure of the Promise. For example:

```javascript
myPromise
  .then(response => {
 // Handle the success of the Promise here
 console.log(response);
 })
  .catch(error => {
   // Handle the failure of the Promise here
console.error(error);
  });
```

In this code, the then method is called on the myPromise object, with a callback that handles the successful resolution of the Promise. The catch method is called on the same object, with a callback that handles the failure of the Promise.

When the Promise is resolved (either successfully or unsuccessfully), the appropriate callback will be executed, allowing you to handle the result of the Promise in your code.

## Promise with Async/Await

Async/await was introduced in JavaScript with the release of ECMAScript 2017, which was published in June 2017.

Async/await was introduced as an alternative to using the then() method to handle asynchronous code in JavaScript. While the then() method is still widely used and is a powerful way to write asynchronous code, async/await offers several advantages over using the then() method alone.

One of the main advantages of async/await is that it makes asynchronous code easier to read and write. Async/await allows you to use language constructs that are familiar from synchronous code, such as the await keyword and the try/catch statement. This makes it easier to write asynchronous code that looks and behaves like synchronous code, which can make it easier to understand and maintain.

Overall, async/await offers a more intuitive and readable way to write asynchronous code in JavaScript, and it is becoming increasingly popular among JavaScript developers. While the then() method is still a powerful and widely used way to handle async functions, async/await offers several advantages that make it a compelling alternative.

### Here is an example of using async/await to consume a real-life API in JavaScript:

```javascript
async function getUserData(userId) {
  // Call the API to get the user data
 const response = await fetch(`https://example.com/api/users/${userId}`);
 const userData = await response.json();
// Do something with the user data
console.log(userData);
}
getUserData(12345);
console.log('I will execute first');
//aysnc functio will execute in background 
// so that's why 'I will execute first' will print first
```

In this example, the async keyword is used to define an asynchronous function called getUserData(), which takes a userId parameter. Inside the function, the fetch() method is used to call the API and get the user data for the specified userId. The await keyword is used to wait for the API call to complete, and the response.json() method is used to parse the response as JSON.

Once the API call has been completed and the user data has been parsed, the userData variable will contain the user data, and you can use it to do something with the data. In this example, the user data is simply logged to the console, but in a real application, you could use the user data to update the UI, make additional network requests, or perform some other action.

### Error Handling

Async/await makes it easy to handle errors when working with asynchronous code in JavaScript. When using async/await, you can use the try/catch statement to handle any errors that may occur.

**Here is an example of how to handle errors using async/await in JavaScript:**

```javascript
async function example() {
try {
 // Wait for the promise to resolve
  const result = await someAsyncFunction();
    // Do something with the result
  console.log(result);
  } catch (error) {
 // Handle any errors that occurred
 console.error(error);
 }
}
```

In this example, the try/catch statement is used to handle any errors that may occur while calling the someAsyncFunction() and waiting for the promise to resolve. If an error occurs, it will be caught by the catch block, and you can handle it by logging the error to the console or performing some other action.

**To throw a new error using async/await in JavaScript, you can use the throw keyword inside the try block of a try/catch statement.**

```javascript
async function example() {
  try {
  // Wait for the promise to resolve
 const result = await someAsyncFunction();
// Do something with the result
 console.log(result);
 // Throw an error if something goes wrong 
// If you remember 'ok' in previous ex, you can use it for real APIs
 if (result === undefined) {  
  throw new Error('Something went wrong!');
  }
 } catch (error) {
 // Handle any errors that occurred
  console.error(error);
 }
}
```

In this example, the throw keyword is used inside the try block to throw a new error if the result is undefined. If an error is thrown, it will be caught by the catch block, and you can handle it by logging the error to the console or performing some other action.

### How to handle return value from async function

```javascript
async function example() {
// Wait for the promise to resolve
 const result = await someAsyncFunction();
 return result;
}
const response = example();
console.log(response); //Promise
```

In this example, the return keyword is used inside the example() function to return the result after it has been resolved by the someAsyncFunction().

**This is where things get interesting :** <mark>when you use the return keyword inside an async function in JavaScript, it will return a promise that resolves to the returned value.</mark>

Once the example() function has been called, you can use the then() method to access the returned value and do something with it.

```javascript
// Call the async function and access the returned promise
example().then(result => {
// Do something with the result
 console.log(result);
});
```

It may seem like we are mixing two different approaches here, using async/await and the then() method to handle the promise. However, if we are using async/await, it would make more sense to use it consistently and handle the return value using async/await as well.

Here is an example of how to use the await keyword to handle the returned promise from an async function in JavaScript:

```javascript
// Call the async function and use the await keyword to handle the returned promise
const result = await example();
// Do something with the result
console.log(result);
```

<mark>In order to use the await keyword, you must define an async function. One way to do this is by using an IIFE (Immediately Invoked Function Expression)</mark>

%[https://twitter.com/mrtyagi07/status/1601477668993892354] 

Let's put the entire code in try/catch block for error handling ad use IIFE

```javascript
async function example() {
  try {
    const result = await someAsyncFunction();
    if (result === undefined) {
      throw new Error('Something went wrong!');
    }
    return result;
  } catch (error) {
    console.error(error);
    //Reject promise returned from async function
      throw error;
  }
}

(async function () {
  try {
    const response = await example();
    console.log(response); //undefined if not throw the error
  } catch (error) {
    console.error(error);
  }
})().finally('No Matter what happens I will Print');
```

<mark>It is worth noting that if an error occurs in the result, the promise will not be rejected, and it will print undefined to the console, despite the use of a try/catch block. To ensure that errors are properly handled, we need to throw the error from the example() function.</mark>

Let's take a live API example; I am attaching a pen below Please check the code for more information.

%[https://codepen.io/mrtyagi07/pen/PoagOOL?editors=1111] 

## Run Promises Parallelly (Promise Combinators)

To run promises in parallel in JavaScript;There are several promise combinators (methods that combine or manipulate promises) in JavaScript, including:

### Promise.all()

You can use the **Promise.all()** method. The Promise.all() method **takes an array of promises as an argument**, and it **returns a single promise** that resolves when all of the promises in the array have been resolved.

Here is an example of how to use the Promise.all() method to run promises in parallel in JavaScript:

```javascript
const promise1 = fetch('https://example.com/api/users/1');
const promise2 = fetch('https://example.com/api/users/2');
const promise3 = fetch('https://example.com/api/users/3');

// Run the promises in parallel using Promise.all()
const results = await Promise.all([promise1, promise2, promise3]);

// Do something with the results
console.log(results);
```

In this example, three promises are created using the fetch() method, and they are stored in the promise1, promise2, and promise3 variables. The Promise.all() method is then used to run the promises in parallel, and it returns a single promise that resolves when all of the promises in the array have been resolved. The results variable will contain an array of the resolved values from the promises, and you can use it to do something with the results.

### Promise.race()

To use the Promise.race() method in JavaScript, you can pass an array of promises as an argument to the Promise.race() method, and **it will return a single promise that resolves or rejects as soon as one of the promises in the array has been resolved or rejected**.

```javascript
const promise1 = fetch('https://example.com/api/users/1');
const promise2 = fetch('https://example.com/api/users/2');
const promise3 = fetch('https://example.com/api/users/3');

// Use Promise.race() to resolve or reject the promise as soon as one of the promises in the array has been resolved or rejected
const result = await Promise.race([promise1, promise2, promise3]);

// Do something with the result
console.log(result);
```

> The Promise.race() method behaves like a short circuit in JavaScript. Unlike the Promise.all() method, which waits for all of the promises in an array to be resolved before resolving the returned promise, the Promise.race() method resolves or rejects the returned promise as soon as one of the promises in the array has been resolved or rejected.

### Promise.allSettled()

The Promise.allSettled() method is a new method that was introduced in the ECMAScript 2020 specification. It is similar to the Promise.all() method, but **it returns a promise that is fulfilled with an array of objects that describes the final state of each of the promises in the iterable passed as an argument.**

```javascript
Promise.allSettled([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
]).then(res => console.log(res));
```

If you run the code snippet you provided, the output will be an array of objects with the following properties:

```javascript
[
  { status: "fulfilled", value: "Success" },
  { status: "rejected", reason: "ERROR" },
  { status: "fulfilled", value: "Another success" },
]
```

In this case, the iterable contains three promises: one that is resolved with the value "Success", one that is rejected with the reason "ERROR", and one that is resolved with the value "Another success".

The Promise.allSettled() method waits for all of the promises in the iterable to be settled (either resolved or rejected), and it returns an array of objects that describes the final state of each promise. Each object in the array has a status property that specifies whether the promise was fulfilled or rejected, and a value or reason property that contains the resolved value or rejected reason from the promise.

> The main difference between the Promise.all() and Promise.allSettled() methods in JavaScript is that the Promise.all() method returns a single promise that is resolved when all of the promises in the iterable passed as an argument have been resolved, while the Promise.allSettled() method returns a single promise that is fulfilled with an array of objects that describes the final state of each of the promises in the iterable.

```javascript
Promise.all([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
]).then(res => console.log(res));
//If you run the code snippet you provided, the output will be a rejected promise with the reason "ERROR".
```

Since one of the promises in the iterable is rejected with the reason "ERROR", the Promise.all() method will return a rejected promise with the same reason. <mark>The then() callback function will not be executed, and the Promise.all() method will not return an array of the resolved values from the promises.</mark>

In contrast, the <mark>Promise.allSettled() method will wait for all of the promises in the iterable to be settled (either resolved or rejected),</mark> and it will return a fulfilled promise with an array of objects that describes the final state of each promise. <mark>This allows you to handle the results of promises that may be rejected without having to deal with rejected promises.</mark>

### Promise.any()

The Promise.any() method is a proposed addition to the ECMAScript specification, but it is not yet part of the official JavaScript language. It is similar to the Promise.race() method, but it returns a promise that is resolved with the value of the first settled promise in the iterable passed as an argument, instead of rejecting the promise if any of the promises in the iterable are rejected.

```javascript
// Use a polyfill or third-party library to add the Promise.any() method to your code
import 'promise.any';

Promise.any([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
]).then(res => console.log(res));
//If you run the code snippet you provided, the output on the console will be the resolved value "Success".
```

In this case, the iterable contains three promises: one that is resolved with the value "Success", one that is rejected with the reason "ERROR", and one that is resolved with the value "Another success". Since the first promise in the iterable is resolved with the value "Success", the Promise.any() method will return a promise that is resolved with the same value. The then() callback function will be executed, and the console.log() statement will print the resolved value "Success" on the console.

*In conclusion, promises are an important concept in JavaScript that allows you to handle asynchronous operations cleanly and efficiently. We have seen how to create and use promises, and how to chain them together using the then() and catch() methods. We have also discussed some advanced techniques for working with promises, such as using async/await, and the various methods in the Promise API, such as Promise.all(), Promise.race(), and Promise.any().*

*Overall, promises are a powerful tool for working with asynchronous operations in JavaScript, and they can help you to write clean, maintainable code that is easy to debug and understand. Whether you are a beginner or an experienced JavaScript developer, it's worth learning more about promises and how they can benefit your projects*

> I hope you enjoyed reading this blog post. If you would like to stay updated on my progress and engage in discussions with me on a variety of topics, you can follow me on Twitter. I regularly post updates on my work and thoughts on various topics, and I am always open to chatting with others on the platform.