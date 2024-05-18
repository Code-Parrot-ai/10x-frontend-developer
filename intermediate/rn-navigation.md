---
title: "Navigation in React Native"
subtitle: "Essential Guide to Implementing Stack, Tab, and Drawer Navigation in React Native"
slug: "navigation-in-react-native"
tags: react-native, react-navigation, mobile-app-development, navigation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716007462018/Y4-XcFAPJ.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Navigation is the backbone of great mobile app experiences, allowing users to seamlessly flow between screens. In React Native development, achieving top-notch navigation is very important for creating engaging apps.

## Understanding the Basics of Navigation

### Why is Navigation Important?

Navigation in mobile apps is not just about moving between screens; it's about creating an accessible pathway for users to explore your app's features. It's crucial for engaging users and providing a smooth user experience. Poor navigation can lead to user frustration and app abandonment.

### Types of Navigation:

- **Stack Navigation:** Allows users to navigate between screens where each new screen is placed on top of a stack. Pressing back leads to the previous screen.

- **Tab Navigation:** Uses a tab bar at the bottom or top of the app, enabling quick switching between different sections.

- **Drawer Navigation:** Provides a slide-out menu that allows for navigation between app sections from a side panel.

### Navigation Libraries:

React Native does not include built-in navigation components. Instead, developers rely on third-party libraries. The most popular is React Navigation, renowned for its extensibility and community support. Other options include Native Navigation, which leverages native components for navigation purposes.

Using React Navigation makes developing excellent navigation for React Native applications a breeze. This powerful library offers multiple navigation patterns, extensive customization, and an active community.

## Setting Up a React Native App

We will be using Expo to create a new React Native project. Run the following commands to get started:

```bash
npx create-expo-app navigation-app
cd navigation-app
npm start
```

You should see the Expo DevTools open in your browser, and you can run the project on an emulator or a physical device. I will be using my physical device to run the project.

## Adding Dependencies

To use React Navigation in your project, you need to install the required dependencies. Run the following command:

```bash
npm install @react-navigation/native
```

and some additional dependencies:

```bash
npx expo install react-native-screens react-native-safe-area-context
```

also install various navigators:

```bash
npm install @react-navigation/stack @react-navigation/bottom-tabs @react-navigation/drawer
```

## Implementing Navigation

### 1. Define the Navigator:

To set up the basic configuration for React Navigation, you need to wrap your app in a `NavigationContainer`. Here's an example:

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createStackNavigator } from "@react-navigation/stack";

const Stack = createStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

Here, we've created a simple stack navigator with two screens: Home and Details. You can customize the navigation options for each screen, such as setting the title or header style.

### 2. Navigating Between Screens:


#### Stack Navigator

In your components, you can use the `navigation` prop to navigate between screens. Here's an example:

Consider this to be the Home Screen of the app:

```tsx
// ..

interface HomeScreenProps {
  navigation: any;
}

const HomeScreen: React.FC<HomeScreenProps> = ({ navigation }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>This is the home page</Text>
      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate("Details")}
      >
        <Text style={styles.buttonText}>Go to Details</Text>
      </TouchableOpacity>
    </View>
  );
};

// ...

export default HomeScreen;
```

And this to be some page called the details page:

```tsx
// ..

interface DetailsScreenProps {
  navigation: any;
}

const DetailsScreen: React.FC<DetailsScreenProps> = ({ navigation }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>This is the details page</Text>
      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate("Home")}
      >
        <Text style={styles.buttonText}>Go to Home</Text>
      </TouchableOpacity>
    </View>
  );
};

// ..

export default DetailsScreen;
```

In your App.tsx, you can pass the `screenOptions` prop to the `Stack.Navigator` to customize the header style:

```tsx
<Stack.Navigator
    screenOptions={{
        headerStyle: {
            backgroundColor: "#333333",
        },
        headerTintColor: "#FFF",
        headerTitleStyle: {
            fontWeight: "bold",
        },
    }}
>
    // ...
</Stack.Navigator>
```

Since we have connected these screens using a stack navigator the output should look something like this:

