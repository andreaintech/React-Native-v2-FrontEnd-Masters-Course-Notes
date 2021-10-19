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

### Network Requests Exercise 📝

### Network Requests Exercise Solution 👀

### Pull to refresh

##### *[Forms →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/6-forms/README.md#forms)*
