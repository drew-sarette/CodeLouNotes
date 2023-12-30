# Datasets
A dataset is an intermediary between page elements, such as input elements and buttons, and the data in a collection. The dataset controlls which collection is available to page elements and what those elements can do with the collection data.

Datasets have three modes, and the mode cannot be changed programmatically:
- Read and Write
- Read only
- Write only

When creating a dataset for a single-item collection, the dataset can only be in Read-only mode.

The other way to work with collections and page elements is using the Data API. The wix-data API requires writing code, while the dataset allows you to take advantage of the data binding that can be set up in the Editor's connect panels.

The wix-dataset API can only be used in your site's front-end code. You do not need to import it.

