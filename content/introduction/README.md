## Introduction
### Welcome

Hi there, and welcome to [React Native v2!](![image](https://user-images.githubusercontent.com/20091777/135774518-6a99ab5b-c3b5-4b94-9fbb-0a5317cefec6.png)
) 👋

### Course Objective

Kadi builds React Native apps for a living and her main goal today is to give you an idea on how I do it - what are the best practices, conventions, do's and dont's.

The aim of the course is to give you the knowledge and resources necessary to start building your own React Native project. We will cover what React Native is, how it works, what kind of components and tooling are available, and how to use them. We will stick with built-in and mainstream components, and minimize the use of third party components and libraries.

### Course guide

The course is designed to be pretty hands-on: the general pattern is that we'll introduce a concept and then apply it.

- Chapters marked with a 📝 emoji are exercises. How you approach them is up to you! If you generally learn best by doing, I'd recommend spending up to 10-15 minutes in completing the exercise independently before looking at the solution.
- Chapters marked with a 👀 emoji are the solutions to exercises.
- Make note of the link 🔗 emojis - these link to a GitHub repository that contains the solution to the code we just added - you can use this as a reference to check your work.
- There are three versions of the solution: [RN] for a plain React Native project, [Expo] for an expo project and [Live Coding] which is a exactly how the exercise was written live on the Workshop day. The resulting app looks the same, but there were some minor changes in variable names and order of operations which might be confusing, so if you're following the course on Frontend Master, you might want to use the version of the solutions with the 👩‍💻 emoji. Thank you [Joumana](https://github.com/joumanae) for the writeup!
- You will also occasionally see links with a 🔍 emoji - these are code examples in Expo Snack, there to help introduce or illustrate a concept. You can look at these in the browser (unless specified otherwise) or on your phone if you have the Expo app installed. Feel free to play around with them, your changes will not be saved to the hosted version.
- You can follow this course with Expo or without, the choice is yours. For most lessons, this doesn't matter. There are a couple of pages that are specific to the platform though. These will be prefixed with [Expo] or [RN] - choose the one that applies to you, but feel free to also check out the other if you're interested.

### About You

The intended audience for this course are people who are familiar with JavaScript, but new to React Native. If you already know React, that's perfect, since your React skills are completely transferrable to React Native with only minor modifications to account for the native platform. However if you are new to both React and Native, never fear! I will be explaining all the React concepts as well as the React Native concepts as we discover them together, however there will be more of a focus on the parts of React Native that differ from React on the web.

In this course, I will be using a MacBook Pro, an iPhone simulator and an Android emulator from Android Studio.

You do not need to match my setup, but you should have:

- either a Mac, Windows or Linux machine.
- either a physical device (iPhone or Android) OR a simulator/emulator installed.

There are a few different ways to set up your development environment, depending on what hardware you have and whether you'd like to use vanilla React Native or Expo. Don't worry about making a decision right away, the next lesson will explain the pros and cons of all your options so you can make an informed decision on what is the best fit for you.

### About Kadi

(writing by her) Hi, my name is Kadi and I am a Senior Software Engineer at [Formidable](https://formidable.com/) where I build things in JavaScript, mostly using React Native. I first got into coding in University where I studied Maths with Psychology. I had just the one programming course in second year of university, in C++. From the first time my program compiled and ran without errors, I was hooked! After that, I followed a long and winding road to end up where I am now, but suffice it to say I have been writing code professionally since 2013, using React since 2015 and React Native since 2017.

As for social media, you can find me on [Twitter](https://twitter.com/kadikraman), [LinkedIn](https://www.linkedin.com/in/kadi-kraman-922a7277/) and [GitHub](https://github.com/kadikraman).

### Why Was This Course Created

This is supplementary material for my [Frontend Masters course - React Native v2](https://frontendmasters.com/courses/react-native-v2/) using the [Gatsby template by Brian Holt](https://github.com/btholt/gatsby-course-starter). Not everyone has the money to pay for these courses which is why these materials are and will be forever open source for you to reference and share. Thank you to the kind folks at [Frontend Masters](https://frontendmasters.com/) who are encouraging teachers to compile and open source these course materials.

![image](https://user-images.githubusercontent.com/20091777/135774493-571e9e1b-a4ca-4570-9dcb-778d3a795c78.png)

### About React Native

![image](https://user-images.githubusercontent.com/20091777/135775309-eb6a12b2-fea2-40f0-ad97-48e36d5e78a4.png)

Smartphones are really just small computers you can carry around in your pocket. Small, but powerful. An often cited comparison is that the average smartphone these days has a 1 million times more RAM and 7 million times more memory than the guidance computer for Apollo 11 that [landed the first humans on the moon!](https://www.realclearscience.com/articles/2019/07/02/your_mobile_phone_vs_apollo_11s_guidance_computer_111026.html)

Due to their smaller screen and touch-based interface, browsing the web on a smartphone is still often a sub-optimal experience. Progressive Web Apps (PWAs) improve the experience somewhat, but nothing beats a good old native Mobile App designed from the ground up with mobile experience in mind.

In 2020, the number of smartphone users in the world is 3.5 billion, which translates to 45.12% of the world's population owning a smartphone. Looking at the global market share for mobile phones we can see Android and iOS clearly in the lead.

![image](https://user-images.githubusercontent.com/20091777/135775360-821ac882-ecbd-4b77-a381-7096f553216b.png)

Note that this is the global stats and vary significantly per country. For instance, the market share for iOS was 57.3% in the US, 51.6% in the UK, but only 2.1% in India. As a result, which platform you focus most of your energy on should depend on your target audience. It is clear however that if you manage to cover both iOS and Android, you will cover 99% of your audience, no matter the country.

Now, as phones are just tiny computers, they have an operating system, the same way your computer does.

- Some examples of computers: MacBook, Dell, Lenovo
- Some examples of operating systems: macOS, Windows, Linux
- Some examples of phones: iPhone, Samsung Galaxy S20, Nexus 5X
- Some examples of phone operating systems: iOS, Android

Applications are designed to run on a particular operating system so you can't just take an iOS app and run it on Android and vice versa. App Store vs Google Play Store aside, the underlying architecture is incompatible.

So in order to target 99% of smartphone users, we'll have to build two apps: one for Android and one for iOS.

![image](https://user-images.githubusercontent.com/20091777/135775475-dad0fb7e-817b-4a34-bd20-ae34c432566a.png)

It's easy to imagine the difficulties this can cause: you'll have to manage two of everything: language, codebases, developer teams, feature sets, release schedules etc. Hiring two developer teams is expensive, and hiring a single team that has in depth knowledge of both Android and iOS is almost impossible.

React Native is a platform developed by Facebook for solving this problem. Their goal was to build a platform that enables you to have:

- Fully native apps (not webviews/PWAs).
- One codebase.
- One development team.
- One language.
- Fully extensible (you should be anything that is possible without using React Native).

![image](https://user-images.githubusercontent.com/20091777/135775518-917012ce-01bb-47c9-a6c2-7813ee9ff4a1.png)

The language of choice ended up being JavaScript probably because React (the popular frontend framework also developed by Facebook) is a JavaScript framework, so it provides the smallest possible learning curve for folks already familiar with React.

Note: React Native is not the only such framework, and it's not even the first, but where it differs from others is that a built React Native app is indistinguishable from a "real" native app. Unlike most of the other frameworks, it is not just a webview that look like a real app. The other really standout feature is that React Native apps are infinitely extensible: you are not constrained by the framework and you can always pure native code in your app if you want to do something the framework doesn't already enabled. Finally, if you're already familiar to React and web development, then the learning curve for React Native is really not that steep.

### How does it work?

Without getting overly technical here, React Native is built in such a way that it targets existing compilers. For example, we have compilers that accept Java / Kotlin code and target Android platform, or Objective C / Swift targeting iOS platform. This is really powerful, because

1. Native compilers are designed for this, so we'll be no worse than non-React Native apps, and
2. This makes the React Native framework extensible to other native platforms. React Native Windows? VR? Web? It could all be available from our one unified JavaScript API.

![image](https://user-images.githubusercontent.com/20091777/135775704-e09e27bf-fa9a-491a-a969-073affb9f072.png)

Source: https://hackernoon.com/understanding-react-native-bridge-concept-e9526066ddb8

### Should you use Expo or plain React Native?

If you've been eyeing up the React Native space already, you've probably heard of [Expo](https://expo.dev/). Expo is essentially a suite of tools build for and around React Native, designed to improve and enhance the developer experience. They are a separate company, not affiliated with Facebook.

Some people have strong options on whether or not they want to use Expo for React Native, and if you're one of those people, feel free to skip this and carry on with your preference. This is an introductory workshop and can be followed with Expo and without. However if you don't have any strong opinions on this and need help deciding, read on!

If you are completely new to mobile development and just want to get a taste of React Native without a lot of upfront configuration work, I'd recommend starting with Expo, just because you'll get to the part where you try out coding much quicker.

You should also definitely go for Expo if you have a Windows or Linux machine, but you want to run the app on your physical iPhone. This is simply not possible with plain React Native, because native iOS apps can only be built on a macOS machine. Expo overcomes this be allowing you to install a native "shell" app on your phone and transfer the JavaScript bundle you're working on directly into this native shell. This way, you end up only writing JavaScript on locally, no native compilation step necessary.

It can take quite a bit time to set up your development environment without Expo, since you'll have to download, install and configure XCode and/or Android Studio. Just to give you an idea of the setup time, here are some really rough estimates based on my experience:

#### macOS
- Expo on physical device: ~10 minutes (Android or iOS).
- Expo on iOS simulator: ~1 hour.
- Expo on Android emulator: ~1.5 hours.
- Plain React Native on physical device: ~2 hours (Android or iOS).
- Plain React Native on iOS simulator: ~2 hours.
- Plain React Native on Android emulator: ~2 hours.

#### Windows or Linux
- Expo on physical device: ~20 minutes (Android or iOS).
- Expo on iOS simulator: ❌
- Expo on Android emulator: ~2 hours.
- Plain React Native on physical device: ~2.5 hours (Android only).
- Plain React Native on iOS simulator: ❌
- Plain React Native on Android emulator: ~3 hours.

Expo restrictions only really come to play when you're doing advanced things with React Native. In particular, if you need to make any native changes to your code. Basically if you need to install any libraries or add anything that changes any of the non-JavaScript code or configurations. You'll have to eject from the Expo safe space and start managing all your native code yourself as you would with plain React Native.

In my experience, all the production apps I've working on have had to be ejected, even if they started with Expo. However it has been an invaluable tool for learning and quick prototyping. I always use Expo for in-person workshops primarily because it'd be a mighty boring workshop if we all spent 2+ hours just setting up our development environment, but also because I have been using a MacBook for the past 5 years and am not confident I can always help debug issues specific to Windows and Linux. For client projects, I have always used plain React Native, usually due to the client's preference.
