# React Native v2 FrontEnd Masters Course Notes

### React Native v2
Building mobile applications

## Table of Contents

### [Introduction](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/tree/main/content/introduction#introduction)
- [Welcome](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/tree/main/content/introduction#welcome)
- [About React Native](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/tree/main/content/introduction#about-react-native)
- [Should you use Expo or plain React Native?](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/introduction/README.md#should-you-use-expo-or-plain-react-native)

### Setup
- [Expo] Getting started with Expo
- [RN] Getting started with plain React Native
- Adding a linter
- Debugging

### Basic components
- Basic React Native components
- Styling
- Styling Exercise 📝
- Styling Exercise Solution 👀
- Components
- Lists
- Lists Exercise 📝
- Lists Exercise Solution 👀

### Navigation
- Navigation Intro
- [Expo] Adding navigation with Expo
- [RN] Adding navigation with plain React Native
- Adding Navigation
- Navigation Exercise 📝
- Navigation Exercise Solution 👀

### Hooks and Network Requests
- useState, useCallback, useEffect
- Network Requests Exercise 📝
- Network Requests Exercise Solution 👀
- Pull to refresh

### Forms
- Overview of Forms in React Native
- Opening a full screen modal
- Form exercise 📝
- Form exercise solution 👀

### Conclusion
- Wrapping up

### Extra Credit
- [Expo] Ejecting from Expo
- Platform Specific Code
- Security




## Setup 

### [Expo] Getting started with Expo

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

### [RN] Getting started with plain React Native

We will be following the [getting started guide](https://reactnavigation.org/docs/getting-started/) on the React Navigation website. Feel free to use it as a reference.

React Navigation is what we call a "library with native dependencies". That is, it doesn't just contain JavaScript code and dependencies: it also has some native to iOS and Android. This is necessary for navigation, because we want to take utilise the tools already natively available for navigation to make the user experience as seamless as possible.

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

### Adding a linter

This step is optional. If you want to just get stuck in the code, feel free to skip this.

Adding a linter to your React Native project is not mandatory, but highly encouraged. Not only does it help ensure a consistent code style throughout the project, it also highlights errors and often uncovers bad practices. I always set up linting and code formatting from the onset when starting a new project, even if it's just personal or a hobby project!

The go-to linter for JavaScript is called [eslint](https://eslint.org). There are three main reasons you should always install a linter:


1. Enforce consistent code style - double quotes or single? Trailing comma or no? Most experienced engineers have a preference one way or another, but ultimately most agree that it doesn't really matter, so long as it's consistent. With eslint we can set up these preferences once, and the whole project will be checked to ensure the same style is followed.

2. Catch mistakes - it's easy to miss typos, unused variables and forgetting to return a variable from a function while developing. When integrating eslint to your code editor, you'll get helpful warnings and errors for these issues while you're writing your code. Saves a lot of debugging time!

3. Avoid bad practices - JavaScript is a pretty amazing language in that it allows you to do pretty much anything. This is very powerful, but dangerous, because it leaves it up to us, the developers, to have some rules and order. Depending on the code style you do with (e.g. functional vs object oriented) there are many linting rules that help you enforce good practices that go with the code style you prefer.

#### Adding eslint - installation (step 1 of 4)

First, we should install the package. For this, open your terminal, navigate to the root directory of your project and run the following:

With npm:

```
npm install eslint @react-native-community/eslint-config --save-dev
```

With yarn:

```
yarn add eslint @react-native-community/eslint-config --dev
```

This will add two packages to your dev dependencies:

- eslint - the code linter for JavaScript
- @react-native-community/eslint-config - a community-built eslint configuration for React Native

You can always configure your own linting rules of course, but I like to start with community presets.

#### Adding eslint - adding the configuration files (step 2 of 4)

We've now installed both eslint and the community preset, but the eslint package doesn't know about the preset. In order to make eslint aware of this, we need to add a configuration file.

Create a new file in the root directory of your project and call it ```.eslintrc.js``` (yes, the filename starts with a ```.```). If you used ```react-native init``` to create your project, then you'll already have this file, but with Expo you'll have to create it.

Open the file and add the following:

```
// .eslintrc.js

module.exports = {
  root: true,
  extends: '@react-native-community',
};
```

This lets the linter know about the configuration package we want to use.

The community package actually comes with prettier pre-installed. Prettier is another package complimentary to eslint, but it focuses on code formatting. It mostly deals how the code looks rather than its correctness. The great thing about prettier is that if you can turn on "format on save" or have a pre-commit hook that runs its before a commit so your code will always be formatted uniformly.

Prettier has very few configuration options, because their mentality is to have as few variations as possible. I am definitely guilty of having a preference here. If you'd like your code to look exactly like mine in the example, add these prettier settings.

Create another file in the root directory of your project and call it ```.prettierrc.js``` (you'll already have this file as well if you used ```react-native init```)

Open the file and add the following:

```
// .prettierrc.js

module.exports = {
  bracketSpacing: true,
  singleQuote: true,
  trailingComma: 'all',
};
```

- ```bracketSpacing``` - adding a space around brackets, e.g. ```import { useState } from 'react';``` vs ```import {useState} from 'react';```
- ```singleQuote``` - using single quotes for strings, e.g. ```import React from 'react'``` vs ```import React from "react"```
- ```trailingComma``` - adding a trailing comma after array arguments (the default is not to have a trailing comma for the last element of the array).

#### Adding eslint - adding the run script (step 3 of 4)

Now we have eslint installed and configured. But how to actually run it? Open the ```package.json``` in your project and add the following under the ```scripts``` section:

```
"lint": "eslint ."
```

Now you can run ```npm run lint``` or ```yarn lint``` in your terminal and the linter will report both eslint and prettier issues.

#### Adding eslint - adding it to your code editor (step 4 of 4)

It's all well and good to lint your code on the command line, but ideally you'd have instant feedback while you're writing your code. Thankfully most code editors have an integration option for this.

#### VSCode
Code => Preferences => Extentions => ESLint

#### Atom

Atom => Preferences => Install => linter-eslint

You may have to close and reopen your code editor for the package to start working, but that's it! You now have the optimal working environment.


🔗 [Expo c4463a28410a10b295fe76c9a273a7c3ae5dc76c](https://github.com/kadikraman/AwesomeProjectExpo/commit/c4463a28410a10b295fe76c9a273a7c3ae5dc76c)

🔗 [RN 4822e123aa0e9d2892970a74065f2dc15ebec6e6](https://github.com/kadikraman/AwesomeProjectRN/commit/4822e123aa0e9d2892970a74065f2dc15ebec6e6)

### Debugging

As developers, we spend a whole lot of time debugging, especially when learning something new. Let's look at some debugging tips for React Native.

Debug menu

- on device - shake the device (yes, really!)
- iOS simulator - Cmd + D
- Android emulator - Cmd + M on Mac, Crl + M on Windows/Linux

![image](https://user-images.githubusercontent.com/20091777/135949426-caee1b62-80fc-434b-be1e-19ca56522cdc.png)

![image](https://user-images.githubusercontent.com/20091777/135949440-603556a2-f8c4-4041-972d-fb1508e9db66.png)

![image](https://user-images.githubusercontent.com/20091777/135949460-f3ad2ccd-3e42-428b-a656-5e80e6ba0d7f.png)

The debug menus for iOS, Android and Expo look a bit different per platform, but they all have the same options available.

The main options you'll use are:

- Refresh: this reloads the JavaScript bundle. You can also do this with Cmd + R (or Ctrl + R)
- Debug: this opens a debug window in your browser
- Show/hide inspector: this allows you to inspect individual elements on the page
- Enable/disable fast refresh: you might know this as "hot reloading", it will update your app with your changes when you save the file, no need to refresh manually

#### console.log() debugging

Sometimes it's just good to log stuff out to see what's going on. The good news is that ```console.log()``` works just the same on React Native as in plain JavaScript.

In order to log out to the console:

- Open the debug menu (as described above) and turn on debug - this will open a new browser window.
- Inspect the browser window (right click + inspect for most browsers).
- ```console.log()``` something in your app.
- The logged out text will appear in the browser console.

Note:

- ```console.warn``` will show a yellow box warning in React Native
- ```console.error``` will show a full screen error

Note: there is a known bug in [VSCode](https://github.com/microsoft/TypeScript/issues/30471) where typing in console incorrectly auto imports ```import console=require('console');```. You can get around this by turning off auto imports. Go to code => preferences => settings => auto imports to do this.

## Basic components

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
### Styling

### Styling Exercise Solution 👀

### Components

### Lists

### Lists Exercise 📝

## Navigation

### Navigation Intro

## Hooks and Network Requests

## Forms

## Conclusion

## Extra Credit
