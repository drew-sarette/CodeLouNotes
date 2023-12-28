# Velo

## Beginner Course
### Working with page Elements
Each Wix page and every element has an id assigned automatically, however they should be named meaningfully to be used in code. Rather than document.getElementById, use $w() api to select elements and add functionality. Camelcase is recommended for id in wix.

```
$w.onReady(function () {
  // This code will run as soon as the user visits the page
  $w('some-id').hide() // selects element with some-id, and hides it.
})
```
## Velo Backend
The Backend is located in "Code Files" 
- Public allows you to access files from the frontend or backend
- Backend includes
  -- Web Modules (.jsw) which allow you to expose functions to the frontend
  -- Regular JS files
  -- Job scheduling, which can execute a function using a cron job
  -- packages, both Velo packages and NPM
  -- it is important to remember that not all npm packages will work in velo

### Web Modules
Web modules have .jsw extension. You can import backend apis, and export functions to the frontend. for example:
```
import wixData from 'wix-data';

export function firstPlanet() {
  wixData.query("collection-id")
  .find()
  .then((results)=>{
    if (results.items.length > 0) {
      let  firstItem = results.items[0];
      console.log(firstItem);
    }
})
}
```
There will be a play button to the left of a function in the editor. Click it to open the testing environment. You can set parameters and run the function. The function can be imported in the page code, and used within $w.onReady(), or outside it.

### Wix Fetch
Create a web module and import wix-fetch:
```
import wixFetch from 'wix-fetch';

export async function fetchPlanets() {
  const settings = {
    method: 'GET',
    headers: {
      Accept: 'application/json'
    }
  }

  try {
    const endpoint = new URL('urlgoes here')
    const res = await fetch(endpoint, settings);
    const data = await res.json();
  } catch(e) {
    return e;
  }
}
```

### Secrets Manager
The secrets manager can be used to securely store secrets to be accessed from the backend.
Access setret with 
```
const secret = await wixSecretsBackend.getSecret("secretName");
```

### NPM Packages
Can install common packages like lodash, stripe, axios, twilio, crypto, node-mailer. Can request packages that are not already offered, and they will be accepted or rejected within 48 hours.

### Velo Packages
Velo Packages is Wix's version of npm. First install it, then import the required functions in your code.

### Scheduled Jobs
Scheduled jobs will only run on a published site!  You cannot schedule a job to run more than once per hour. A job may not actually run exactly on time. The function to be executed must be exported. Use the validator tool in the automatically generated jobs file to create a cron expression. 


### Expose APIs
- Create a http-functions.js file (not a web module) in the backend folder.
- Functions are named ```export function <prefix>_<functionName>(request) { }```
- Functions always run with permissions of an anonymous site visitor
- Test your http functions using functional testing. You do not have to publish first.
- Functional testing is not yet supported in Wix Studio
- Must publish at least once before using testing or producion endpoints
- Prod Endpoint for premium site: ```https://www.{user\_domain}/\_functions/<functionName>```
- Testing endpoint for premium: ```https://{user\_name}.wixsite.com/{site\_name}/\_functions/<functionName>```
- free production endpoint: ```https://www.{user\_domain}/\_functions-dev/<functionName>```
- free testing endpoint: ```https://{user\_name}.wixsite.com/{site\_name}/\_functions-dev/<functionName>```




```
import { created, serverError, ok } from 'wix-http-functions';
import wixData from 'wix-data';

export function post_mySubmission(request){
  let options = {
    "headers": {
      "Content-Type": "application/json"
    }
  }

  //get the request body
  return request.body.text()
    .then((body) => {
      return wixData.insert("collectionName", JSON.parse(body));
    })
    .then((results) => {
      options.body = {
        "Message": results
      };
      return created(options);
    })
    .catch((error) => {
      options.body = {
        "error": error
      };
      return serverError(options);
    });
}

const getResponse = (body) => {
  return {
    headers: {
      "Content-Type": "application/json"
    },
    body
  }
}

export async function get_listAllPlanets(request){
  const { items: planets } = await wixData.query("Galaxy").include("planet").find();
  const response = getResponse([planets]);
  return ok(response);
}
```

Can access query params like this: 
```
import {ok, notFound, serverError} from 'wix-http-functions';
import wixData from 'wix-data';

export function get_myFunction(request) {
  // URL looks like: https://www.mysite.com/_functions/myFunction/John/Doe
  let options = {
    "headers": {
      "Content-Type": "application/json"
    }
  };
  // query a collection to find matching items
  return wixData.query("myUserCollection")
    .eq("firstName", request.path[0])
    .eq("lastName", request.path[1])
    .find()
    .then( (results) => {
      // matching items were found
      if(results.items.length > 0) {
        options.body = {
          "items": results.items
        };
        return ok(options);
      }
      // no matching items found
      options.body = {
        "error": `'${request.path[0]} ${request.path[1]}' was not found`
      };
      return notFound(options);
    } )
    // something went wrong
    .catch( (error) => {
      options.body = {
        "error": error
      };
      return serverError(options);
    } );
}

```

## Frontend
No access to html or css, only javascript and Wix's APIs.
Can access elements using the $w("elementId") api. Rename elements IDs in the properties panel.
Static events can be programmed in the properties panel.
Dynamic event hanlers can be added like this:
```
$w("elementId").onClick = () =>
```









