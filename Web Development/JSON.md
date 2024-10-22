# JSON
Stands for JavaScript Object Notation. It is a Data Representation Format similar to YAML or XML, and is used widely for API's and config files. It is extremely lightweight, and more readable than XML. It integrates well with JS, and nearly every language has tools to work with JSON

## JSON types
Strings, numbers, booleans, null, arrays, objects. But mostly objects.

Any of these types are valid JSON. However, the top level of the .json file is typically an array or object, and the contents are other values.

## Example
This sample json file contains an object representing a user:

```
{
    "name": "Whomever",
    "favoriteNumber": 68,
    "isAlive": true,
    "hobbies": ["sniffing cakes", "counting stars"],
    "friends": [{
        "name": "somebody",
        "favoriteNumber": 4,
        "isAlive": false,
        "hobbies": ["pushing up daisies", "counting worms"],
        "friends": [...]
    }]
}
```
Note that all keys must be in double quotes in JSON.
## JSON.parse()
JSON.parse() takes a string and converts it to a javascript object.