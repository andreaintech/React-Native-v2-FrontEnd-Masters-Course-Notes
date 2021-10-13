## Navigation

### Navigation Intro
Now it's time to add navigation to our app. Let's start with adding a new page where we could list multiple color schemes as a list, and then navigate to a new page to view their details.

In order to achieve this, we will need a way to navigate between screens.

You may be surprised to learn that React Native does not actually come with any navigation tools. Despite the fact that pretty much every React Native application has navigation, it's not bundled into the framework and you'll have to install it separately. This is because Facebook have their own in-house navigation solution which is really customized for their own use case, so there was no way to share it for general use.

There are two popular libraries to choose from: [React Navigation](https://reactnavigation.org/) and [React Native Navigation](https://wix.github.io/react-native-navigation/#/). Despite the somewhat misleading name, they are both definitely React Native navigation libraries.

They both have more of less the same feature set - you can navigate between screens and stacks, add a bottom nav, create modals etc, so the choice really comes down to personal preference. React Native Navigation is the most similar with Facebook's own solution, and has historically had better performance. However, React Navigation has come a long way since it's initial release and should now be on par when it comes to performance.

For this workshop, we will be using React Navigation, because this is what is also bundle with Expo, and we want to keep the course content such that it could be followed with and without Expo.

### [Expo] Adding navigation with Expo

If you're using Expo, you're in luck. This setup is not nearly as tricky as pure React Native, since Expo have done all the heavy lifting for you. All you need to do is first install the navigation library:

```
npm install @react-navigation/native
```

and then all the expo-compatible dependencies:

```
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

Finally, open ```App.js``` and add the following:

```
import { NavigationContainer } from '@react-navigation/native';

const App = () => {
  return (
    <NavigationContainer>{/* Rest of the app code */}</NavigationContainer>
  );
};

export default App;
```

Specifically, you are importing the ```NavigationContainer``` from the navigation library we just installed, and wrapping the whole application in it. That's it! We're ready to start navigating.

There won't be any UI changes after this change. We're just setting things up for the next step.

🔗 [Expo fe48ac7768b92ea954b3333c09f7f7b62fa2b8ba](https://github.com/kadikraman/AwesomeProjectExpo/commit/fe48ac7768b92ea954b3333c09f7f7b62fa2b8ba)

### [RN] Adding navigation with plain React Native

We will be following the [getting started guide](https://reactnavigation.org/docs/getting-started) on the React Navigation website. Feel free to use it as a reference.

React Navigation is what we call a "library with native dependencies". That is, it doesn't *just* contain JavaScript code and dependencies: it also has some native to iOS and Android. This is necessary for navigation, because we want to take utilise the tools already natively available for navigation to make the user experience as seamless as possible.

First, let's install the necessary dependencies. Run this in your terminal in tour project directory:

```
npm install @react-navigation/native react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

#### iOS

If you are building iOS, you'll need to also install the native dependencies. The package manager we will be using for iOS is called CocoaPods, or "Pods" for short. You can think of it as npm for iOS. If you look inside the ```/ios``` directory of your application, you'll find a ```Podfile``` and a ```Podfile.lock``` (sounds a lot like ```package.json``` and ```package.lock```!). Prior to React Native 0.60, users had to "manually link" their native libraries. This was tedious and error prone. Now however, the dependencies are "autolinked", but you still have to install them yourself.

Check if you have CocoaPods installed by running:

```
pod --version
```

If not, you can install it on the terminal with:

```
sudo gem install cocoapods
```

This might take a little while. Once you have CocoaPods installed, navigate to the ios directory and install the pods!

```
cd ios
pod install
cd ..
```

#### Android

If you are building for Android you won't need to install the native dependencies yourself. This is done automagically by Gradle. Gradle is not a package manager par se, but let's just say it's a build toolkit for Android. When you run your Android project for the first time, it will download all the missing or changed dependencies.

You will however need to add some dependencies yourself: open ```android/app/build.gradle``` and add the following under ```dependencies```:

```
implementation 'androidx.appcompat:appcompat:1.1.0-rc01'
implementation 'androidx.swiperefreshlayout:swiperefreshlayout:1.1.0-alpha02'
```

These are just some native android tools necessary for compatibility with the latest version of the navigation library.

#### Finally (both iOS and Android)

Finally, open ```App.js``` and add the following:

```
import 'react-native-gesture-handler';
// other imports
import { NavigationContainer } from '@react-navigation/native';

const App = () => {
  return (
    <NavigationContainer>{/* Rest of the app code */}</NavigationContainer>
  );
};

export default App;
```

Note that the gesture handle import has to be the very first line in your file, even before the React import, and the ```<NavigationContainer>``` wraps around the whole app.

Now you'll have to also rebuild the native application. Whenever you add a library that has native dependencies, you'll have to reinstall in order for the new library to be included in the build.

Open you terminal and run ```npx react-native run-ios``` or ```npx react-native run-android``` depending on what you're building for.

🔗 [RN 3824add6be518a449c38e5935f1a39c26326352f](https://github.com/kadikraman/AwesomeProjectRN/commit/3824add6be518a449c38e5935f1a39c26326352f)

### Adding Navigation

There are two main types of navigation on mobile: bottom navigation, and stack navigation. You've certainly seen bottom navigation before, most apps have it: these are navigation items at the bottom of the screen and allow you to navigate between different sections of the app. Open the Twitter app for instance. (If you don't use Twitter, open Facebook, Instagram, Headspace, Spotify - most any app really, they all work the same regardless of whether they're build with React Native or not) Notice we have 4 bottom navigation items: home, search, notifications and messages. Notice also that navigating between them is pretty instant. When the app is launched, all the root pages of the bottom navigation get rendered at once. This is something to be mindful of if you're doing a lot of network requests on your root pages.

Now make sure you're on the home page of the twitter app and press on a tweet. Notice that the home icon is still selected, we've not navigated away from Home, but we've pushed another page onto the stack. This is the tweet detail screen. Most root pages on the bottom navigator are stacks. Notice also that this screen has a back button so we can navigate back to our root page. Leave the tweet detail page selected and move from home to search and back - notice that the tweet detail page is still selected even though we navigated away? That's something to be mindful of.

We don't need a bottom navigator yet, let's start with a single stack and two screens: ```Home``` and ```ColorPalette```. First things first, let's install the npm module for the stack navigator:

```
npm install @react-navigation/stack
```

Create a new folder in your project called ```screens``` and add two files: ```Home.js``` and ```ColorPalette.js```.

Open the ```Home.js``` and add some text to render:

```
// screens/Home.js

import React from 'react';
import { View, Text } from 'react-native';

const Home = () => {
  return (
    <View>
      <Text>Solarized</Text>
    </View>
  );
};

export default Home;
```

We don't need to use ```SafeAreaView``` anymore, since the navigation library handles the spacing above the screen for us.

Next, open ```ColorPalette.js``` and copy the code from ```App.js``` that renders the list of colors:

```
// screens/ColorPalette.js

import React from 'react';
import { Text, StyleSheet, FlatList } from 'react-native';
import ColorBox from '../components/ColorBox';

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

const ColorPalette = () => {
  return (
    <FlatList
      style={styles.container}
      data={COLORS}
      keyExtractor={item => item.hexCode}
      renderItem={({ item }) => (
        <ColorBox hexCode={item.hexCode} colorName={item.colorName} />
      )}
      ListHeaderComponent={<Text style={styles.heading}>Solarized</Text>}
    />
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
  heading: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
});

export default ColorPalette;
```

Open the ```App.js``` and remove all the code we've copied away to ```ColorPalette.js```.

Next, we'll want to import the Home and ColorPalette screens:

```
import Home from './screens/Home';
import ColorPalette from './screens/ColorPalette';
```

We'll also need to create a stack navigator:

```
import { createStackNavigator } from '@react-navigation/stack';

const Stack = createStackNavigator();
```

Finally, we want to add the stack navigator inside the ```<NavigationContainer>``` with our two new routes:

```
// App.js

<NavigationContainer>
  <Stack.Navigator>
    <Stack.Screen name="Home" component={Home} />
    <Stack.Screen name="ColorPalette" component={ColorPalette} />
  </Stack.Navigator>
</NavigationContainer>
```

The main thing to note here is that we give each screen a *unique* name. This name is important, as this is what we will be using to navigate between the screens.

Now we need to make it so when you press on the word ```Solarized```, it will open our ColorPalette component. For this we have a selection of touchable components to choose from:

- [TouchableOpacity](https://reactnative.dev/docs/touchableopacity) - the wrapped component has opacity applied when touch is in progress.
- [TouchableHighlight](https://reactnative.dev/docs/touchablehighlight) - the wrapped component darkens when touch is in progress.
- [TouchableWithoutFeedback](https://reactnative.dev/docs/touchablewithoutfeedback) - no visual feedback.
- [TouchableNativeFeedback](https://reactnative.dev/docs/touchablenativefeedback) - (Android only) adds Android-style touch feedback.

We will be using ```TouchableOpacity```. Go ahead and wrap the text in the ```Home.js``` component in a ```<TouchableOpacity>```. On the web, buttons have an ```onClick``` property. On mobile, we have an ```onPress``` which takes a function that will be executed when the user presses on anything inside the touchable area.

Finally, we'll need a way to tell the navigation where we'd like to go. Every component inside ```Stack.Screen``` will automatically get access to a special [```navigation``` prop](). This is the main tool you'll be using for anything navigation-related in your app. It can do a bunch of things, like programmatically go back a screen, reset the navigation stack and much more. We will be using it to navigate to the ColorPalette screen. This is done by calling the navigate function on the prop and passing in the desired route name:

### Navigation Exercise 📝

### Navigation Exercise Solution 👀


##### *[Hooks and Network Requests →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/5-hooks-and-network-requests/README.md#hooks-and-network-requests)*
