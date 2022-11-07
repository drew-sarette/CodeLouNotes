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

    app.use("/api/", router);

    const server = app.listen(5000, function() {
        console.log("Node Server is listening on port 5000");
    });
``.
