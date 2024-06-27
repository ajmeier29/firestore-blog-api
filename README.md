# firestore-blog-api

## Description

For now, this will just be a note tracking repo, with intentions to easily create a new Express.js backend for interfacing with Firebase Firestore.

## Installation

#### Dependencies

```
├── axios@1.7.2
├── cors@2.8.5
├── dotenv@16.4.5
├── express@4.19.2
├── firebase@10.12.2
└── nodemon@3.1.4
```

#### Init project
```
npm init
```
```
npm install express
```

#### Add this to the package.json

```json
"type": "module",
```

#### Create server.js in the src folder
```js
const express = require("express");
const app = express();

app.listen(3001, () => console.log("Server listening at port 3001"));

// Include route files
const authRoute = require('./src/routes/auth');
// Use routes
app.use('/auth', authRoute);
```

#### The auth route (this is just a proxy retnring an api key). It's located in the /src/routes folder
```js
// src/routes/auth.js
const express = require('express');
const router = express.Router();
require('dotenv').config()

// Define a route
router.get('/', (req, res) => {
    res.send({
        'X-CAPTCHA-Key': process.env.CAPTCA_SECRET
    });// this gets executed when user visit http://localhost:3000/user
});

// export the router module so that server.js file can use it
module.exports = router;
```

#### Create the firebase.js file at the src root with the server.js
```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAnalytics } from "firebase/analytics";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
    apiKey: process.env.API_KEY,
    authDomain: process.env.AUTH_DOMAIN,
    projectId: process.env.PROJECT_ID,
    storageBucket: process.env.STORAGE_BUCKET,
    messagingSenderId: process.env.MESSAGING_SENDER_ID,
    appId: process.env.APP_ID,
    measurementId: process.env.MEASUREMENT_ID
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app);
```

#### Create the .env file
```
CAPTCHA_SECRET=XXXXXXXXXXXXXXXX
API_KEY=XXXXXXXXXXXXXXXX
AUTH_DOMAIN=XXXXXXXXXXXXXXXX
PROJECT_ID=XXXXXXXXXXXXXXXX
STORAGE_BUCKET=XXXXXXXXXXXXXXXX
MESSAGING_SENDER_ID=XXXXXXXXXXXXXXXX
APP_ID=XXXXXXXXXXXXXXXX
MEASUREMENT_ID=XXXXXXXXXXXXXXXX
```

#### Run the server
```
nodemon server.js
```