![Stack Navigation](https://cdn.hashnode.com/res/hashnode/image/upload/v1715595759303/zZuZwjORR.gif?auto=format)

#### Tab Navigator

Change your `App.tsx` to use Tab Navigator instead of Stack Navigator:

```tsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import HomeScreen from './components/HomeScreen';
import DetailsScreen from './components/DetailsScreen';
import { Text } from 'react-native';
import { Ionicons } from '@expo/vector-icons';


const Tab = createBottomTabNavigator();

function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator
          // ..
          tabBarIcon: ({ focused, color, size }) => {
            let iconName;
            if (route.name === 'Home') {
              iconName = focused ? 'home' : 'home-outline';
            } else if (route.name === 'Details') {
              iconName = focused ? 'list' : 'list-circle';
            }
            return <Ionicons name={iconName} size={size} color={color} />;
          },
          tabBarActiveTintColor: '#1E88E5', 
          tabBarInactiveTintColor: 'gray',
          tabBarStyle: {
            backgroundColor: '#424242', 
            paddingBottom: 5,
          },
          tabBarLabelStyle: {
            fontSize: 12,
          },
        })}
      >
        <Tab.Screen name="Home" component={HomeScreen} options={{ tabBarBadge: 3 }} />
        <Tab.Screen name="Details" component={DetailsScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

Here we pass an additional prop called `tabBarIcon` to customize the icons for each tab. We can also provide a `tabBarBadge` to show a badge on top of the tab icon. 

You should see something like this:

![Tab Navigation](https://cdn.hashnode.com/res/hashnode/image/upload/v1715595844804/STKhc3nZb.gif?auto=format)

#### Drawer Navigator

Change your `App.tsx` to use Drawer Navigator instead of Stack Navigator:

```tsx
// ...
import { createDrawerNavigator } from '@react-navigation/drawer';

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator initialRouteName="Home" 
          screenOptions={{
            headerStyle: {
                backgroundColor: "#333333",
            },
            headerTintColor: "#FFF",
            headerTitleStyle: {
                fontWeight: "bold",
            },
            drawerInactiveTintColor: "#FFF",
            drawerActiveTintColor: "#e91e63",
            drawerActiveBackgroundColor: '#333',
            drawerContentContainerStyle: {
                backgroundColor: '#333',
                height: '100%',
            },
        }}>
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Details" component={DetailsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

Here, we've created a drawer navigator with two screens: Home and Details. You can customize the drawer's appearance using the `screenOptions` prop.

You should see something like this:

![Drawer Navigation](https://cdn.hashnode.com/res/hashnode/image/upload/v1715595954712/VlGtYhqvt.gif?auto=format)

## Passing Data Between Screens

In React Native applications, managing and transferring data between screens is a fundamental requirement for many use cases. Whether you’re passing user selections, form entries, or complex objects, understanding how to navigate between screens with data is crucial. React Navigation provides straightforward solutions to handle these needs.

### Why Passing Data is Important?

Passing data between screens is essential for maintaining the continuity and context of the user's experience. For example, a user selects a product from a list in one screen, and you need to display the detailed information of that product in another screen. Efficient data transfer between screens ensures a seamless and responsive user experience.

### Using Parameters in React Navigation

React Navigation allows you to pass parameters along with the route when navigating between screens. Here’s how you can implement this:

Let's define a parameter to pass in the `HomeScreen` component:

```tsx
  const productDetails = {
    id: '01',
    name: 'Example Product',
    description: 'This is an example product.'
  };
```

In the `HomeScreen` component, you can pass the parameter to the `DetailsScreen` component:

```tsx
<TouchableOpacity style={styles.button} onPress={() => navigation.navigate('Details', {product: productDetails})}>
    <Text style={styles.buttonText}>Go to Details</Text>
</TouchableOpacity>
```

You pass the parameters by providing an object as the second argument to the `navigate` function. In this case, we are passing the `productDetails` object to the `DetailsScreen`.

In the `DetailsScreen` component, you can access the parameter using the `route` prop:

```tsx
interface DetailsScreenProps {
  navigation: any;
  route: any;
}

const DetailsScreen: React.FC<DetailsScreenProps> = ({ navigation, route }) => {
  const { product } = route.params;
  console.log(product); // Logging the product to the console

  return (
    <View style={styles.container}>
      <Text style={styles.text}>This is the details page</Text>
      <TouchableOpacity style={styles.button} onPress={() => navigation.navigate('Home')}>
        <Text style={styles.buttonText}>Go to Home</Text>
      </TouchableOpacity>
      <View style={styles.productContainer}>
        <Text style={styles.productText}>Product ID: {product.id}</Text>
        <Text style={styles.productText}>Product Name: {product.name}</Text>
        <Text style={styles.productText}>Product Description: {product.description}</Text>
      </View>
    </View>
  );
};
```

Now after visiting the `DetailsScreen` from the `HomeScreen`, you should see the product details displayed on the screen:

![Passing Data Between Screens](https://cdn.hashnode.com/res/hashnode/image/upload/v1715597093716/Ayq_pwd98.gif?auto=format)

## Conclusion

This is just a starting point for implementing navigation in React Native applications. You can further customize the navigation options, add animations, and integrate other features to enhance the user experience. React Navigation provides a robust foundation for building complex navigation patterns in your mobile apps. You can check out the official documentation here: [React Navigation](https://reactnavigation.org/).