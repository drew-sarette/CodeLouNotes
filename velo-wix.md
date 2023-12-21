## Working with page Elements
Each Wix page and every element has an id assigned automatically, however they should be named meaningfully to be used in code. Rather than document.getElementById, use $w() api to select elements and add functionality. Camelcase is recommended for id in wix.

```
$w.onReady(function () {
  // This code will run as soon as the user visits the page
  $w('some-id').hide() // selects element with some-id, and hides it.
})
```
