[youtube link](https://www.youtube.com/watch?v=GZvSYJDk-us)

# Application Programming Interface
- Interface is a way of controlling a device or software without knowing how exactly it works.
- Pretty much every built in function in a language is an API. They abstract away the details of how basic tasks get done.
- Web APIs allow you to access computational power as well as huge amounts of data from mobile devices
    - Google Translate's AR does complex computations and sends back lots of data

# how the web works
URI = Universal Resource Identifier
- www.google.com for example
URL = Universal Resource Locator
- includes the protocol
- http://www.google.com for example

client = the machine requesting a document
server = machine serving documents and services to clients
HTML = HyperText Markup Language

Clients request a document via HTTP when the url is entered in the browser. The request is typically either a GET, POST, FETCH or other request

The server returns a response including headers, and a body containing the HTML in most cases. 

# RESTful API
Rest stands for REpresentational State Transfer
- Client-Server architecture
- Statelessness - server remembers nothing about the client from request to request. Login details must be sent each time
- Layered System
- cacheability
