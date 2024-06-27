# firestore-blog-api

## Description

For now, this will just be a note tracking repo, with intentions to easily create a new Express.js backend for interfacing with Firebase Firestore.

## Installation

Dependencies

```
├── axios@1.7.2
├── cors@2.8.5
├── dotenv@16.4.5
├── express@4.19.2
├── firebase@10.12.2
└── nodemon@3.1.4
```

Init project
```
npm init
```
```
npm install express
```
Create server.js in the src folder
```js
const express = require("express");
const app = express();

app.listen(3001, () => console.log("Server listening at port 3001"));

// Include route files
const authRoute = require('./src/routes/auth');
// Use routes
app.use('/auth', authRoute);
```
The auth route (this is just a proxy retnring an api key). It's located in the /src/routes folder

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
Creaate the firebase.js file at the src root with the server.js
```js

```

