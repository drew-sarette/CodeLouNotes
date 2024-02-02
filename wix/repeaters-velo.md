# Repeaters
A repeater is a statically or dynamically generated list of items that is displayed with the same styles on your page. 

## Populate w Static Data
Create a list of items that the repeater will show.  A repeater accepts an array of objects like this:
```
const data = [
    {
        _id: "id1",
        name: "Ima Person",
        image: "url1"
    },
    {
        _id: "id2",
        name: "Imanother Persontoo",
        image: "url2"
    }
]
```
All ojects in the array must have a unique _id property. The _id can include letters, numbers and hyphens and should follow a similar pattern to be organized.

Select the repeater with its  id, and specify where each items data should be displayed within the item. Then immediately after, assign the data to the repeater's data property.

```
$w.onReady(function () {
    $w("#repeaterId").onItemReady(($item, itemData, index) => {
        $item("#nameText").text = itemData.name;
        $item("#picture").src = itemData.image;
    })

    $w("#repeaterId").data = data
})
```
Here the onItemReady function is similar to the onReady function, but is for preparing each item with the appropriate data before it is displayed.

## Populate with Dynamic Data
To access data from the CMS, you need to know the collection id as well as the field key. Find the field key in the "properties" of the field.

This code sets up the repeater as before, but gets the data from a collection using wixData, and assigns it to customName, before putting that data into the repeater.

```
$w.onReady( async function () {
   $w("#repeaterId").onItemReady(($item, itemData, index) => {
        $item("#nameText").text = itemData.name;
        $item("#picture").src = itemData.image;
    })

    const { items: customName } = await wixData.query('collectionId').find();

    $w("#repeaterId").data = customName;
})
```

## Populate with Third Party Data 
Can fetch from an api in the backend using a web module, import that function to the frontend, and use that data in a repeater
```
import { getPlanets } from 'backend/planet.jsw';

$w.onReady(function () {
    getPlanets().then(planetInfo => {
        // can sort, change, calculate, add to, etc... the data received as planetInfo
        const processedData = planetInfo.slice().sort(sortFunc);
        
        $w("#repeaterId").onItemReady(($item, itemData, index) => {
            $item("#nameText").text = itemData.name;
            $item("#picture").src = itemData.image;
        })

        $w("#repeaterId").data = processeData
    })
})
```

## Lifecycle: Add items
can add an item to a repeater like this:

```
const newData = [{},{},{}]
$w("#repeaterId").data = $w("#repeaterId").data.concat(newData)
```

## Lifecycle: remove items
Can remove items the same way by updating the repeater data.  the onItemRemoved() method lets you do something whenever an item is removed from a repeater.

```
$w("#repeaterId").onItemRemoved((item) => {
    //do stuff here. You have access to the items data
})
```
## Lifecycle: update items
To update a specific item, first get the repeater's data property and the _id of the item to update. Find the index of the item, and update its properties.  Then use forItems method to update the displayed items in the repeater.

```
$w.onReady(function () {
    const ogRepeater = $w("#repeaterId").data;
    const idToUpdate = $w("#getItfromSomewhere").value;

    const indexToUpdate = ogRepeater.findIndex(item => item._id === idToUpdate);
    ogRepeater[indexToUpdate].something = newStuff;

    $w("#myRepeater").forItems( ["idToUpdate"], ($item, itemData, index) => {
        $item("#someElement").text = itemData.something;      
    } ) ;
})

```

## Clickable Repeaters
To get data for a repeater that was clicked on, there are two ways: 
1. For a repeater populated by connecting it to a dataset:
```
$w.onReady( function () {
  $w("#repeatedContainer").onClick( (event) => {
    let $item = $w.at(event.context);
    let clickedItemData = $item("#myDataset").getCurrentItem();
  } );
} );
```
2. For a repeater populated by setting its data property:
```
$w.onReady( function () {
  $w("#repeatedContainer").onClick( (event) => {
    const data = $w("#myRepeater").data;
    let clickedItemData = data.find(item => item._id === event.context.itemId);
  } );
} );
```