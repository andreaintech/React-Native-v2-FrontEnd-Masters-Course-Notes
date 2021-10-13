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

- [View style props](https://reactnative.dev/docs/view-style-props)
- [Text style props](https://reactnative.dev/docs/text-style-props)
- [Image style props](https://reactnative.dev/docs/image-style-props)

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

To center all content in a container vertically, we can use ```justifyContent: 'center'```. We'll also have to use ```flex: 1``` to ensure the component takes up the whole height of the screen. If the component is nested inside another component, you'll have to make sure the other component also has ```flex: 1```:

```
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
  },
});
```

#### Styles without StyleSheet

You should always aim to write your styles in a StyleSheet, but sometimes it's not possible or just sub-optimal. For example if you had to add styles dynamically. In this case, we can pass styles into the component as plain objects like so:

```
<View style={{ backgroundColor: 'teal' }} />
```

Notice the double braces? The first set of braces is to tell JSX we're passing in an object and the second is for the actual object. This is equivalent:

```
const componentStyle = { backgroundColor: 'teal' };

<View style={componentStyle} />;
```

#### Multiple styles in one component

Sometimes you may want to add multiple style objects to one element. You can do this by passing in an array of styles instead of a single style like so:

```
<View style={[styles.firstStyle, styles.secondStyle]} />
```

The styles cascade as they would on the web, so the later styles would override the former if there are any repeats.

You can also mix ```StyleSheet``` styles and object styles:

```
<View style={[styles.firstStyle, { backgroundColor: 'teal' }]} />
```

#### Side note: Styled Components

If you are a fan of styled components, you might be excited to know that they have React Native support! Styling native elements looks pretty much the same as on the web, only instead of:

```
import styled from 'styled-components';

const StyledDiv = styled.div`
  background-color: lavender;
`;
```

You'll have to do:

```
import styled from 'styled-components/native';

const StyledView = styled.View`
  background-color: lavender;
`;
```

Otherwise the experience is exactly the same! You can even use ```snake-case``` like on the web! For this workshop, we will use ```StyleSheet```, but feel free to explore this in your own time. Read more about it [here](https://styled-components.com/docs/basics#react-native).

### Styling Exercise 📝

The best way to learn is by doing so let's start off by adding some colour. Here's a little app I built, showcasing come of my favourite colours. Try to recreate it!

Here are the colours I used:

```
Cyan: #2aa198
Blue: #268bd2
Magenta: #d33682
Orange: #cb4b16
```

![image](https://user-images.githubusercontent.com/20091777/137065168-421d6ff5-ba0f-443d-bedc-8a5a54e268dd.png)

![image](https://user-images.githubusercontent.com/20091777/137065182-4b1f3099-4235-4ac4-a200-448fd4c8e075.png)

### Styling Exercise Solution 👀

🔗 [Expo b12c0f43f24a77c62699e216705d5311ac8e942d](https://github.com/kadikraman/AwesomeProjectExpo/commit/b12c0f43f24a77c62699e216705d5311ac8e942d)

🔗 [RN df8184f4c4d0695a683df85009b4e808cad4cc5d](https://github.com/kadikraman/AwesomeProjectRN/commit/df8184f4c4d0695a683df85009b4e808cad4cc5d)

👩‍💻 [Live Coding a684004b411015049c2ccbaf5abca3b28cd93cd6](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/a684004b411015049c2ccbaf5abca3b28cd93cd6)

The first thing you'll want to do is add some padding to the container. Let's to 50 from the top and 10 from the sides:

```
const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    paddingHorizontal: 10,
  },
});
```

Now it's time to add the new text. Since we already have some text on the page, we can do this by replacing the copy for our "Hello, world!" message and adding the style:

```
// replace "hello world" text and add style prop

<Text style={styles.heading}>Here are some boxes of different colours</Text>
```

```
// place this in the stylesheet, under the container style

heading: {
  fontSize: 18,
  fontWeight: 'bold',
  marginBottom: 10,
}
```

Now for lets add a box for cyan. For this we need to add a new ```View``` and a ```Text``` with styles. Remember we'll have to use flex to position the text inside the boxes!

```
<View style={styles.cyanBox}>
  <Text style={styles.text}>Cyan #2aa198</Text>
</View>
```

```
text: {
  fontWeight: 'bold',
  color: 'white'
},
cyanBox: {
  padding: 10,
  borderRadius: 3,
  justifyContent: 'center',
  alignItems: 'center',
  marginBottom: 10,
  backgroundColor: '#2aa198'
}
```

Looking good! Let's add the blue box as well. Your ```App.js``` now looks something like this:

```
// App.js

import React from 'react';
import { View, Text, SafeAreaView, StyleSheet } from 'react-native';

const App = () => {
  return (
    <SafeAreaView>
      <View style={styles.container}>
        <Text style={styles.heading}>
          Here are some boxes of different colours
        </Text>
        <View style={styles.cyanBox}>
          <Text style={styles.text}>Cyan #2aa198</Text>
        </View>
        <View style={styles.blueBox}>
          <Text style={styles.text}>Blue #268bd2</Text>
        </View>
      </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    paddingHorizontal: 10,
  },
  heading: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  text: {
    fontWeight: 'bold',
    color: 'white',
  },
  cyanBox: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
    backgroundColor: '#2aa198',
  },
  blueBox: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
    backgroundColor: '#268bd2',
  },
});

export default App;
```

This is looking good, but you might have noticed there are a lot of repeated styles between the two boxes and this can get cumbersome pretty quickly. Lets break these out and use the style array instead:

```
<View style={[styles.box, styles.cyan]}>
    <Text style={styles.text}>Cyan #2aa198</Text>
</View>
<View style={[styles.box, styles.blue]}>
    <Text style={styles.text}>Blue #268bd2</Text>
</View>
```

```
box: {
  padding: 10,
  borderRadius: 3,
  justifyContent: 'center',
  alignItems: 'center',
  marginBottom: 10,
},
cyan: {
  backgroundColor: '#2aa198'
},
blue: {
  backgroundColor: '#268bd2'
},
```

Finally add boxes for the remaining colours (magenta and orange) the same way, and we're all done!

### Components

React (Native) is a component-based framework. This means that your app is made from lots of components that are nested within each other. You always have one root component (in our case it is our App component), but inside it we can have as many big or small components as we'd like.

It's generally a really good practice to break your app into components and to make the components as small and standalone as possible. This is handy because:


1. It promotes component reuse - you've already built a button once. Why not reuse it?
2. Easier to follow - no one wants to debug a 1000 line component if they can help it
3. Easier to test - the smaller the unit, the easier it is to unit test!

Look at the app we're built so far. Can you see something that could be extracted into a component and reused? I can! The coloured boxes are a great candidate.

Lets start by creating a new folder called ```components``` in the root level of your project directory. Generally it is a good practice to have one component per file, so we'll do that.

Inside your ```components``` directory, create a new file called ```ColorBox.js``` and open it.

Let's add some code to display the box on the screen:

```
// components/ColorBox.js

import React from 'react';
import { View, Text } from 'react-native';

const ColorBox = () => {
  return (
    <View>
      <Text>I am a color box!</Text>
    </View>
  );
};

export default ColorBox;
```

But nothing is appearing in our app. That's because we need to import this new component into our ```App.js``` and add it to our code.

Open the ```App.js``` and add the new ColorBox component just inside the last view, under the last existing coloured box:

```
// App.js

import ColorBox from './components/ColorBox';

// add this in a new line, just before the last </View>
<ColorBox />;
```

Now you should be able to see the text "I am a color box" in your app just under the last box!

🔗 [Expo 15c2fda13a771ddb0923ebf536c493fbc32d6f90](https://github.com/kadikraman/AwesomeProjectExpo/commit/15c2fda13a771ddb0923ebf536c493fbc32d6f90)

🔗 [RN 19af3bead2ec10cb93c96f3805590ee38c3a434c](https://github.com/kadikraman/AwesomeProjectRN/commit/19af3bead2ec10cb93c96f3805590ee38c3a434c)

#### Props

In order for our new ColorBox component to be able to reused for different colours, we'll need to somehow dynamically set its colour. To do this, we can use ```props```. Props is short for properties and is basically a way to pass information down the component tree.

Our color box will need to know two things - the name of the color and the hex code. Let's start with cyan and add these props to the ```<ColorBox>``` component in ```App.js```:

```
// App.js

<ColorBox hexCode="#2aa198" colorName="Cyan" />
```

These props are now available to ColorBox. Let's open ColorBox again and display the name of the color dynamically:

```
// components/ColorBox.js

const ColorBox = props => {
  return (
    <View>
      <Text>
        {props.colorName} {props.hexCode}
      </Text>
    </View>
  );
};
```

Notice that we have to use braces ```{}``` around variables in order to display them inside Text. This is so React Native can distinguish between plain text and variables that should be evaluated.

Last thing we'll need to do is style the box! Remember that we can pass in an array to the ```style``` prop to add multiple styles!

```
// components/ColorBox.js

import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const ColorBox = props => {
  const colorStyle = {
    backgroundColor: props.hexCode,
  };

  return (
    <View style={[styles.box, colorStyle]}>
      <Text style={styles.text}>
        {props.colorName} {props.hexCode}
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  box: {
    padding: 10,
    borderRadius: 3,
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: 10,
  },
  text: {
    fontWeight: 'bold',
    color: 'white',
  },
});

export default ColorBox;
```

Finally, replace update all the existing colour boxes to use our new component and remove unused code, and we're done! The app looks the same, but our code is a whole lot cleaner.

🔗 [Expo 51f04c9bd3d42d7518882686c0593156dd1773ac](https://github.com/kadikraman/AwesomeProjectExpo/commit/51f04c9bd3d42d7518882686c0593156dd1773ac)

🔗 [RN a4ed9cd18fc164c560d3537f82c9a94d17c91441](https://github.com/kadikraman/AwesomeProjectRN/commit/a4ed9cd18fc164c560d3537f82c9a94d17c91441)

👩‍💻 [Live Coding 6266918a02853bbbc0c61a62a44531d041d7690f](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/6266918a02853bbbc0c61a62a44531d041d7690f)

### Lists

What if instead of 4 colors, we had 10 or even 100? How would we display them then? If you're already familiar with React, you might be tempted to add all the colors in an array and .map over them. This is a very common mistake for newcomers to React Native. While it may be fine to do on the web, in React Native you should avoid using map in the render. This is because mapping over an array is not optimized. React Native will attempt to render every single element in the array all at once, regardless of whether they are visible on the screen or not.

There are special components in React Native for rendering lists: these are [FlatList](https://reactnative.dev/docs/flatlist) and [SectionList](https://reactnative.dev/docs/sectionlist).

#### FlatList

FlatList has a whole bunch of configuration options, but the minimum you will need to give it is 3 props:

- data - this is the array of data you want to map over.
- renderItem - this is a function that is passed the item and its index and will return the individual item component.
- keyExtractor - this is a function that gets passed an item and its index.

🔍 [FlatList example](https://snack.expo.io/@kadikraman/flatlist-example)

In this FlatList example, you'll see an array of foods being displayed using a FlatList.

#### SectionList

SectionList is a similar to FlatList, but it allows you to render items in sections with a header item between. The data for the SectionList is still an array, but each array item will need to be an object with a title (a string) and a data (an array) prop.

Additionally you can pass in a prop called ```renderSectionHeader``` which will let you render the title for each section.

🔍 [SectionList example](https://snack.expo.io/@kadikraman/sectionlist-example)

This is incredibly powerful and provides a really nice native experience for the user on the device.

#### List props

The list elements have a bunch of built in properties to help customize for your experience. Check out the [FlatList](https://reactnative.dev/docs/flatlist) and [SectionList](https://reactnative.dev/docs/sectionlist) docs for all of them. Here are some I tend to use most often:

- [ItemSeparatorComponent](https://reactnative.dev/docs/flatlist#itemseparatorcomponent) - renders a custom separator between your items. Handy if you have to e.g. render a line or even something dynamic instead of building it into the list items.
- [ListEmptyComponent](https://reactnative.dev/docs/flatlist#listemptycomponent) - this is rendered when the ```data``` is an empty array or undefined. Saves you from doing conditional rendering manually!
- [ListFooterComponent](https://reactnative.dev/docs/flatlist#listfootercomponent) - renders something at the bottom of the list.
- [ListHeaderComponent](https://reactnative.dev/docs/flatlist#listheadercomponent) - renders something at the top of the list.
- [extraData](https://reactnative.dev/docs/flatlist#extradata) - the list only gets re-rendered if the ```DATA``` changes. It might happen though that what you display depends on some external factors. In this case use the ```extraData``` to pass in any variables that should also trigger a re-render when changed.
- [horizontal](https://reactnative.dev/docs/flatlist#extradata) - render the list horizontally instead of vertically.
- [numColumns](https://reactnative.dev/docs/flatlist#extradata) - render multiple columns.
- [onEndReached](https://reactnative.dev/docs/flatlist#extradata) - fires when the user has scrolled to the end of the list. Handy for pagination.

### Lists Exercise 📝

You might have already recognized the colours we were using earlier. They are part of the [Solarized](https://en.wikipedia.org/wiki/Solarized_(color_scheme)) color scheme by Ethan Schoonover. The colour palette actually contains 16 colours and next up, we'd like to display them all:

```
const COLORS = [
  { colorName: 'Base03', hexCode: '#002b36' },
  { colorName: 'Base02', hexCode: '#073642' },
  { colorName: 'Base01', hexCode: '#586e75' },
  { colorName: 'Base00', hexCode: '#657b83' },
  { colorName: 'Base0', hexCode: '#839496' },
  { colorName: 'Base1', hexCode: '#93a1a1' },
  { colorName: 'Base2', hexCode: '#eee8d5' },
  { colorName: 'Base3', hexCode: '#fdf6e3' },
  { colorName: 'Yellow', hexCode: '#b58900' },
  { colorName: 'Orange', hexCode: '#cb4b16' },
  { colorName: 'Red', hexCode: '#dc322f' },
  { colorName: 'Magenta', hexCode: '#d33682' },
  { colorName: 'Violet', hexCode: '#6c71c4' },
  { colorName: 'Blue', hexCode: '#268bd2' },
  { colorName: 'Cyan', hexCode: '#2aa198' },
  { colorName: 'Green', hexCode: '#859900' },
];
```

You should be using FlatList for this.

For extra credit - also display the name of the color in white on the darker colors and in black on the lighter ones!

![image](https://user-images.githubusercontent.com/20091777/137172600-76661b40-0384-42a7-b6df-015e9061f65a.png)

![image](https://user-images.githubusercontent.com/20091777/137172615-fecf98e4-89ca-4bcb-885a-b3580b6e1f1b.png)

### Lists Exercise Solution 👀

🔗 [Expo ed604b55573dbf95c2090ee34b6672fcc3fb05df](https://github.com/kadikraman/AwesomeProjectExpo/commit/ed604b55573dbf95c2090ee34b6672fcc3fb05df)

🔗 [RN 98c2e0bf744c42290c39b94afbed70db351e0de4](https://github.com/kadikraman/AwesomeProjectRN/commit/98c2e0bf744c42290c39b94afbed70db351e0de4)

👩‍💻 [Live Coding cb8f698fefdffb4564384638643448c21e7ddfe8](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/cb8f698fefdffb4564384638643448c21e7ddfe8)

In this solution we're removed the individual ```ColorBox```es and rendered them all using a ```FlatList```. Some things to note:

- Since we no longer have a containing ```View```, we not pass in the component styles into the ```FlatList``` component instead. Almost all native components in React Native can by styled using the style prop.
- Notice that the name of the palette scrolls with the colors. This is because we added it to FlatList using the ```ListHeaderComponent``` prop.
- We've used a little calculation to adjust text colour for the background colour. There are better algorithms to do this, but this is definitely the shortest: ```parseInt(props.hexCode.replace('#', ''), 16) > 0xffffff / 1.1```. Here we essentially get the lightest 10% of the background colors and display black text for these, and white for the rest.

##### *[Navigation Intro →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/4-navigation/README.md#navigation)*
