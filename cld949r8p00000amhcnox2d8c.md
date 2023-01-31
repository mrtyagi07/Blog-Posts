# Creating a Dynamic GIF Search Experience with React and Tailwind

Welcome to my blog on creating a custom GIF search feature in React. In this blog post, I'll be using the [Giphy API](https://developers.giphy.com/) to access a vast collection of GIFs and integrate them into a React application.

Before we begin, you'll need to sign up for a Giphy API key. This key will be used to authenticate your requests to the Giphy API. Once you have your key, you're ready to start building your GIF search feature.

We'll be using React as our front-end framework and Tailwind CSS for styling. If you're not familiar with these technologies, don't worry - I'll provide all the necessary code and explain everything as we go along.

### Setup

Let's start by setting up a new React project and installing the necessary dependencies. In your terminal, run the following commands:(you can use whatever you want or CodesandBox)

```javascript
npx create-tw@latest
cd appname
yarn dev
```

With our project set up, we can now start building out our GIF search feature. We'll begin by creating a simple search bar that allows the user to input their search query. Next, we'll use the Giphy API to retrieve a list of GIFs that match the user's query. Finally, we'll display these GIFs in our application.

Throughout the tutorial, we'll be breaking down each step of the process, so you can follow along and build your GIF search feature.

So, let's begin!

### Let's create a simple search bar

```javascript
//App.jsx
<div>
 <input type="text" placeholder="LOL" />
      <button type="button">Search</button>
</div>
```

**Add Some Style to the search bar**

```javascript
//App.jsx
<div className="flex items-center border-b border-teal-500 py-2">
      <input
        className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
        type="text"
        placeholder="LOL"
      />
      <button
        className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
        type="button"
      >
        Search
      </button>
    </div>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674533460896/b4f34ad9-cb77-4450-9c46-dfbf137b80db.png align="center")

### Create a State for fetching input data entered by the user, a state for storing API data, and a method when the user clicks on the search button

```javascript
//App.jsx
const [input, setInput] = useState("");
const [data, setData] = useState([]);

  const handleSearch = () => {
    console.log(input);
  };
```

The initial value of the state variable is set to an empty string "" . This state variable will be used to store the value of the search input so that we can use it to make a request to the Giphy API later on.

**Now let's add onChnage and onClick on button**

```javascript
<div className="flex items-center border-b border-teal-500 py-2">
      <input
        className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
        type="text"
        placeholder="LOL"
        aria-label="gif"
        value={input}
        onChange={(e) => setInput(e.target.value)}
      />
      <button
        className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
        type="button"
        onClick={handleSearch}
      >
        Search
      </button>
    </div>
```

The input element has a `value` attribute that is set to the current value of the `input` state variable we defined earlier. It also has an `onChange` event handler that is set to a callback function which takes the event object as an argument, it then calls the `setInput` function that updates the state with the current value of the input field.

An `onClick` event handler that is set to a callback function named `handleSearch` which will be used to make the request to the Giphy API with the current value of the `input` state variable when the button is clicked.

### Let's add API fetching logic in our handleSearch

```javascript
 const handleSearch = () => {
    fetch(
      `https://api.giphy.com/v1/gifs/search?api_key=YOUR_KEY&q=${input}&limit=25&offset=0&rating=g&lang=en`
    )
      .then((res) => res.json())
      .then((data) => setData(data.data))
      .catch((err) => console.log(err));
  };
```

The function uses the `fetch` method to make a GET request to the Giphy API with the search query as part of the URL. The API key is also included in the URL, so the API can authenticate the request. The `q` parameter in the URL is used to specify the search query, and it's set to the current value of the `input` state variable. The `limit` parameter is used to specify the number of results that should be returned, `offset` parameter to specify the starting point of the result set, `rating` for filter the search by rating and `lang` for language of the results.

### Let's render API data on UI

After the Search button div add this.

```javascript
<div className="grid grid-cols-3 gap-4">
        {data?.map((el) => (
          <div
            key={el.id}
            className="max-w-sm rounded overflow-hidden shadow-lg"
          >
            <img
              className="w-full"
              src={el.images.original.url}
              alt="Sunset in the mountains"
            />
          </div>
        ))}
      </div>
```

It is using a JavaScript map method to iterate through the data returned from the API, which is stored in the `data` state variable. The map method is called on the `data` array and for each element in the array, it returns a new `div` element.

This code is responsible for displaying the GIFs returned from the API in a grid layout on the screen. The `key` attribute is used for performance optimization in React, it helps React to identify which items have changed, been added, or been removed.

### Putting it all together: The Complete Code for Building a Dynamic GIF Search

```javascript
import React, { useState } from "react";
import "./app.css";

const App = () => {
  const [input, setInput] = useState("");
  const [data, setData] = useState([]);

  const handleSearch = () => {
    fetch(
      `https://api.giphy.com/v1/gifs/search?api_key=YOUR_KEY&q=${input}&limit=25&offset=0&rating=g&lang=en`
    )
      .then((res) => res.json())
      .then((data) => setData(data.data))
      .catch((err) => console.log(err));
  };

  return (
    <>
      <div className="flex justify-center items-center p-8">
        <div className="flex items-center border-b border-teal-500 py-2">
          <input
            className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
            type="text"
            placeholder="LOL"
            aria-label="gif"
            value={input}
            onChange={(e) => setInput(e.target.value)}
          />
          <button
            className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
            type="button"
            onClick={handleSearch}
          >
            Search
          </button>
        </div>
      </div>
      
      <div className="grid grid-cols-3 gap-4">
        {data?.map((el) => (
          <div
            key={el.id}
            className="max-w-sm rounded overflow-hidden shadow-lg"
          >
            <img
              className="w-full"
              src={el.images.original.url}
              alt="Sunset in the mountains"
            />
          </div>
        ))}
      </div>
    </>
  );
};

export default App;
```

## Ready to Try? Play with the Live Version of the GIF Search Built in React

%[https://codesandbox.io/embed/gify-question-nh03k7?fontsize=14&hidenavigation=1&theme=dark] 

I hope that you found this blog helpful and were able to follow along to build your own custom GIF search feature. I also hope that you have learned a lot about how to use the Giphy API, React hooks, and Tailwind CSS to create a dynamic and interactive user interface.

Thank you for checking out this blog. If you have any further questions or want more information on this topic, please let me know. I would be happy to help!

In addition, Thanks for your time and patience in reading this blog. If you have any suggestions or feedback, I would be glad to hear from you. I hope you enjoyed building this feature and I would be excited to see what you will come up with next.