1. make dir let say HelloReact
2. cd HelloReact
3. npm init # will create package.json
4. install global packages, we need babel plugins
* npm install -g babel
* npm install -g bable-cli
5. add dependencies and plugins, we need webpack bundler, --save command will
   add packages on the package.json file
* npm install webpack --save
* npm install webpack-dev-server --save
6. To use React, install it first with --save command
* npm install react --save
* npm install react-dom --save
7. let's install other babel plugins as well
* npm install babel-core
* npm install babel-loader
* npm install babel-preset-react
* npm install babel-preset-es2015
8.create some required files
* touch index.html
* touch App.jsx
* touch main.js
* touch webpack.config.js
9. set compiler, server and loaders
open webpack.config.js file and add the following code
set main.js as webpack entry point
output path is the place where bundled app will be served
we are also setting development server to 8080 port and you can choose any port
you want
At last, set babel loaders to search for js files, also use es2015 and react
presets that we already installed

webpack.config.js
var config = {
  entry: './main.js',
  output: {
    path: '/',
    filename: 'index.js',
  },
  devServer: {
    inline: true,
    port: 8080
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      }
    ]
  }
}
module.exports = config;

10. open package.json and delete "test":"echo......" which is inside "scripts"
    object, we are deleting as we do not need any testing
    Add "start" command instead
     * "start": "webpack-dev-server --hot"
    To execute above script, it requires webpack-dev-server
    To install webpack-dev-server, use the following commands
    * npm install webpack-dev-server -g
    * npm start # starts the server
    --hot command will add live reload after something is changed inside our
files so we don't need to refresh the browser every time we change our code

11. index.html
<body>
  <div id="app"></div>
  <script src="index.js"></script>
</body>

12. App.jsx
import React from 'react'
class App extends React.Component {
  render () {
    return (
      <div>Hello world!!</div> 
    );
  }
-}
export default App;

13. main.js # where App.jsx component will import and render it to our App
    element
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.jsx';
ReactDOM.render(<App />, document.getElementById('app'));

Note: To make component reusable, you need to export component after creation
and import it in the file where you want to use it

14. run the server and access on browser with localhost:8080
* npm start

15. sometime you will get couple of errors, those errors are:
WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value.
Solution: just add below code on webpack.config.js
* mode: 'development'

The CLI moved into a separate package: webpack-cli.
Please install 'webpack-cli' in addition to webpack itself to use the CLI.
-> When using npm: npm install webpack-cli -D
* npm install webpack-cli -D
* yarn add webpack-cli -D

✖ ｢wds｣: Invalid configuration object. Webpack has been initialised using a configuration object that does not match the API schema.
 - configuration.module has an unknown property 'loaders'.
 >> To get rid from this error, just you need to change loaders to rules on webpack.config.js
 i.e: module: {
      rules: [

Router Tutorial:
Follow all the steps mentioned above as per requirements:
I suggest you to start by in stalling react-router-dom
* sudo npm install react-router-dom

Configure the .babelrc file in the root of the project
touch .babelrc
{
  "presets": ["es2015", "react"]
}

index.html
------------
<body>
  <div id = "app"></div>
  <script type = "text/javascript" src = "bundle.js"></script>
</body>

webpack.config.js
-------------------
module.exports = {
   entry: './app/main.js',
   output: {
      filename: 'bundle.js'
   },
   module: {
      loaders: [
         {
            loader: 'babel-loader',
            test: /\.js$/,
            exclude: /node_modules/
         }
      ]
   },
   devServer: {
      port: 7777
   }
};

add router:
Main.js
--------
import React from 'react';
import { render } from 'react-dom';
import App from './App';

render(<App />, document.getElementById('app'));

App.js
-------
import React, { Component } from 'react';
import { BrowserRouter as Router, Switch, Route, Link } from 'react-router-dom';
import Home from './Home';
import Login from './Login';

class App extends Component {
   render() {
      return (
         <Router>
            <div>
               <h2>Welcome to React Router Tutorial</h2>
               <ul>
                  <li><Link to={'/'}>Home</Link></li>
                  <li><Link to={'/Login'}>Login</Link></li>
               </ul>
               <hr />
               
               <Switch>
                  <Route exact path='/' component={Home} />
                  <Route exact path='/Login' component={Login} />
               </Switch>
            </div>
         </Router>
      );
   }
}
export default App;

step 3: create components
Home.js
--------
import React, { Component } from 'react';

class Home extends Component {
   render() {
      return (
         <div>
            <h2>Home</h2>
         </div>
      );
   }
}
export default Home;

Login.js
---------
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class Login extends Component {
   render() {
      return (
         <div>
            <h2>Login</h2>
         </div>
      );
   }
}
export default Login;

