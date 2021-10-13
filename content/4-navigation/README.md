## Navigation

Now it's time to add navigation to our app. Let's start with adding a new page where we could list multiple color schemes as a list, and then navigate to a new page to view their details.

In order to achieve this, we will need a way to navigate between screens.

You may be surprised to learn that React Native does not actually come with any navigation tools. Despite the fact that pretty much every React Native application has navigation, it's not bundled into the framework and you'll have to install it separately. This is because Facebook have their own in-house navigation solution which is really customized for their own use case, so there was no way to share it for general use.

There are two popular libraries to choose from: [React Navigation](https://reactnavigation.org/) and [React Native Navigation](https://wix.github.io/react-native-navigation/#/). Despite the somewhat misleading name, they are both definitely React Native navigation libraries.

They both have more of less the same feature set - you can navigate between screens and stacks, add a bottom nav, create modals etc, so the choice really comes down to personal preference. React Native Navigation is the most similar with Facebook's own solution, and has historically had better performance. However, React Navigation has come a long way since it's initial release and should now be on par when it comes to performance.

For this workshop, we will be using React Navigation, because this is what is also bundle with Expo, and we want to keep the course content such that it could be followed with and without Expo.

### Navigation Intro

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

### [Expo] Adding navigation with Expo

### [RN] Adding navigation with plain React Native

### Adding Navigation

### Navigation Exercise 📝

### Navigation Exercise Solution 👀


##### *[Hooks and Network Requests →](https://github.com/adasilvapdev/React-Native-v2-FrontEnd-Masters-Course-Notes/blob/main/content/5-hooks-and-network-requests/README.md#hooks-and-network-requests)*
