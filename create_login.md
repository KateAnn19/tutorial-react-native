Create Login View
=================================
In this part, we are going to make a nickname input section and entrance button.  


### 1. Run React Native
First, run the project that we created previous step.  
  
```unix  
   $ npm start  
   $ react-native run-ios  
```  
  
On the other way, you can open this project by xcode and execute.  
Following screen will be displayed.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/run-ios-01.png" width=510 height=420 />    
  
  
### 2. Make Navigator
In this part, We are going to add screen transition in our app with [Navigator](http://facebook.github.io/react-native/docs/navigator.html#content).   
First, Make a `src` directory under the `root` directory and make a `main.js` file inside of the `src` directory.  
Second, Make a `components` directory under the `src` directory and make a `login.js` file inside of the `components` directory.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/make-file-01.png" width=202 height=329 />  
  
Modify `index.ios.js` file as follows.  
  
```javascript  

  var React = require('react-native');
  var {
    AppRegistry
  } = React;
  
  var Main = require('./src/main')
  
  AppRegistry.registerComponent('SendBirdSample', () => Main);
  
```  
  
  
Modify `src/main.js` file as follows.  
  
```javascript  

  var React = require('react-native')
  var {
    Navigator,
    StyleSheet
  } = React;
  
  var Login = require('./components/login');
  
  var ROUTES = {
    login: Login
  };
  
  module.exports = React.createClass({
    renderScene: function(route, navigator) {
      var Component = ROUTES[route.name];
      return <Component route={route} navigator={navigator} />;
    },
    render: function() {
      return (
        <Navigator
          style={ styles.container }
          initialRoute={ {name: 'login'} }
          renderScene={this.renderScene}
          configureScene={ () => { return Navigator.SceneConfigs.FloatFromRight; } }
        />
      );
    }
  });
  
  var styles = StyleSheet.create({
    container: {
      flex: 1
    }
  });

  
```  
  
  
Modify `src/components/login.js` file as follows.  
  
```javascript  

  var React = require('react-native');
  var {
    View,
    Text,
    StyleSheet
  } = React;
  
  module.exports = React.createClass({
    render: function() {
      return (
        <View style={styles.container}>
          <Text style={{color: 'white'}}>SendBird JavaScript SDK!!!</Text>
        </View>
      );
    }
  });
  
  var styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: 'center',
      alignItems: 'stretch',
      backgroundColor: '#6E5BAA'
    }
  });

  
```  
  

Refresh the simulator.  
Following screen will be displayed.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/login-image-01.png" width=372 height=684 />  
  

### 3. Make Login View
We make one input box and one login button.  
We need [TextInput](http://facebook.github.io/react-native/docs/textinput.html#content), [TouchableHighlight](http://facebook.github.io/react-native/docs/touchablehighlight.html#content) and `getInitialState` for this view.  
`getInitialState` is init code before call `render` function.  
And for SendBird login, need `sendbird` that we install package previous step.  

Add `TextInput`, `TouchableHighlight` and `getInitialState` function.  
  
```javascript  
  
  var React = require('react-native');
  var {
    View,
    Text,
    TextInput,
    TouchableHighlight,
    StyleSheet
  } = React;
  
  module.exports = React.createClass({
    getInitialState: function() {
      return {
        username: ''
      };
    },
    render: function() {
      return (
        <View style={styles.container}>
          <View style={styles.loginContainer}>
            <TextInput
              style={styles.input}
              value={this.state.username}
              onChangeText={(text) => this.setState({username: text})}
              placeholder={'Enter User Nickname'}
              maxLength={12}
              multiline={false}
              />
  
            <TouchableHighlight
              style={styles.button}
              underlayColor={'#328FE6'}
              onPress={this.onPress}
              >
              <Text style={styles.label}>LOGIN</Text>
            </TouchableHighlight>
          </View>
        </View>
      );
    },
    onPress: function() {
      console.log(this.state.username);
    }
  });
  
  var styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: 'center',
      alignItems: 'stretch',
      backgroundColor: '#6E5BAA'
    },
    loginContainer: {
      flex: 1,
      justifyContent: 'center',
      alignItems: 'center',
    },
    input: {
      width: 250,
      color: '#555555',
      padding: 10,
      height: 50,
      borderColor: '#32C5E6',
      borderWidth: 1,
      borderRadius: 4,
      alignSelf: 'center',
      backgroundColor: '#ffffff'
    },
    button: {
      justifyContent: 'center',
      alignItems: 'center',
      borderWidth: 1,
      borderRadius: 5,
      borderColor: '#328FE6',
      padding: 10,
      marginTop: 10,
      backgroundColor: '#32c5e6'
    },
    label: {
      width: 230,
      flex: 1,
      alignSelf: 'center',
      textAlign: 'center',
      fontSize: 20,
      fontWeight: '600',
      color: '#ffffff'
    }
  });

```  
  
Refresh the simulator.  
Following screen will be displayed.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/login-image-02.png" width=372 height=684 />  
  

### 3. Debug with Chrome development tools
개발을 하며 `console.log()`를 통해 확인을 하는 방법을 알아보겠습니다.  
`command+D`를 누르면 아래 화면과 같이 `Debug in Chrome`이라는 버튼이 보입니다.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/login-image-03.png" width=373 height=685 />    
  
이 버튼을 클릭하면 `Chrome`창이 나타나고 개발자 도구를 이용하여 `console`에 찍히는 값을 확인할 수 있습니다.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/login-image-04.png" width=766 height=221 />  
    
위의 코드에서 `LOGIN`버튼을 클릭했을때 호출되는 함수로 `onPress`를 등록해 놓았습니다.  
`TextInput`에 `nickname`을 입력하고 `LOGIN`버튼을 클릭했을때 입력한 값이 `Chrome Development Tools`에 나타나면 정상적으로 동작하는 것입니다  
다음과 같이 나타나면 정상적으로 동작하고 있는 것입니다.  
  
<img src="https://s3-ap-northeast-1.amazonaws.com/sendbird-react-native-tutorial-image/login-image-05.png" width=893 height=481 />  
  

### 4. Login SendBird


