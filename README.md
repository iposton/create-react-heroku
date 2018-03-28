# Create React App, Heroku - <a href="https://create-react-test.herokuapp.com/">Demo</a> 
 
### Description
This is the create react app live on heroku using node.js and express server. 

### You can learn this
* Deploy a create react app to Heroku. 

### Software used for this application
* React (version 16.2.0) 
* [Create React App](https://github.com/facebook/create-react-app)    
* Heroku [Set up a free account ](https://www.heroku.com/)
* NPM (version 5.6.0)
* Node (version 6.10.3)
* express (version 4.16.3)

### Clone and serve this app.
* First `npm install` then run `npm start`. (may need to have npm version 5.2+ installed on your machine)

### Deploy create react app to Heroku. 
* Go to [Create React App](https://github.com/facebook/create-react-app) and follow the instructions in the readme.
* `cd app-name` into app <code>npm run-script build</code> to build the app in a build directory.
* Create an `app.js` file `touch app.js`.
* For Heroku this app points to the <code>app.js</code> server which uses node.js and express. (node.js is required to serve locally)

```js

//app.js

const express = require('express');
const http = require('http');
const path = require('path');

var app = express();

app.use(express.static(path.join(__dirname, 'build')));

const port = process.env.PORT || '8080';
app.set('port', port);

const server = http.createServer(app);
server.listen(port, () => console.log(`Running on localhost:${port}`));

```
* Run <code>node app.js</code> to serve the app at `http://localhost:8080`.
* Run <code>touch Procfile</code> in this app's root specifies the server for heroku to use.

```text

//Procfile

web: node app.js

```

* Run `npm install express --save`.
* A few adjustments to `package.json` are necessary for the heroku deploy process. `postinstall` and `engines` are important parts of `package.json` for a successful deploy. 

```json

//package.json

{
  "name": "app-name",
  "version": "0.1.0",
  "private": true,
  "main": "app.js",
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject",
    "postinstall": "react-scripts build"
  },
  "engines": {
    "node": "~6.10.3",
    "npm": "~5.6.0"
  },
  "dependencies": {
    "express": "^4.16.3",
    "react": "^16.2.0",
    "react-dom": "^16.2.0",
    "react-scripts": "1.1.1",
  }
}

``` 

* Assuming the heroku account is created and heroku toolbelt is installed make an initial commit and push to a github repo, then login to heroku, create a heroku app and push to heroku. Steps as follow.
* `git commit -am "initial commit"` then `git push`. (pushing app to new github repo)
* Login to heroku `heroku login` enter heroku password.
* Create heroku app `heroku create app-name`. (this will add the heroku remote)
* Deploy to heroku `git push heroku master`.

There may be an error during deploy pertaining to `package.lock` and `yarn.lock`. Delete `yarn.lock` from the app, commit and push to github repo and then `git push heroku master` again and the error will go away.

Each time there is a change to the app commit and push to github then `git push heroku master` to keep the two master branches in sync.  