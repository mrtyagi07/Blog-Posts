---
title: "Debugging: Because Writing Perfect Code is Overrated"
seoTitle: "Debugging"
seoDescription: "Debugging is a crucial part of the software development process, but it can be frustrating and time-consuming if you don't have the right mindset."
datePublished: Tue Mar 07 2023 13:24:37 GMT+0000 (Coordinated Universal Time)
cuid: cleya99z4000g09l6bhi57yq3
slug: debugging-because-writing-perfect-code-is-overrated
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678194808948/686e8c11-5803-4b31-9a6c-2598edfea092.png
tags: javascript, reactjs, debuggingfeb

---

In my opinion, coding represents only 10% of the equation, while debugging comprises the remaining 90%. If you excel at debugging, you can effectively tackle any coding problem. As such, I would like to share some tips that I have acquired through my experience.

Having good debugging skills is directly proportional to your understanding of the problem at hand. The better you comprehend the problem, the easier it is to identify and fix issues that may arise during the coding process. Therefore, it is crucial to invest time and effort into comprehending the problem thoroughly before attempting to write code.

## Understand the Flow

Whenever I encounter difficulties in my coding process, I resort to a simple yet effective technique. I grab a pen and paper and start drawing a flowchart that outlines the overall structure of my program. This approach allows me to gain a better understanding of how my code behaves in practice and enables me to identify potential issues more easily.

Here's a simple example of code in React that demonstrates understanding the flow:

```javascript
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  const handleDecrement = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={handleIncrement}>Increment</button>
      <button onClick={handleDecrement}>Decrement</button>
    </div>
  );
}

export default Counter;
```

We have a `Counter` component that displays a count value and two buttons to increment and decrement the count. We're using the `useState` hook to manage the count state and two event handlers to update the count value when the user clicks on the buttons. By understanding the flow of data through the component and the lifecycle of state updates, we can ensure that our component functions correctly and efficiently

## Pay attention to the error messages

It is essential to pay attention to error messages when programming. Error messages can give you valuable information about what went wrong in your code and can help you quickly identify and fix the issue.

When you encounter an error message, make sure to read it carefully and try to understand what it's telling you. Often, error messages will include details about the type of error, the file and line number where the error occurred, and other information that can be useful in diagnosing the problem.

```javascript
function multiply(a, b) {
  return a * b;
}

console.log(multiply(2, 3, 4));
```

We have a function `multiply` that takes two arguments and returns their product. However, in the `console.log` statement, we're calling the `multiply` function with three arguments instead of two. When we run this code, we get the following error message in the console:

```javascript
Uncaught TypeError: multiply() takes 2 positional arguments but 3 were given
```

This error message tells us that we're calling the `multiply` function with three arguments, but it only takes two. By paying attention to this error message, we can quickly identify the problem and fix it by removing the extra argument from the `console.log` statement.

## Logs Data in the Console

During the coding process, it is common to want to verify the point at which your code is executing or to ensure that you are receiving the correct values. Conversely, if you are receiving unexpected or incorrect values, this may indicate an error in your code. In either case, it is essential to use the print statements technique to identify and resolve any issues promptly.

```javascript
function factorial(n) {
  if (n === 0) {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

console.log(factorial(5));
```

In this example, we have a recursive function `factorial` that calculates the factorial of a given number `n`. We're using console.log to print the result of the function to the console.

By logging data in the console, we can get a better understanding of how our code is working and identify any errors or unexpected behaviors. In this case, if we run the code and look at the console output, we can see that the factorial of 5 is 120. If we had made a mistake in our function and calculated the wrong factorial value, we would have seen that in the console output and could have used that information to debug our code.

## Comment the Code

Commenting your code is one of the best ways to debug it. You can comment certain parts of your code, allowing you to compile it first and then add comments step by step. This approach will help you to identify errors and solve them efficiently. Therefore, it is always a good practice to comment your code as it can make debugging much easier and faster.

## Use Debugger

Using a debugger can save you a lot of time when debugging your code. It allows you to step through your code line by line, observe variable values, and identify errors more quickly and easily. For example, for CSS development, a tool like DevTools can be incredibly useful for inspecting elements, modifying styles, and understanding the box model.

Similarly, for React development, React Developer Tools can be incredibly helpful for inspecting React components, their props, and their state. It also makes it easy to identify issues with component rendering or state management.

Additionally, using breakpoints in tools like VS Code can be very effective in isolating and diagnosing issues in your code. By setting a breakpoint at a specific line of code, you can pause the execution of your program at that point and inspect the values of variables and other information. This can help you to quickly pinpoint the source of the issue and fix it efficiently.

## Test

It's important to test your code again and again, using different inputs and scenarios, to ensure that it works correctly in a variety of situations. This will help you to catch errors and bugs that may not have been apparent during initial testing

```javascript
function isEven(num) {
  return num % 2 === 0;
}

console.log(isEven(4)); // true
console.log(isEven(7)); // false
console.log(isEven(-2)); // true
```

We have a function `isEven` that takes a number as an argument and returns `true` if it's even, and `false` if it's odd. We're using console.log to test the function with different input values and verify that it's working correctly.

By testing our code, we can identify any issues or bugs and make sure that our function is working as expected. In this case, we can see that the function is returning the correct results for the input values we tested it with.

Overall, testing our code is an essential part of the debugging process, allowing us to catch errors and ensure that our code is working correctly. We can use various testing methods, such as unit tests, integration tests, and end-to-end tests, to verify the behavior of our code and ensure its quality.

> That's it for this blog! I hope you found these tips and techniques helpful for improving your debugging skills. Remember, debugging is not just about finding and fixing errors, but also about learning and improving our code.
> 
> By approaching debugging with a positive attitude and a willingness to learn from our mistakes, we can become better developers and create software that is more reliable and robust.Thank you for reading, and I'll see you in the next blog!