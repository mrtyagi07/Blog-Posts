# What is Virtual DOM in React?

The virtual DOM is a fundamental React concept. If you've written React code in the past few years, then you've probably heard of it. However, you may not understand how it works and why React uses it.

In this blog post, we will dive deep into the topic of the virtual DOM in React. We will explore what the virtual DOM is, how it works, and its benefits in React. We will also see some practical examples of how virtual DOM is used in React applications. By the end of this blog post, you will have a better understanding of virtual DOM and how it plays a crucial role in the performance and efficiency of React applications. So, let's get started!

# Overview

## DOM

Before delving into the intricacies of the virtual DOM, it's important to have a solid understanding of the Document Object Model (DOM). If you're new to the concept of the DOM, I recommend reading my [previous blog post](https://vaibhavtyagi.hashnode.dev/dom-document-object-model) where I cover the basics of the DOM and how it works. With a strong understanding of the DOM, the concept of the virtual DOM will be much easier to grasp. So, let's dive in and explore the virtual DOM in depth.

%[https://vaibhavtyagi.hashnode.dev/dom-document-object-model] 

# Virtual DOM

Virtual DOM is not a concept unique to React. Virtual DOM is a general concept that can be implemented in any JavaScript framework or library. The idea behind virtual DOM is to abstract away the real DOM and instead work with a lightweight in-memory representation of the real DOM. This allows for a more efficient way of updating the actual DOM because instead of manipulating the real DOM directly, changes are made to the virtual DOM first.

For example, instead of re-rendering an entire component and its children when only a small part of the component's state changes, React can use the virtual DOM to determine exactly which parts of the actual DOM need to be updated, and update those parts only.

## **The virtual DOM object**

```javascript
import React from 'react';

const myVirtualDomElement = React.createElement('div', {className: 'my-class'}, 'Hello, Virtual DOM!');
console.log(myVirtualDomElement);
```

In this example, `React.createElement()` is used to create a virtual `div` element with the class name "my-class" and the text content "Hello, Virtual DOM!". The created virtual DOM element is then logged to the console, allowing you to see its properties and structure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674021250877/ee888abe-ab90-4aa8-9e04-7f40890659a1.png align="center")

The object, as seen above, is the virtual DOM. It represents the user interface.

## Dive Deeper

Let's take an example to understand better

```javascript
import React from "react";

function MyComponent({ data }) {
  const [name, setName] = React.useState("John Smith");

  const handleClick = () => {
    setName("Jane Doe");
  };

  return (
    <div>
      <p>Name: {name}</p>
      <button onClick={handleClick}>Change Name</button>
    </div>
  );
}
export default MyComponent;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674023005718/4c8a0015-2924-4b1b-aadf-6f269abe226f.png align="center")

The image on the left is the initial render. As time changes, React creates a new tree with the updated node, as seen on the right side.

<mark>Remember, virtual DOM is just an object representing the UI; nothing gets drawn on the screen</mark>

1. When the component first renders, React will create a virtual DOM object that represents the initial state of the component.
    
2. When the button is clicked and the handleClick function is called, React will update the virtual DOM object to reflect the new state.
    
3. React will then compare the current virtual DOM object with the previous one and find the difference [using a diffing algorithm](https://reactjs.org/docs/reconciliation.html#the-diffing-algorithm), which in this case is the change in the value of the "name" variable.
    
4. React will then update the actual DOM to match the changes made to the virtual DOM.
    
5. This process is known as **<mark>"reconciliation"</mark>** and is what allows React to efficiently update the DOM with minimal changes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674023759444/eb31e97b-1fba-4896-b790-985050429324.png align="center")

As seen in the image above, only the node whose data changes gets repainted in the actual DOM.

In summary, on every render, When a component's state or props change, React will first update the virtual DOM, which is a lightweight representation of the actual DOM. This updated virtual DOM is then compared with the previous version of the virtual DOM to determine which changes need to be made to the actual DOM. <mark>This process is called "reconciliation".</mark>

## A closer look at defining process

The diffing process is an algorithm that compares the virtual DOM tree with the previous version of the virtual DOM tree and calculates the minimum number of changes that need to be made to the actual DOM to bring it in line with the new virtual DOM tree. The algorithm uses a tree-diffing strategy, which means that it compares each individual node in the tree, and determines which nodes have been added, removed, or updated.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674047182895/79cbb102-729a-4efd-9155-c279b67128bf.png align="center")

In our previous example, it will see that the text of the &lt;p&gt; element has changed and update the text accordingly.

When React diffs two virtual DOM trees, it starts by comparing whether or not both s have the same root element. If they have the same elements — in our case, the updated nodes are of the same `p` element type — React moves on and recurses on the attributes.

In both, no attribute is present or updated on the `p` element. React then repeats the procedure on the children. Upon seeing that the `Name` text node has changed, React will only update the actual node in the real DOM.

### How to avoid destroying the old DOM?

When the virtual DOM detects that the elements in the two snapshots have different types, it will perform a complete re-render and destroy the old DOM nodes and build new ones. It's important to note that this type of update should be avoided whenever possible as it can lead to poor performance.

```javascript
import React from "react";

function MyComponent({ data }) {
  const [name, setName] = React.useState("John Smith");
  const [elementType, setElementType] = React.useState("p");

  const handleClick = () => {
    setName("Jane Doe");
    setElementType("h1");
  };

  return (
    <div>
      {elementType === "p" ? <p>Name: {name}</p> : <h1>Name: {name}</h1>}
      <button onClick={handleClick}>Change Name and Element Type</button>
    </div>
  );
}
export default MyComponent;
```

In this example, the handleClick function is changing the state of the elementType from "p" to "h1", which means that the element type of the component changes and react will destroy the old DOM node and build a new one.

### **How do React diffs lists?**

```javascript
<ul> 
  <li>item 2</li>
  <li>item 3/li>
  <li>item 4</li>
</ul>
```

In the next update, let’s append an `item 5` at the end, like so:

```javascript
<ul> 
  <li>item 2</li>
  <li>item 3</li>
  <li>item 4</li>
  <li>item 5</li>
</ul>
```

When comparing items, React starts at the top. It matches the first, second, and third items, and only inserts the last one. It is straightforward for React to compute this.

If we insert `item 1` at the beginning?

```javascript
<ul> 
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  <li>item 4</li>
</ul>
```

Similarly, React compares from the top, and immediately realizes `item 2` doesn’t match `item 1` of the updated tree. It then determines that a list is entirely new, it will rebuild the entire list rather than trying to diff individual items.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674050419406/a147a198-8778-4e21-a2ad-b87d83365f8e.png align="center")

Whenever we map to render a list of items, React alerts us in the browser console if we forget the key prop.

### Why do we need a key?

```javascript
<ul> 
  <li key="2">item 2</li>
  <li key="3">item 3</li>
  <li key="4">item 4</li>
</ul>
 
<ul> 
  <li key="1">item 1</li>
  <li key="2">item 2</li>
  <li key="3">item 3</li>
  <li key="4">item 4</li>
  <li key="5">item 5</li>
</ul>
```

This is known as "keyed" diffing and it helps React optimize the process of updating lists by allowing it to quickly identify which items have changed and which have not. When a list is rebuilt, React will assign a unique key to each list item, and will use that key to compare the current and next list. If an item's key is the same in both lists, React will keep the item in the DOM. However, if an item's key is different in the next list, React will remove the item from the DOM and add a new item with the same key. This process is faster than recreating the entire list from scratch because React only needs to make changes to the items that have been added, removed, or moved.

## What is shadow DOM?

The virtual DOM and shadow DOM are both concepts used in web development to improve the performance of web applications, but they serve different purposes and are implemented differently.

The shadow DOM is a <mark>feature of web browsers that allows developers to attach a separate DOM to an element</mark>. This separate DOM is called the "shadow" DOM and it is hidden from the main page's DOM. The shadow DOM allows developers to create encapsulated, reusable components that can be used across a website or application.

Take, for instance, the HTML `input` element `date`:

```javascript
<input type="date" />
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674051456022/1ff0a239-cf1d-4a73-a286-65865bdd75c0.png align="center")

