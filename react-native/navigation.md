# Navigation

{% code-tabs %}
{% code-tabs-item title="./App.js" %}
```javascript
import React from 'react';
import { StyleSheet, Text, View,Button } from 'react-native';

import {createAppContainer} from 'react-navigation';
import {createStackNavigator} from 'react-navigation-stack';
import {HomeScreen} from './src/screens/HomeScreen';
import {ProfileScreen} from './src/screens/ProfileScreen'

const MainNavigator = createStackNavigator(
  {
    Home: HomeScreen,
    Profile: ProfileScreen
  },
  {
    initialRouteName: 'Home'
  }
)
const AppContainer = createAppContainer(MainNavigator);

export default class App extends React.Component{
  render(){
    return <AppContainer/>;
  }
};
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="./src/screens/HomeScreen.js" %}
```javascript
import React from 'react';
import { StyleSheet, Text, View,Button } from 'react-native';

export class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    const {navigate} = this.props.navigati
on;
    return (
      <Button
        title="Go to the Profile"
        onPress={() => navigate('Profile')}
      />
    );
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="./src/screens/ProfileScreen.js" %}
```javascript
import React from 'react';
import { 
StyleSheet, Text, View,Button } from 'react-native';

export class ProfileScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    return (
      <Button
        title="Back to the Home"
      />
    );
  }
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}



{% embed url="https://facebook.github.io/react-native/docs/navigation" %}

