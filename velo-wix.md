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
