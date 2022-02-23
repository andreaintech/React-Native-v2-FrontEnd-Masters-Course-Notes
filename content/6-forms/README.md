## Forms

### Overview of Forms in React Native 

Forms in React Native are just a collection of inputs. Whereas on the web we have a ```<form>``` element and a submit button, this is not the case in React Native. Let's looks at some of the inputs we have available.
  
#### TextInput

The [TextInput](https://reactnative.dev/docs/textinput) is probably the most common and frequently used text form in React Native. It is actually incredibly powerful and has a many important features.

🔍 [TextInput examples](https://snack.expo.dev/@kadikraman/textinput-example)

Here we have 4 examples of what you can do with TextInput:

##### Basic text input

The first input is a basic TextInput with no embellishments. We use 4 props:

- ```style``` - adding some padding and a border color for the input to be better visible on the screen. The Text Input has no default styles
- ```value``` - the current value
- ```onChangeText``` - gets called with the new value whenever the user changes the content of the input
- ```placeholder``` - some placeholder text to be displayed when the input is empty

##### Number input

Here we use an additional prop called ```keyboardType```. You can use [this prop](https://reactnative.dev/docs/textinput#keyboardtype) to define what type of input this is. Since we're working on phones, this will define what type of keyboard the user gets to work with.

The options that work on both iOS and Android are:

- default
- number-pad
- decimal-pad
- numeric
- email-address
- phone-pad

##### Password input

For password inputs we don't want to show what the user has types. For this we can use the ```secureTextEntry``` prop and set it to true (default is false). This ensures the input displays *** instead of the actual content.

##### Multiline input

For a multiline input, we use ```multiline={true}```. This will allow the input to grow infinitely. If we'd like to cap the height of the input on the page, we can also set it to a specific number of lines, e.g. 4 with ```numberOfLines={4}```.

##### Picker

The [Picker](https://reactnative.dev/docs/picker) component is an interesting one, because it's looks very different across platforms.

🔍 [Picker example](https://snack.expo.io/@kadikraman/picker-example)

![image](https://user-images.githubusercontent.com/20091777/138000556-2143a807-4e75-49e5-adc7-5b8ed28b1268.png)

![image](https://user-images.githubusercontent.com/20091777/138000568-bd3853fc-af57-4c63-bd34-5d2463422db8.png)

As you can see, the iOS picker is an inline wheel, and the Android picker is a modal! You'll come across these types of UX issues every now and then with React Native. It's great that we can use one codebase to build two fully native apps, but we still have to spend time to learn and explore environment-specific nuances in both platforms.

##### Switch

A [Switch](https://reactnative.dev/docs/switch) is essentially a toggle button. Some styling nuances aside, it looks quite similar across platforms.

🔍 [Switch example](https://snack.expo.io/@kadikraman/switch-example)

#### Other components

We have now played around with the most important components built into the core React Native library, but there are loads of community components you can install separately and use!

If you want to find some more, head over the [React Native Directory](https://reactnative.directory/) website.

### Opening a full screen modal

Before we get stuck into our form challenge, we'll need to do some prep work. Specifically, we need to open a modal to put that form in. This requires some tinkering with navigation again, so we'll do that first. This is an animation of what we'd like to get to:

![open-modal-demo](https://user-images.githubusercontent.com/20091777/138001047-6bd5b041-afa8-4027-b08c-cb3c9166abf6.gif)

![android-open-modal-demo](https://user-images.githubusercontent.com/20091777/138001096-561f426a-bbb0-4dff-a73e-5abfda9c3176.gif)

For the forms challenge, we'd like to be start adding our own color schemes to the list. But the best way to do that would be using a modal, so first we need to update out navigation so allow us to trigger display modals. In order to do this, we'll have to, once again, refactor our navigation.

Looking at our navigation as a tree, this is the layout we need to get to:

![image](https://user-images.githubusercontent.com/20091777/138001140-ce28027a-b34d-4cd4-a25c-69c3cf87fb51.png)

We'll be doing this following the react navigation [docs](https://reactnavigation.org/docs/modal/).

Our current layout only has the RootStack, HomeScreen, and DetailsScreen, so we need to add the a MainStack and a Modal Screen in the middle.

First lets rename our Stack to RootStack:

```
// App.js

const RootStack = createStackNavigator();
```

Now below that, we declare our MainStack:

```
// App.js

const MainStack = createStackNavigator();
```

Now let's add the MainStack and pull our existing navigation all out of the App component and into its own MainStackScreen component:

```
// App.js

const MainStackScreen = () => {
  return (
    <MainStack.Navigator>
      <MainStack.Screen name="Home" component={Home} />
      <MainStack.Screen
        name="ColorPalette"
        component={ColorPalette}
        options={({ route }) => ({ title: route.params.paletteName })}
      />
    </MainStack.Navigator>
  );
};
```

Finally, update the App component to use RootStack and MainStackScreen:

```
// App.js

const App = () => {
  return (
    <NavigationContainer>
      <RootStack.Navigator mode="modal">
        <RootStack.Screen
          name="Main"
          component={MainStackScreen}
          options={{ headerShown: false }}
        />
      </RootStack.Navigator>
    </NavigationContainer>
  );
};
```

Note that we had to use ```mode="modal"``` on ```RootStack.Navigator``` to tell the navigation that we're going to have a modal in there. We also had to add ```options={{ headerShown: false }}``` to ```RootStack.Screen```. If we didn't do this, we'd end up with two top navs in our main stack!

🔗 [Expo dc18d3d81fc5ff6a336971e8a369b5c51e11c8ec](https://github.com/kadikraman/AwesomeProjectExpo/commit/dc18d3d81fc5ff6a336971e8a369b5c51e11c8ec)

🔗 [RN 9fb150fcd1e5e2d9199f8826920d9f298de24f86](https://github.com/kadikraman/AwesomeProjectRN/commit/9fb150fcd1e5e2d9199f8826920d9f298de24f86)

Now all we need to do is add the modal. Create a new file called ```ColorPaletteModal.js``` in your ```screens``` directory and add some default content:

```
// screens/AddNewPaletteModal.js

import React from 'react';
import { View, Text } from 'react-native';

const AddNewPaletteModal = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};

export default AddNewPaletteModal;
```

And finally import the Modal in your App.js and add the modal to the RootStack:

```
import AddNewPaletteModal from './screens/AddNewPaletteModal';

// place this just before </RootStack.Navigator>
<RootStack.Screen name="AddNewPalette" component={AddNewPaletteModal} />;
```

🔗 [RN 18501165c8a8f854c749da6a6d87ae0b376174a0](https://github.com/kadikraman/AwesomeProjectRN/commit/18501165c8a8f854c749da6a6d87ae0b376174a0)

🔗 [Expo 7b6e1c682eb50ab2379cb87833252897dfc65c92](https://github.com/kadikraman/AwesomeProjectExpo/commit/7b6e1c682eb50ab2379cb87833252897dfc65c92)

👩‍💻 [Live Coding a5fa145d345e29ea5005508f09bc9d143441f3c0](https://github.com/FrontendMasters/AwesomeProjectExpo/commit/a5fa145d345e29ea5005508f09bc9d143441f3c0)

### Form exercise 📝

For the final exercise, let's add a form that lets the user submit their own color scheme, and add it to the top of the list.

Note: this exercise is meant to be challenging and provide you with scope to add your own features. If you decide to have a go at this on your own, don't expect to finish this in 15 minutes, or even an hour.

Here's an example of the finished product:

![forms-exercise](https://user-images.githubusercontent.com/20091777/155254872-27e138bd-ddff-4b47-aa6d-8e89db3dc1ae.gif)


### Form exercise solution 👀

##### *[Conclusion →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/7-conclusion/README.md#conclusion)*
