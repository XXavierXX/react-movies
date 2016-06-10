# react-movies

This Android application produces a list of popular movies containing the word "react."

This program utilizes the React Native framework using a hybrid of syntaxes between HTML5 and JavaScript.

react-movies reflects the React Native tutorial on building applications for iOS and Android.

The code shown below can be found in the file index.android.js

```
/**
 * Brandon Santana
 * Sample React Native App
 * https://github.com/facebook/react-native
 */
 
import React, { Component } from 'react';
import {
  AppRegistry,
  Image,
  ListView,
  StyleSheet,
  Text,
  View,
} from 'react-native';


var MOCKED_MOVIES_DATA = [
	  {title: 'Title', year: '2016', 
	   posters: {thumbnail: 'http://i.imgur.com/UePbdph.jpg'}},
];

var REQUEST_URL = 'https://raw.githubusercontent.com/facebook/react-native/master/docs/MoviesExample.json';


class AwesomeProject extends Component {
  
  constructor(props) {
    super(props);
    this.state = {
	dataSource: new ListView.DataSource({
	  rowHasChanged: (row1, row2) => row1 !== row2,
    }),
     loaded: false,
    };
  }  

  componentDidMount() {
    this.fetchData();
  }

  fetchData() {
    fetch(REQUEST_URL)
      .then((response) => response.json())
      .then((responseData) => {
	this.setState({
	  dataSource: this.state.dataSource.cloneWithRows(responseData.movies),
	  loaded: true,
	});
      })
      .done();
  }

  render() {

    if (!this.state.loaded) {
      return this.renderLoadingView();
    }

     return (
       <ListView
	        dataSource={this.state.dataSource}
	         renderRow={this.renderMovie}
	         style={styles.listView}
       />
     );
   } 
  	
  renderLoadingView() {
    return (
	<View style={styles.container}>
	  <Text>
	    Loading movies...
	  </Text>
	</View>
    );
  }

  renderMovie(movie) {
    return (
      <View style={styles.container}>
      	<Image
      	  source={{uri: movie.posters.thumbnail}}
      	  style={styles.thumbnail}
      	/>
         <View style={styles.rightContainer}>
           <Text style={styles.title}>{movie.title}</Text>
           <Text style={styles.year}>{movie.year}</Text>
         </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  thumbnail:{
    width: 53,
    height: 81,
  },
  
  rightContainer: {
    flex: 1,
    
  },
  title: {
    fontSize: 20,
    marginBottom: 8,
    textAlign: 'center',
  },
  year: {
    textAlign: 'center',
  },
  ListView: {
    paddingTop: 20,
    backgroundColor: '#F5FCFF',
  },
});

AppRegistry.registerComponent('AwesomeProject', () => AwesomeProject);
```
