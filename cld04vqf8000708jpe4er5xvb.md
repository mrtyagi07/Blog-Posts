# Become a Hooks Pro Part-2: A Hands-on Guide to useRef and useMemo in React

Part 1 can be found here if you haven't read it yet

%[https://vaibhavtyagi.hashnode.dev/become-a-hooks-pro-a-hands-on-guide-to-usestate-and-useeffect-in-react] 

# useRef:

## Basic

`useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

```javascript
const ref = useRef(initialValue)
```

The `ref` variable will be an object with a `current` property that is set to "initial value".

It's worth noting that the `initialValue` argument is optional, if you don't provide an initial value, the `current` property will be `undefined` initially. This is because the `useRef` hook doesn't set a default value like `useState` does.

## Dive deeper

The `useRef` hook in React is used to access and manipulate the DOM or other elements outside of the React component's rendered output. It creates and returns a reference object, which can be used to store a value or a reference to an element in the DOM, and this value will persist across re-renders of the component.

```javascript
import { useRef } from 'react';

function Example() {
  const inputRef = useRef(null);
  console.log(inputRef);//{current: null}

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <>
      <input type="text" ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </>
  );
}
```

In this example, we're using `useRef` to create a reference to an input element. The `useRef` hook is called in the component's body and it returns an object with a single property called `current`. Initially, the `current` property is set to `null`, but we can assign it a value later on.

We're then passing the `inputRef` object as a `ref` prop to the input element, this way React can associate the input element with the `inputRef` object. By doing so, we can access the input element later on by calling `inputRef.current`.

We also have a button that when it's clicked, it calls the `handleClick` function, inside this function we are using the `current` property to call the focus method of the input element, this way when the button is clicked the input will be in focus.

<mark>It's important to note that the useRef hook doesn't cause a re-render when the value of the current property changes, it's used to retain the values across re-renders.</mark>

Also, it's important to notice that the `useRef` hook can be used to store references to any type of value, not only DOM elements, you can use it to store references to any type of object, like a web worker, a timer, a network connection and more.

### Example

%[https://codesandbox.io/embed/compassionate-cookies-2yh3vt?fontsize=14&hidenavigation=1&theme=dark] 

The component renders a button with an onClick event that calls the `handleClick` function. The function updates the current value of the ref object by adding 1 to it, and then it shows an alert message displaying the number of clicks. The button also displays the current value of the ref object.

<mark>Observe carefully</mark> when you click on a button, it will never display a new value on the button; that's where the two pitfall lies, and what you should know before using useRef:

1. 🚩 Don't write a ref during rendering
    
    ```javascript
    myRef.current = 173;
    ```
    
2. 🚩 Don't read a ref during rendering
    
    ```javascript
    <button onClick={handleClick}>
         {ref.current} Click me!
        </button>
    ```
    

You can read or write refs **from event handlers or effects instead**.

1. ✅ **effects**
    

```javascript
 useEffect(() => {
    // ✅ You can read or write refs in effects
    myRef.current = 173;
  });
```

1. ✅ Event Handlers
    
    ```javascript
     function handleClick() {
        // ✅ You can read or write refs in event handlers
        doSomething(myOtherRef.current);
      }
    ```
    

<mark>It's important to note that useRef is not reactive, meaning that if the value stored in a ref changes, it doesn't trigger a re-render of the component, so it should be used only when you need to store a value that doesn't change often.</mark>

# useMemo

## Basic

`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```javascript
const cachedValue = useMemo(calculateValue, dependencies)
```

This is the basic syntax for using the `useMemo` Hook. The first argument passed to useMemo is the function that performs the calculation, and the second argument is an array of dependencies. The result of the calculation will be cached and returned by useMemo. If any of the dependencies change, the calculation will be run again and the result will be cached again.

## Dive deeper

`useMemo` is a React hook that allows you to memoize a value. This means that the value is only recalculated if one of the dependencies has changed. This can be useful for performance optimization, as it allows you to avoid unnecessary re-rendering of a component.

For example, if you have a component that performs a complex calculation each time it renders, you can use `useMemo` to memoize the result of that calculation. This way, if the component's props or state do not change, the result of the calculation will be reused, and the component will not need to perform the calculation again.

```javascript
import { useMemo } from 'react';

function MyComponent({ data }) {
  const memoizedValue = useMemo(() => {
    // Perform a complex calculation with data
    return someCalculation(data);
  }, [data]);

  return <div>{memoizedValue}</div>;
}
```

In this example, the useMemo hook is used to memoize the result of the `someCalculation` function, which is passed the `data` prop as an argument. The hook takes a function as its first argument and an array of dependencies as its second argument. The dependencies in this case is `data` props.

In this way, React will only call the `someCalculation` function and update the `memoizedValue` when the `data` prop changes. If the `data` prop does not change, the previous result will be used, and the component will not need to perform the calculation again.

### Usage

