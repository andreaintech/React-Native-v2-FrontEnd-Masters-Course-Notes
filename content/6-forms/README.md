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

[Requirements]()

- Pressing on "add color scheme" opens a modal
- The user can enter the name for the color scheme
- The user can use toggle buttons to select colors to add to the scheme
- If the user hits submit without entering a name for the color, they will get an error message
- If the user hits submit without entering the number of colors, they will get an error message
- If the user has entered a name for the color scheme and picked at least 3 colors, the modal will close and the color scheme they created gets added to the top of the list

[Hints]()

- Don't use all the colors all at once. Start with 3 to get the toggle buttons to work. Then figure out how to add more
- You can use the native Alert modal to notify the user of any errors in the form
- navigation.navigate() works like navigation.goBack() if the page you target is already in the stack. You can use it to pass parameters back to the parent screen

[Data]()

These are all the named HTML5 colors:

```
const COLORS = [
  { colorName: 'AliceBlue', hexCode: '#F0F8FF' },
  { colorName: 'AntiqueWhite', hexCode: '#FAEBD7' },
  { colorName: 'Aqua', hexCode: '#00FFFF' },
  { colorName: 'Aquamarine', hexCode: '#7FFFD4' },
  { colorName: 'Azure', hexCode: '#F0FFFF' },
  { colorName: 'Beige', hexCode: '#F5F5DC' },
  { colorName: 'Bisque', hexCode: '#FFE4C4' },
  { colorName: 'Black', hexCode: '#000000' },
  { colorName: 'BlanchedAlmond', hexCode: '#FFEBCD' },
  { colorName: 'Blue', hexCode: '#0000FF' },
  { colorName: 'BlueViolet', hexCode: '#8A2BE2' },
  { colorName: 'Brown', hexCode: '#A52A2A' },
  { colorName: 'BurlyWood', hexCode: '#DEB887' },
  { colorName: 'CadetBlue', hexCode: '#5F9EA0' },
  { colorName: 'Chartreuse', hexCode: '#7FFF00' },
  { colorName: 'Chocolate', hexCode: '#D2691E' },
  { colorName: 'Coral', hexCode: '#FF7F50' },
  { colorName: 'CornflowerBlue', hexCode: '#6495ED' },
  { colorName: 'Cornsilk', hexCode: '#FFF8DC' },
  { colorName: 'Crimson', hexCode: '#DC143C' },
  { colorName: 'Cyan', hexCode: '#00FFFF' },
  { colorName: 'DarkBlue', hexCode: '#00008B' },
  { colorName: 'DarkCyan', hexCode: '#008B8B' },
  { colorName: 'DarkGoldenRod', hexCode: '#B8860B' },
  { colorName: 'DarkGray', hexCode: '#A9A9A9' },
  { colorName: 'DarkGrey', hexCode: '#A9A9A9' },
  { colorName: 'DarkGreen', hexCode: '#006400' },
  { colorName: 'DarkKhaki', hexCode: '#BDB76B' },
  { colorName: 'DarkMagenta', hexCode: '#8B008B' },
  { colorName: 'DarkOliveGreen', hexCode: '#556B2F' },
  { colorName: 'Darkorange', hexCode: '#FF8C00' },
  { colorName: 'DarkOrchid', hexCode: '#9932CC' },
  { colorName: 'DarkRed', hexCode: '#8B0000' },
  { colorName: 'DarkSalmon', hexCode: '#E9967A' },
  { colorName: 'DarkSeaGreen', hexCode: '#8FBC8F' },
  { colorName: 'DarkSlateBlue', hexCode: '#483D8B' },
  { colorName: 'DarkSlateGray', hexCode: '#2F4F4F' },
  { colorName: 'DarkSlateGrey', hexCode: '#2F4F4F' },
  { colorName: 'DarkTurquoise', hexCode: '#00CED1' },
  { colorName: 'DarkViolet', hexCode: '#9400D3' },
  { colorName: 'DeepPink', hexCode: '#FF1493' },
  { colorName: 'DeepSkyBlue', hexCode: '#00BFFF' },
  { colorName: 'DimGray', hexCode: '#696969' },
  { colorName: 'DimGrey', hexCode: '#696969' },
  { colorName: 'DodgerBlue', hexCode: '#1E90FF' },
  { colorName: 'FireBrick', hexCode: '#B22222' },
  { colorName: 'FloralWhite', hexCode: '#FFFAF0' },
  { colorName: 'ForestGreen', hexCode: '#228B22' },
  { colorName: 'Fuchsia', hexCode: '#FF00FF' },
  { colorName: 'Gainsboro', hexCode: '#DCDCDC' },
  { colorName: 'GhostWhite', hexCode: '#F8F8FF' },
  { colorName: 'Gold', hexCode: '#FFD700' },
  { colorName: 'GoldenRod', hexCode: '#DAA520' },
  { colorName: 'Gray', hexCode: '#808080' },
  { colorName: 'Grey', hexCode: '#808080' },
  { colorName: 'Green', hexCode: '#008000' },
  { colorName: 'GreenYellow', hexCode: '#ADFF2F' },
  { colorName: 'HoneyDew', hexCode: '#F0FFF0' },
  { colorName: 'HotPink', hexCode: '#FF69B4' },
  { colorName: 'IndianRed', hexCode: '#CD5C5C' },
  { colorName: 'Indigo', hexCode: '#4B0082' },
  { colorName: 'Ivory', hexCode: '#FFFFF0' },
  { colorName: 'Khaki', hexCode: '#F0E68C' },
  { colorName: 'Lavender', hexCode: '#E6E6FA' },
  { colorName: 'LavenderBlush', hexCode: '#FFF0F5' },
  { colorName: 'LawnGreen', hexCode: '#7CFC00' },
  { colorName: 'LemonChiffon', hexCode: '#FFFACD' },
  { colorName: 'LightBlue', hexCode: '#ADD8E6' },
  { colorName: 'LightCoral', hexCode: '#F08080' },
  { colorName: 'LightCyan', hexCode: '#E0FFFF' },
  { colorName: 'LightGoldenRodYellow', hexCode: '#FAFAD2' },
  { colorName: 'LightGray', hexCode: '#D3D3D3' },
  { colorName: 'LightGrey', hexCode: '#D3D3D3' },
  { colorName: 'LightGreen', hexCode: '#90EE90' },
  { colorName: 'LightPink', hexCode: '#FFB6C1' },
  { colorName: 'LightSalmon', hexCode: '#FFA07A' },
  { colorName: 'LightSeaGreen', hexCode: '#20B2AA' },
  { colorName: 'LightSkyBlue', hexCode: '#87CEFA' },
  { colorName: 'LightSlateGray', hexCode: '#778899' },
  { colorName: 'LightSlateGrey', hexCode: '#778899' },
  { colorName: 'LightSteelBlue', hexCode: '#B0C4DE' },
  { colorName: 'LightYellow', hexCode: '#FFFFE0' },
  { colorName: 'Lime', hexCode: '#00FF00' },
  { colorName: 'LimeGreen', hexCode: '#32CD32' },
  { colorName: 'Linen', hexCode: '#FAF0E6' },
  { colorName: 'Magenta', hexCode: '#FF00FF' },
  { colorName: 'Maroon', hexCode: '#800000' },
  { colorName: 'MediumAquaMarine', hexCode: '#66CDAA' },
  { colorName: 'MediumBlue', hexCode: '#0000CD' },
  { colorName: 'MediumOrchid', hexCode: '#BA55D3' },
  { colorName: 'MediumPurple', hexCode: '#9370D8' },
  { colorName: 'MediumSeaGreen', hexCode: '#3CB371' },
  { colorName: 'MediumSlateBlue', hexCode: '#7B68EE' },
  { colorName: 'MediumSpringGreen', hexCode: '#00FA9A' },
  { colorName: 'MediumTurquoise', hexCode: '#48D1CC' },
  { colorName: 'MediumVioletRed', hexCode: '#C71585' },
  { colorName: 'MidnightBlue', hexCode: '#191970' },
  { colorName: 'MintCream', hexCode: '#F5FFFA' },
  { colorName: 'MistyRose', hexCode: '#FFE4E1' },
  { colorName: 'Moccasin', hexCode: '#FFE4B5' },
  { colorName: 'NavajoWhite', hexCode: '#FFDEAD' },
  { colorName: 'Navy', hexCode: '#000080' },
  { colorName: 'OldLace', hexCode: '#FDF5E6' },
  { colorName: 'Olive', hexCode: '#808000' },
  { colorName: 'OliveDrab', hexCode: '#6B8E23' },
  { colorName: 'Orange', hexCode: '#FFA500' },
  { colorName: 'OrangeRed', hexCode: '#FF4500' },
  { colorName: 'Orchid', hexCode: '#DA70D6' },
  { colorName: 'PaleGoldenRod', hexCode: '#EEE8AA' },
  { colorName: 'PaleGreen', hexCode: '#98FB98' },
  { colorName: 'PaleTurquoise', hexCode: '#AFEEEE' },
  { colorName: 'PaleVioletRed', hexCode: '#D87093' },
  { colorName: 'PapayaWhip', hexCode: '#FFEFD5' },
  { colorName: 'PeachPuff', hexCode: '#FFDAB9' },
  { colorName: 'Peru', hexCode: '#CD853F' },
  { colorName: 'Pink', hexCode: '#FFC0CB' },
  { colorName: 'Plum', hexCode: '#DDA0DD' },
  { colorName: 'PowderBlue', hexCode: '#B0E0E6' },
  { colorName: 'Purple', hexCode: '#800080' },
  { colorName: 'Red', hexCode: '#FF0000' },
  { colorName: 'RosyBrown', hexCode: '#BC8F8F' },
  { colorName: 'RoyalBlue', hexCode: '#4169E1' },
  { colorName: 'SaddleBrown', hexCode: '#8B4513' },
  { colorName: 'Salmon', hexCode: '#FA8072' },
  { colorName: 'SandyBrown', hexCode: '#F4A460' },
  { colorName: 'SeaGreen', hexCode: '#2E8B57' },
  { colorName: 'SeaShell', hexCode: '#FFF5EE' },
  { colorName: 'Sienna', hexCode: '#A0522D' },
  { colorName: 'Silver', hexCode: '#C0C0C0' },
  { colorName: 'SkyBlue', hexCode: '#87CEEB' },
  { colorName: 'SlateBlue', hexCode: '#6A5ACD' },
  { colorName: 'SlateGray', hexCode: '#708090' },
  { colorName: 'SlateGrey', hexCode: '#708090' },
  { colorName: 'Snow', hexCode: '#FFFAFA' },
  { colorName: 'SpringGreen', hexCode: '#00FF7F' },
  { colorName: 'SteelBlue', hexCode: '#4682B4' },
  { colorName: 'Tan', hexCode: '#D2B48C' },
  { colorName: 'Teal', hexCode: '#008080' },
  { colorName: 'Thistle', hexCode: '#D8BFD8' },
  { colorName: 'Tomato', hexCode: '#FF6347' },
  { colorName: 'Turquoise', hexCode: '#40E0D0' },
  { colorName: 'Violet', hexCode: '#EE82EE' },
  { colorName: 'Wheat', hexCode: '#F5DEB3' },
  { colorName: 'White', hexCode: '#FFFFFF' },
  { colorName: 'WhiteSmoke', hexCode: '#F5F5F5' },
  { colorName: 'Yellow', hexCode: '#FFFF00' },
  { colorName: 'YellowGreen', hexCode: '#9ACD' },
];
```

### Form exercise solution 👀

##### *[Conclusion →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/7-conclusion/README.md#conclusion)*
