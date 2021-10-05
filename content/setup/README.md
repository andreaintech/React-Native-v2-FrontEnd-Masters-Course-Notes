## Setup 

### [Expo] Getting started with Expo

The fastest way to get started with React Native is to us Expo and run the app on your device. Feel free to use the React Native docs or Expo docs for reference.

#### You'll need:
- A computer (Mac, Windows or Linux).
- A smartphone (iPhone or Android).

#### Install Node

First, make sure you have Node.js installed (12 or later). You can do this by opening a terminal and running ```node -v```. If not you can install it [here](https://nodejs.org/en/). There's usually two versions to choose from, pick the one that says LTS (Long Term Support) after the version number.

#### Install Expo
```
npm install -g expo-cli
```

This installs the expo cli globally. We'll be using this to create our new project.

#### Create the project

```
expo init AwesomeProject
```

You'll be prompted to choose a template. Pick 'blank' - we're starting from scratch!

#### Run the project

```
cd AwesomeProject
npm start
```

Note that you can also use ```expo start``` or ```yarn start``` if you have yarn installed.

#### Preview the app on your phone

First, make sure that your phone is connected to the same WiFi network as your computer. This is really important!

Next you'll need to install the Expo client on your phone. This is the native shell Expo provides that lets you get started without having the build the native app yourself. Go to the App Store or Play store, search for "Expo" and install it. You will also have to create an Expo account if you don't already have one (don't worry - it's free!).

Finally, open the browser window that was opened when you ran the packages. See the QA code? If you're on Android, you can scan the code with your Expo app. On iOS, open the camera app to can the code. You will be prompted to "open in Expo".

At this point you should see something like this:

![image](https://user-images.githubusercontent.com/20091777/135953772-1b3c5303-b7a8-4b02-9e52-00a0bba3adc6.png)

And that's it! You're ready to start coding!

🔗 [Expo dd3bca50a532c90902252a3e9dcd0ef608000ee8](https://github.com/kadikraman/AwesomeProjectExpo/commit/dd3bca50a532c90902252a3e9dcd0ef608000ee8)




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