`useMemo` is commonly used in performance-sensitive components that need to compute derived data based on props or state. A common example is a component that renders a large table or list, where the rows are built from a large dataset that is passed as props. Without useMemo, the component would need to re-compute the rows every time the component re-renders, even if the dataset hasn't changed.

Using `useMemo` to memoize the calculation of the rows means that the component only re-computes the rows if the dataset has changed, resulting in a significant performance boost.

**Example 1 :**

```javascript
import { useMemo } from 'react';

function Table({ data }) {
  const rows = useMemo(() => {
    // Calculate the rows for the table based on the data
    // This calculation could be expensive, so we only want to do it if the data has changed
    return data.map(item => (
      <tr key={item.id}>
        <td>{item.name}</td>
        <td>{item.age}</td>
        <td>{item.address}</td>
      </tr>
    ));
  }, [data]);

  return (
    <table>
      <tbody>{rows}</tbody>
    </table>
  );
}
```

In this example, the component will only re-calculate the rows if the data prop changes. This can be a big performance boost if the data prop is large and the calculation of the rows is expensive.

useMemo is important for performance optimization as it allows to avoid unnecessary re-renders and calculations if the data is not changed. <mark>It is especially useful in cases where the component is rendering a large amount of data and the calculation of that data is expensive.</mark> By memoizing the calculation, we can ensure that the component is only re-calculating when it needs to, which can greatly improve the performance of the application.

**Example 2 :**

%[https://codesandbox.io/embed/vigorous-faraday-vlg83x?fontsize=14&hidenavigation=1&theme=dark] 

In this example, the expensiveCalculation function is only called when the values of `a` and `b` change. Without useMemo, this function would be called on every render, causing a significant performance hit. By caching the result of the calculation with useMemo, we ensure that the calculation is only performed when necessary.

**<mark>By default, when a component re-renders, React re-renders all of its children recursively.</mark>**

This can be inefficient if the children are expensive to render, or if they don't need to change.

For example, consider a component that renders a list of items. Each item has a title and a description. The title is passed in as a prop, but the description is calculated based on the title.

```javascript
function Item({ title }) {
  const description = useMemo(() => calculateDescription(title), [title]);
  
  return (
    <div>
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  );
}
```

In this example, the `calculateDescription` function is a relatively expensive operation. If the parent component re-renders and passes a new title prop to the `Item` component, React will re-render the `Item` component and call `calculateDescription` again.

By wrapping the `calculateDescription` call in a `useMemo` hook, we can tell React to only re-run the function and re-render the component if the `title` prop has changed. This can improve the performance of our application.

It's important to note that `useMemo` only applies to a component's own render, not to the renders of its children. <mark> If a component using useMemo re-renders and the memoized value changes, all its children will re-render as well.</mark>

### **Memoizing a dependency of another Hook**

```javascript
import { useMemo } from 'react';

function MyComponent({ data, filter }) {
  // Create the filter object directly in the component body
  const filterOptions = {
    name: filter.name,
    age: filter.age,
  };

  // Use the filterOptions object as a dependency for useMemo
  const filteredData = useMemo(() => {
    // Perform the filtering calculation
    return data.filter(item => {
      return item.name === filterOptions.name && item.age === filterOptions.age;
    });
  }, [data, filterOptions]);// 🚩 Caution: Dependency on an object created in the component body

  return (
    <div>
      {filteredData.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
}
```

In this example, the `filterOptions` object is created directly in the component body and is used as a dependency for the `useMemo` hook. This can cause unnecessary re-renders because the `filterOptions` object will be different on every re-render. A better approach would be to extract the creation of the `filterOptions` object into a separate function that is only called when the filter values actually change, and use the returned object as the dependency for the `useMemo` hook.

```javascript
function createFilterOptions(filter) {
  return {
    name: filter.name,
    age: filter.age,
  };
}

function MyComponent({ data, filter }) {
  const filterOptions = useMemo(() => createFilterOptions(filter), [filter]);

  const filteredData = useMemo(() => {
    return data.filter(item => {
      return item.name === filterOptions.name && item.age === filterOptions.age;
    });
  }, [data, filterOptions]);//// ✅ Only changes when filterOptions or data changes


  return (
    <div>
      {filteredData.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
}
```

This way, the filterOptions object is only recreated when the filter values change, and the filteredData calculation will only re-run when the data or filterOptions change.

# Conclusion

In conclusion, React hooks have revolutionized the way we think about and write React components. The useRef and useMemo hooks are just as powerful as useState and useEffect. The useRef hook allows us to create references to DOM nodes, making it easy to access and manipulate them directly. The useMemo hook enables us to cache the results of calculations, helping us to optimize our components' performance by only recalculating when necessary. With a deeper understanding of these hooks, we can write more efficient and maintainable code. In my next blog, I will delve deeper into the world of React hooks and explore some of the other important hooks that are available to us. Stay tuned for more insights on the power of React hooks!