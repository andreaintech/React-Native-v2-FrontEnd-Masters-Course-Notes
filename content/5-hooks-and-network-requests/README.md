## Hooks and Network Requests

### useState, useCallback, useEffect
React hooks were added to React in v16.8.0 and React Native in v0.59. Hooks are a built in system for managing state and side-effects in function components. The introduction of hooks was incredibly exciting for the community. Before hooks the only way to do anything even mildly complicated like save component state or make a network request required a class component, or setting up redux and thunks or sagas. This is no longer the case! A lot of modern React and React Native applications are written using just function components and React hooks!

Hooks in React Native work exactly the same as in plain React, so if you already know about hooks, you're good to go! Refer to the [React documentation](https://reactjs.org/docs/hooks-intro.html) on hooks for more info.

For the majority of use-cases, the only hooks you will need are ```useState```, ```useCallback``` and ```useEffect```. Let's look into these in detail.

#### ```useState```

[useState](https://reactjs.org/docs/hooks-state.html) is for saving and updating state inside the component.

```
import React, { useState } from 'react';

const [value, setValue] = useState(0);
```

Hooks are placed *inside* the component, as high as possible, always above the ```return``` statement. The ```useState``` hook returns an array of two items which you can name whatever you want: the first one is the current value of the item you're saving, and the second is a function that allows you to update the value. Although you can choose any name you like for these functions, by convention they are named ```varName``` and ```setVarName``` as seen in ```[value, setValue]```, ```[colour, setColour]``` etc. Following this convention improves your code readability by immediately signalling to yourself and other developers that this is a React ```useState``` hook so it is recommended to name accordingly unless you have a specific reason not to. Finally, the ```0``` we passed in is the initial value for our ```value```. This is optional and will default to *undefined*.

In order to update this value, we simply call ```setValue``` with the new value. This will update ```value``` to reflect the new value, cause a re-render of the component and your UI will reflect the new state.

There are two ways to update the value: 

1. Pass in a function which accepts the current value and returns the next value:

```
setValue(currentValue => currentValue + 1);
```

Or set the value directly without any reference to the current value:

```
setValue(1);
```

🔍 [useState example](https://snack.expo.dev/@kadikraman/usestate-example)

#### ```useCallback```

[useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback) is for any kind of action you may want to perform: be it a state update, a network request or launching a modal.

In our counter example before, we pass in the ```onPress``` function for incrementing and decrementing the counter directly. It's not so much of a problem, but it might get hard to read if the function was longer. So ideally we'd like to extract the ```handleIncrement``` and ```handleDecrement``` functions from the render method, like so:

```
const handleIncrement = () => setCount(current => current + 1);
const handleDecrement = () => setCount(current => current - 1);

<TouchableOpacity onPress={handleIncrement}>

<TouchableOpacity onPress={handleDecrement}>
```

This works, but the problem is that the constants for ```handleIncrement``` and ```handleDecrement``` get re-initialized every time the component re-renders, and because React is built to be dynamic, this happens *a lot*. ```useCallback``` to the rescue!

```
import React, { useCallback } from 'react';

const handleIncrement = useCallback(() => {
  setCount(current => current + 1);
}, []);
```

This may be a bit hard to read at first, but you'll soon get used to it. ```useCallback``` is a function that takes two arguments: the function we want to return (notice this is *exactly* the function we had before), and an array of values that should trigger the function to be re-initialized. In our case, this array is empty, because the ```useState``` function is the same, and we're not using any other outside variables inside the ```useCallback```. As a rule of thumb, any variables used inside the ```useCallback``` should be added to the array.

🔍 [useCallback example](https://snack.expo.dev/@kadikraman/usecallback-example)

#### ```useEffect```

[useEffect](https://reactjs.org/docs/hooks-effect.html) is tied to the component render cycle. If you're already familiar with React Components, you can think of this as a combined ```componentDidMount``` and ```componentDidUpdate```.

There are two main types of use-cases for ```useEffect```: ones that require cleanup and ones that don't.

```
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, status => setIsOnline(status.isOnline);

  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, []);
```

This bit of example code shows how you might subscribe to a chat API. Notice that the function body does the subscription, and the return value is a function that removes the subscription. Any function you return from a ```useEffect``` will be run when the component is unmounted. This is important to keep in mind to prevent memory leaks.

The other use-case is similar to the above, but for actions that do not require cleanup.

```
useEffect(() => {
  someActionWeNeedToDoOnce();
}, []);
```

The above code will only be executed once when the component is rendered and never again.

Note that the second argument to ```useEffect``` is an array of items that should trigger the effect to run again (the same as the second argument for ```useCallback```). The second argument is optional, but if it is not provided it will run on every component render. If you want to run the effect only on component load (equivalent to ```componentDidMount``` in a React class component), provide an empty array ```[]```. You should be especially careful about making sure you pass in the empty array when making network requests that trigger a component re-render otherwise you'll end up in an infinite loop!

🔍 [useEffect example[(https://snack.expo.dev/@kadikraman/useeffect-example)

☝️ you should run this on your phone or the in-browser emulator or you'll get CORS errors. In this example we do a network request to fetch some random cat facts when the component is rendered.

### Network Requests Exercise 📝

Update your application to fetch the color palettes from the following url: https://color-palette-api.kadikraman.now.sh/palettes

Hint: you should use ```useEffect```, ```useCallback``` and ```useState``` for this!

### Network Requests Exercise Solution 👀

🔗 [Expo 7d9e2920cce72f29547d8f6b113a31dac44da696](https://github.com/kadikraman/AwesomeProjectExpo/commit/7d9e2920cce72f29547d8f6b113a31dac44da696)

🔗 [RN 6cbb5e4895a2c8e65928cf998865a5d1062bc6bc](https://github.com/kadikraman/AwesomeProjectRN/commit/6cbb5e4895a2c8e65928cf998865a5d1062bc6bc)

👩‍💻 [Live Coding 58cae1baaa963249697ac3f30d457e0ab1a8f635](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/58cae1baaa963249697ac3f30d457e0ab1a8f635)

In this exercise, we've used all 3 hooks we just learnt about!

```
const [palettes, setPalettes] = useState([]);

const handleFetchPalettes = useCallback(async () => {
  const response = await fetch(URL);
  if (response.ok) {
    const palettes = await response.json();
    setPalettes(palettes);
  }
}, []);

useEffect(() => {
  handleFetchPalettes();
}, []);
```

First, we initialise a ```useState``` with an empty array to store the fetched color palettes. Make sure to also update the FlatList data prop to use the new ```palettes``` variable.

Then we create the actual function that does the network request. The ```fetch``` keyword works in React Native the same way it does on the web (with the exception that you can't get CORS errors). We fetch the data from the api, check that we received a non-error response, and save the response to the ```palettes``` variable which will automatically update out UI.

Finally, we add a ```useEffect``` which will trigger the ```handleFetchPalettes``` function when the component is first rendered.

### Pull to refresh

##### *[Forms →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/6-forms/README.md#forms)*
