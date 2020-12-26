# fireact

A chat application with React(frontend) and Firebase(BaaS)

## dependencies

- firebase
- react-firebase-hooks

`npm install firebase react-firebase-hooks`

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Deployment

Click here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

## Security rules for FireStore

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }

    match /messages/{docId} {
    allow read: if request.auth.uid != null;
    allow create: if canCreateMessage();
    }

    function canCreateMessage(){
    let isSignedIn = request.aut.uid != null;
    let isOwner = request.auth.uid == request.resource.data.uid;

    let isNotBanned = exists(
    /databases/$(database)/documents/banned/$(request.auth.uid))
     == false;

     return isSignedIn && IsOwner && isNotBanned;

    }
  }
}
```

## Adding serverless backend server

`firebase login`
`firebase init functions`
`npm i bad-words`


//cloud function
//serverless server
const functions = require("firebase-functions");
const Filter = require(bad-words");

const admin require("firebase-admin")
admin.initializeApp();

const db = admin.firestore();

exports.detectEvilUsers = function.firestore
.document("message/{msgId}")
.onCreate(async (doc,ctx) =>)
