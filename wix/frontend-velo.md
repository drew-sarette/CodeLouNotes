# Frontend Course
No access to html or css, only javascript and Wix's APIs.
Can access elements using the $w("elementId") api. Rename elements IDs in the properties panel.
Static events can be programmed in the properties panel.
Dynamic event hanlers can be added like this:
```
$w("elementId").onClick = () =>
```
## Wix Location API
You must publish your site to use the wixLocation API.
wixLocation.to('http://URI') can be used to send the user to any uri. You must include the http protocol.

You can use wixLocation to add a query parameter to the url. this can be used to find results in a database/dataset/repeater that meets a user's search criteria. Simply concatenate the query to the string in the to() method.

```
export function navToNewPageWithQuery() {
    const searchInput = $w("#searchInput").value;

    if (searchInput){
        wixLocation.to("/home?query=" + searchInput);
    }
}
```
If this function gets the user's query, and adds it to the url to pass that info to the next page, in this case home.

## Wix Window 
Can use to open a lightbox and send it data.
```
function openLightbox() {
    const [item1, item2] = [$w("input1").value, $w("input2.value")];
    const data = {
        "item1": item1,
        "item2"; item2
    }
    wixWindow.openLightbox("Pupup", data);
}
```
Popup is already added to the page, access it using its name(case sensetive). Can pass a data object after that. 

In the code for the popup, inside the onready function, do this to get the data:
```
$w.onReady(function () {
    let data = wixWindow.lightbox.getContext();
    $w("someElement").text = data.item1;
    $w("someOtherElement").text = data.item2;
})
```
## Wix Storage
```
import { session } from 'wix-storage';
import wixWindow from 'wix-window';

$w.onReady(function () {
    if (!session.getItem("firstVisit")) {
        wixWindow.openLightbox("FirstTime");
        session.setItem("fistVisit", "yes");
    }
})
```
checks localstorage to see if there is an item "firstVisit" stored. If not, shows the lightbox, and stores the firstVisit item in localStorage

## Test and Debug with Velo
To see console.log() in the developer console, you must be in a published version of the site. You can toggle what types of logs are shown in the Velo developer console. You can also debug and log inside of the browser's developer tools.

### Release Manager
Test sites can be set to receive a centain precentage  of visitors using the release manager.