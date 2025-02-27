<h2 style="color:darkgreen;">React Native Swipe Button Component</h2>
<hr>
<div style="color:darkcyan; font-size: 15px;">
  <code>
    <p>npm install rn-swipe-button --save</p>
    <p>import SwipeButton from 'rn-swipe-button';</p>
    &lt;SwipeButton /&gt; 
  </code>
</div>
<hr>
<div>
  <h2 style="color:darkgreen;">Screenshots of Android and iOS</h2>
  <img src="https://udaysravank.github.io/RNSwipeButton/rn-swipe-button-ios.png" width="200" style="margin-right: 30px;"/>
  <img src="https://udaysravank.github.io/RNSwipeButton/rn-swipe-button.png" style="margin-right: 30px;" width="230"/>
  <img src="https://udaysravank.github.io/RNSwipeButton/rn-swipe-button.gif" width="230" />
  <p>These screenshots are from demo app under examples folder in the repo</p>
</div>
<hr>
<h2 style="color:darkgreen;">Component properties</h2>
<pre style="font-size: 15px; color: brown;">
    <b>disabled</b>: PropTypes.bool,
    <b>disabledRailBackgroundColor</b>: PropTypes.string,
    <b>disabledThumbIconBackgroundColor</b>: PropTypes.string,
    <b>disabledThumbIconBorderColor</b>: PropTypes.string,
    <b>enableRightToLeftSwipe</b>: PropTypes.bool,
    <b>height</b>: PropTypes.number,
    <b>onSwipeFail</b>: PropTypes.func,
    <b>onSwipeStart</b>: PropTypes.func,
    <b>onSwipeSuccess</b>: PropTypes.func,
    <b>railBackgroundColor</b>: PropTypes.string,
    <b>railBorderColor</b>: PropTypes.string,
    <b>railFillBackgroundColor</b>: PropTypes.string,
    <b>railFillBorderColor</b>: PropTypes.string,
    <b>swipeSuccessThreshold</b>: PropTypes.number, <span style="color: blueviolet">// Ex: 70. Swipping 70% will be considered as successful swipe</span>
    <b>thumbIconBackgroundColor</b>: PropTypes.string,
    <b>thumbIconBorderColor</b>: PropTypes.string,
    <b>thumbIconComponent</b>: PropTypes.node,
    <b>thumbIconImageSource</b>: PropTypes.oneOfType([
      PropTypes.string,
      PropTypes.number,
    ]),
    <b>title</b>: PropTypes.string,
    <b>titleColor</b>: PropTypes.string,
    <b>titleFontSize</b>: PropTypes.number,
    <b>width</b>: PropTypes.number,
</pre>
<hr>
<h2 style="color:darkgreen;">Code for above screenshots</h2>

```
import React from 'react';
import {View, Text} from 'react-native';
import Icon from 'react-native-vector-icons/FontAwesome';

import thumbIcon from './assets/thumbIcon.png';
import styles from './styles';

import SwipeButton from 'rn-swipe-button';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: 'swipe status appears here',
    };
  }
  showToastMessage = message => this.setState({message});
  renderSubHeading = heading => (
    <Text style={styles.subHeading}>{heading}</Text>
  );
  renderSwipeStatus = () => (
    <Text style={styles.swipeStatus}>{this.state.message}</Text>
  );
  render() {
    const TwitterIcon = () => <Icon name="twitter" color="#3b5998" size={30} />;
    const facebookIcon = () => (
      <Icon name="facebook" color="#3b5998" size={30} />
    );

    setInterval(
      () => this.setState({message: 'swipe status appears here'}),
      5000,
    );

    return (
      <View style={styles.container}>
        <Text style={styles.title}>React Native Swipe Button</Text>
        {this.renderSwipeStatus()}
        {this.renderSubHeading('Disabled')}
        <SwipeButton disabled={true} />
        {this.renderSubHeading('Swipe status callbacks')}
        <SwipeButton
          disabled={false}
          onSwipeStart={() => this.showToastMessage('Swipe started!')}
          onSwipeFail={() => this.showToastMessage('Incomplete swipe!')}
          onSwipeSuccess={() =>
            this.showToastMessage('Submitted successfully!')
          }
        />
        {this.renderSubHeading('Right to left swipe enabled')}
        <SwipeButton
          enableRightToLeftSwipe
          thumbIconBackgroundColor="#FFFFFF"
          thumbIconComponent={facebookIcon}
          title="Slide to unlock"
          onSwipeSuccess={() => this.showToastMessage('Slide success!')}
        />
        {this.renderSubHeading('Set a component as thumb icon')}
        <SwipeButton
          thumbIconBackgroundColor="#FFFFFF"
          thumbIconComponent={TwitterIcon}
          title="Slide to unlock"
        />
        {this.renderSubHeading('Set .png image as thumb icon')}
        <SwipeButton thumbIconImageSource={thumbIcon} />
        {this.renderSubHeading('Set height')}
        <SwipeButton height={25} />
        {this.renderSubHeading('Set height and width')}
        <SwipeButton height={35} width={150} title="Swipe" />
      </View>
    );
  }
}
```
