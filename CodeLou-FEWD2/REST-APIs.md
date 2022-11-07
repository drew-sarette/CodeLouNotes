# Setting up Express server
1. mkdir server && cd server
2. npm init -y
3. npm install express nodemon
    "nodemon" is short for "node monitor" and it will reload your browser/endpoint when changes are made on the server.
4. add index.js file (default starting file) in the server folder.
5. ```
    const express = require("express");
    const app = express();
    const router = express.Router();

    router.get("/", function (req, res, next) {
        res.send("apple");
    });

    //All endpoints will be prefixed with "/api/"
    app.use("/api/", router);

    //Tell the express app to listen on port 5000
    const server = app.listen(5000, function() {
        console.log("Node Server is listening on port 5000");
    });```
6. In packages.json, add '''"start": "nodemon index.js"```
This causes npm start to run nodemon on index.js, allowing you to see changes live.
7. npm start
8. can now test server!

# Responding to get request 
Any literal javascript object (primitives, arrays, objects) can be sent in response.

## using appropriate status code
200 is the default http status code if the request was successful, but you can change the code using 
```
router.get("/", function(req, res, next) {
    res.status(nnn).send(stuff);
});
```
Best practice is to always use the status() method with an appropriate code.
## Wrapping data in a JSON object
instead of sending back a JS object, it is best to send JSON:
```
res.status(200).json({
    "status": 200,
    "statusText": "OK",
    "message": "Put whatever you need to here",
    "data": data
});
```
The status, statusText, and message make the response user-friendly, and the data property contains the actual response.