If we inspect the element using the browser‘s developer tools, we will only see a simple input element. However, internally, browsers encapsulate and hide other elements and styles that make up the input date.

Using Chrome DevTools, we can enable the “Show user agent shadow DOM” option from “Settings” to see the shadow DOM like so:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674051562074/d9e191e2-79ac-472e-be70-9946c957895f.png align="center")

When this element is rendered, the browser creates a shadow tree within the element that contains the elements needed to display the date picker. This includes the calendar grid, the previous and next buttons, and the input field for the selected date. The styles for these elements are also scoped to the shadow tree and do not affect the rest of the page. This ensures that the date picker will be consistent across different browsers and platforms.

## **Comparison chart: Real DOM vs Virtual DOM vs Shadow DOM**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674053730014/44c6dcaf-62e0-4743-a542-473eebdb79b1.png align="center")

# Conclusion

In conclusion, the virtual DOM is a powerful concept that enables React to optimize the rendering process of components. By creating a lightweight replica of the actual DOM, React can efficiently update and re-render components based on state changes, without having to rebuild the entire DOM tree. The virtual DOM also allows for efficient and accurate diffing of components, which helps to minimize the number of DOM operations and improve the overall performance of the application. Additionally, understanding the concept of the virtual DOM is essential for anyone working with React, as it is a fundamental building block of the library. The virtual DOM is different from the shadow DOM, which is a web component technology that allows for the encapsulation of DOM and styles. Understanding the differences between these technologies can help developers choose the best solution for their projects. Stay tuned for more blogs!