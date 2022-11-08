# Setting up Express server
1. mkdir server && cd server
2. npm init -y
3. npm install express
    
4. npm install --save-dev nodemon
    "nodemon" is short for "node monitor" and it will reload your browser/endpoint when changes are made on the server. THe --save-dev option saves it as a development dependency.

5. add index.js file (default starting file) in the server folder.
6. ```
    // Bring in the express server and create application
    const express = require("express");
    const app = express();

    // Use the Express router object. 
    const router = express.Router();

    router.get("/", function (req, res, next) {
        res.send("apple");
    });

    //All endpoints will be prefixed with "/api/"
    app.use("/api/", router);

    //Tell the express app to listen on port 5000
    const server = app.listen(5000, function() {
        console.log("Node Server is listening on port 5000");
    });
    ```
7. In packages.json, add ```"devStart": "nodemon index.js"``` under "scripts". Then you can use ```npm run devStart``` to run nodemon on index.js, allowing you to see changes live.
8. npm run devStart
9. can now test server! Postman or Thunderclient -> enter http://localhost:PORT/api/ to trigger the router.get() function.

# Responding to get request 
Any literal javascript object (primitives, arrays, objects) can be sent in response.

## using appropriate status code
200 is the default http status code if the request was successful, but you can change the code using 
```
stuff = [
    {
        "id": 1,
        "name": "thing 1"
    },
    {
        "id": 2,
        "name": "thing 2"
    }
]
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
## Retrieve JSON from a separate file
Better option than leaving it cluttering up index.js. The principle is to separate the logic for the controller (index.js) and the data (gets its own data module)/
1. create repos/pieRepo.js, containing
    ```
    let pieRepo = {
        get: function() {
            return [
            { "id": 1, "name": "apple" },
            { "id": 1, "name": "apple" },
            { "id": 1, "name": "apple" },
        ];

        }
    };
    module.exports = pieRepo;
    ```
2. in index.js, add
    ```let pieRepo = require("./repos/pieRepo");```
    This lets you access your pie data with
    ```const pies = pieRepo.get();```
3. Add assets/pies.json, containing 
    ```[
            { "id": 1, "name": "apple" },
            { "id": 1, "name": "apple" },
            { "id": 1, "name": "apple" },
        ]```
        
4. in pieRepo.js, import the fs module (built in to node) with 
    ```const fs = require(fs);```
5. Change pieRepo.js to read
     ```
    const FILE_NAME = "./assets/pies.json";
    let pieRepo = {
        get: function(resolve, reject) {
        fs.readFile(FILE_NAME, function (err, data) {
            if (err) {
                reject(err);
            }
            else {
                resolve(JSON.parse(data));
            }
        });
        }
    };
    module.exports = pieRepo;
    ```
7.  change index.js so that pieRepo.get() is called in the router.get, and takes two anonymous functions, the first sends the JSON on a succussesful file read, and the second passes an error object to the next middleware:
    ```
     router.get("/", function (req, res, next) {
        pieRepo.get(function(data){
            res.status(200).json({
                "status": 200,
                "statusText": "OK",
                "message": "Put whatever you need to here",
                "data": data
            });
        }, function(err) {
            next(err);
        });
    });
    ```
## Get a single piece of data 
1. in pieRepo.js, add a function to search for a pie with a given id:
```
getById: function (id, resolve, reject) {
    fs.readFile(FILE_NAME, function (err, data) {
        if (err) {
            reject(err);
        }
        else {
            let pie = JSON.parse(data).find(pie => pie.id == id);
            resolve(pie);
        }
    });
}
```
2. in index.js, modify the router.get() to take the :id from the url and pass it to the pieReop.getById function:
```
router.get("/:id", function (req, res, next) {
    pieRepo.getById(req.params.id, function(data) {
        if (data) {
            res.status(200).json({
                "status": 200,
                "statusText": "OK",
                "message": "Single pie retrieved.",
                "data": data
            });
        }
        else {
            res.status(404).json({
                "status": 404,
                "statusText": "Not Found",
                "message": `The pie ${req.params.id} could not be found.`,
                "error": {
                    "code": "NOT_FOUND",
                    "message": `The pie ${req.params.id} could not be found.`
                }
            });
        }
    }, function(err) {
        next(err);
    });
});
```
Notice the json sent back if the pie is not found contains an error object.

## Modifying data with POST PUT PATCH DELETE
### Post method:
1. add insert method to pieRepo.js:
```
insert: function (newData, resolve, reject) {
    fs.readFile(FILE_NAME, function (err, data) {
        if (err) {
            reject(err);
        }
        else {
            let pies = JSON.parse(data);
            pies.push(newData);
            fs.writeFile(FILE_NAME, JSON.stringify(pies), function (err) {
                if (err) {
                    reject(err);
                }
                else {
                    resolve(newData);
                }
            });
        }
    });
}
```
This code takes a new pie object, reads the file containing all pies, adds the two together, and then writes it to the same file. A better way to do the same thing would be using a database.

2. add middleware in index.js to allow the app to support json:
```app.use(express.json());```

3. add post method:
```
router.post("/", function (req, res, next) {
    pieRepo.insert(req.body, function(data) {
        res.status(201).json({
            "status": 201,
            "statusText": "Created",
            "message": "New pie added.",
            "data": data
        });
    }, function (err) {
        next(err);
    });
})
```

### PUT method:
1. add an update function to pieRepos.js:
```
update: function (newData, id, resolve, reject) {
    fs.readfile(FILE_NAME, function (err, data){
        if (err) {
            reject(err);
        }
        else {
            let pies = JSON.parse(data);
            let pie = pies.find(p => p.id == id);
            if (pie) {
                Object.assign(pie, newData);
                fs.writeFile(FILE_NAME, JSON.stringify(pies), function (err) {
                    if (err) {
                        reject(err);
                    }
                    else {
                        resolve(newData);
                    }
                });
            }
        }
    });
}
```
This takes the new data, finds the pie with the appropiate id from the file, and then updates that, writes the file again.

2.  In the index.js, add the put route:
```
router.put("/:id", function (req, res, next) {
    pieRepo.getById(req.params.id, function (data) {
        if (data) {
            pieRepo.update(req.body, req.params.id, function (data) {
                res.status(200).json({
                "status": 200,
                "statusText": "OK",
                "message":`Pie ${req.params.id} updated`,
                "data": data
                });
            })
        }
    })
})
```

### Delete method
1. add the delete method to pieRepos.js
```
delete: function(id, resolve, reject) {
    fs.readFile(FILE_NAME, function(err, data) {
        if (err) {
            reject(err);
        }
        else {
            let pies = JSON.parse(data);
            let index = pies.findIndex(p => p.id == id);
            if (index != -1) {
                pies.splice(index, 1);
                fs.writeFile(FILE_NAME, JSON.stringify(pies), function(err) {
                    if (err) {
                        reject(err);
                    }
                    else {
                        resolve(index);
                    }
                });
            }
        }
    });
}
```

2. Add the delete route to index.js:
```
router.delete("/:id", function (req, res, next) {
    pieRepo.getById(req.params.id, function (data) {
        if (data) {
            // Attempt to delete
            pieRepo.delete(req.params.id, function (data) {
                res.status(200).jsonres.status(200).json({
                "status": 200,
                "statusText": "OK",
                "message":`Pie ${req.params.id} deleted`,
                "data": data
                });
            });
        }
        else {
            res.status(404).json({
                "status": 404,
                "statusText": "Not Found",
                "message": `The pie ${req.params.id} could not be found.`,
                "error": {
                    "code": "NOT_FOUND",
                    "message": `The pie ${req.params.id} could not be found.`
                }
                });
    }, function (err) {
        next(err);
    });
})
```

### Patch is used to update just a few properties, instead of a complet object.
Since the Update method uses Object.assign(), it can be used with patch.
In index.js, add
```
router.patch("/:id", function (req, res, next) {
    pieRepo.getById(req.params.id, function (data) {
        if (data) {
            pieRepo.update(req.body, req.params.id, function (data) {
                res.status(200).json({
                "status": 200,
                "statusText": "OK",
                "message":`Pie ${req.params.id} updated`,
                "data": data
                });
            })
        }
    })
})
```






    






