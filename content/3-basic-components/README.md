## Basic Components

### Basic React Native components
If you're already familiar with React then you've got a head start, lucky you! Before we dive into React Native, let's start by looking at this "hello world" React component:

```
// App.js

import React from 'react';

const App = () => {
  return <div>Hello, world!</div>;
};

export default App;
```

This is a minimal React component. If you're used React before, this will be familiar to you. If not, let's talk through what's going on here.

React uses what they call JSX as syntax sugar for displaying components. JSX stands for "JavaScript and XML", and although XML is quite dated, it really works out for React, because the XML syntax looks very similar to HTML! The bonus is that we can do JavaScript around it.

At the top of the file we have an import statement - ```import React from 'react';``` - though ```React``` is not used in the file. This is because ```React``` is needed for the JSX. As a rule of thumb, if the file includes any components with braces (```<>```) you'll need to import React.

Now let's look at a corresponding React Native component:

```
// App.js

import React from 'react';
import { View, Text } from 'react-native';

const App = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};

export default App;
```

There are a couple of important differences here. We can't use ```div```, ```span```, ```p``` or other html elements in React Native. Instead, we have special native components. The notable difference is that you have to import these components from ```react-native``` rather than just having them built into jsx.

- ```<View>``` - if you're already familiar with web development, you can think of ```<View>``` as a native equivalent to ```<div>```. It's a container to use for styling and positioning the elements within.
- ```<ScrollView>``` - pages do not scroll by default. If you have lots of content to display, you can use a ```ScrollView```

- ```<Text>``` - the ```<Text>``` component is used for displaying, you guessed it, text! In React Native, all text you want to display must be contained in ```<Text>``` tags or you'll have errors.

Now that we've got some components to work with - let's get coding!

#### Basic Components and SafeAreaView

Open your ```App.js```, delete the content and replace it with our "Hello, World" template.

```
// App.js

import React from 'react';
import { View, Text } from 'react-native';

const App = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};

export default App;
```

How does it look? Not great I imagine. You might notice that the text is overlaid by the notification bar at the top of the screen. You could add some padding to the top of the screen, but that wouldn't serve for a general solution - while it might work for the phone you're testing on for the moment, there are tends of iPhones and hundreds of Android phones with different specs.

Thankfully there is something handy built into React Native to help with this. ```SafeAreaView``` is a component that automatically adds the necessary padding around your content to ensure that you don't overlap with the top and bottom of the screen. This was especially handy when iPhone X came out, as it handles the bottom spacing necessary for the notch.

All you need to do is to import the ```SafeAreaView``` from ```react-native``` and wrap your content around it like so:

```
// App.js

import React from 'react';
import { View, Text, SafeAreaView } from 'react-native';

const App = () => {
  return (
    <SafeAreaView>
      <View>
        <Text>Hello, world!</Text>
      </View>
    </SafeAreaView>
  );
};

export default App;
```

Now you can be confident your content will be visible regardless of the device.

🔗 [Expo 49584b83f6871b73bd3fc6219db048e0875e8f53](https://github.com/kadikraman/AwesomeProjectExpo/commit/49584b83f6871b73bd3fc6219db048e0875e8f53)

🔗 [RN 43e1c4d6ae62f4befb51857fa4b95b1c14ddd3de](https://github.com/kadikraman/AwesomeProjectRN/commit/43e1c4d6ae62f4befb51857fa4b95b1c14ddd3de)

### Styling

In React Native, all styling is done using inline styles. We use a ```StyleSheet``` from ```react-native``` to create the styles. Usually we add this styles constant at the bottom of the file, or in a separate file:

```
const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
});
```

React Native styles are actually very similar to css styles on the web. The debugger also displays helpful error messages when you try to add styles that don't exist on a particular component type.

```StyleSheet.create``` creates an optimized style object where you can access the individual styles like on a regular object. In this case, ```styles.container``` would give you all the container styles. Now we can use this style prop inside our JSX by passing it into the relevant element:

```
<View style={styles.container}>
  <Text>Hello, world!</Text>
</View>
```

This is pretty similar to the styles on the web, only we omit the units (```px```, ```em```, ```rem``` etc), because all dimensions in React Native are unitless, and represent density-independent pixels.

Adding a background colour for the component while your debugging can help understand positioning. We could add a background color using the ```backgroundColor``` property:

```
const styles = StyleSheet.create({
  container: {
    backgroundColor: 'lavender',
    padding: 10,
  },
});
```

Note that all the web colors will work here, but we can also use hex ```#ffffff``` or rgb ```rgb(255,255,255)``` or rgba ```rgba(255,0,0,0.3)```.

Notice that the style names in React Native are in camelCase instead of kebab-case, but otherwise are the same as the web!

The style properties you can use depend on the component you're trying to style, and fall into 3 categories:

- [View style props]()
- [Text style props]()
- [Image style props]()

There are some special properties you might not have seen on the web. For instance, you will frequently find yourself applying the same padding or margin. There is a shorthand for it on the web where you can do ```margin: 10, 20```, but this won't fly here, since we use number, not strings. Instead, we can set the styles to be ```horizontal``` or ```vertical```. So instead of writing this:

```
const styles = StyleSheet.create({
  container: {
    paddingLeft: 10,
    paddingRight: 10,
    marginTop: 20,
    marginBottom: 20,
  },
});
```

We can write this:

```
const styles = StyleSheet.create({
  container: {
    paddingHorizontal: 10,
    marginVertical: 20,
  },
});
```

#### Positioning

In React Native, all positioning is done using FlexBox and all elements have ```display: flex``` applied by default. If you've not used flex much before it may seem a bit daunting, but the basics are not too tricky to grasp. If you have time, [FlexBox froggy]() is a fun little game that introduce you to the flex iteratively while you move frogs around the pond. For everyday reference [this guide]() from CSS Tricks is pretty handy.

Suppose we wanted to center all content in a container horizontally. For this, we can use ```alignItems: 'center```:

```
const styles = StyleSheet.create({
  container: {
    alignItems: 'center',
  },
});
```

### Styling Exercise 📝

### Styling Exercise Solution 👀

### Components

### Lists

### Lists Exercise 📝

### Lists Exercise Solution 👀
