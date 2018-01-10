---

@title[Introduction]
### NODE JS
---
@title[what is Node?]
### So, what is Node?
- Open source server framework
- Free
- Runs on various platforms (Windows, Linux, Unix, Mac OS X, etc.)
- Uses JavaScript on the server
---
@title[Why Node.js?]
### Why Node.js?
- Asynchronous programming
- Eliminates the waiting
- Runs single-threaded, non-blocking
---

@title[Getting started with Node]
### Getting started with Node
- Download and Install Node for your machine at: https://nodejs.org/
- Click on the big green Install button
- Create a Node.js file named "myfirst.js", and add the following code:

```js
var http = require('http');

http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.end('Hello World!');
}).listen(8080);
```
---
@title[Node.js Modules]
### Node.js Modules
- Http module
- File system
- Event module

+++

@title[Http Module]
### Http Module

```js
var http = require('http');
var url = require('url');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  var q = url.parse(req.url, true).query;
  var txt = q.year + " " + q.month;
  res.end(txt);
}).listen(8080);
```
+++

@title[File system]
### File system
- Read/Create/Update/Delete/Rename files
```html
<html>
<body>
<h1>My Header</h1>
<p>My paragraph.</p>
</body>
</html>
```

```js
var http = require('http');
var fs = require('fs');
http.createServer(function (req, res) {
  fs.readFile('demofile1.html', function(err, data) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    res.end();
  });
}).listen(8080);
```
+++

@title[Event module]
### Event module
- Node.js has a built-in module, called "Events", where you can create-, fire-, and listen for- your own events.
- All event properties and methods are an instance of an EventEmitter object

```js
var events = require('events');
var eventEmitter = new events.EventEmitter();

//Create an event handler:
var myEventHandler = function () {
  console.log('I hear a scream!');
}

//Assign the event handler to an event:
eventEmitter.on('scream', myEventHandler);

//Fire the 'scream' event:
eventEmitter.emit('scream');
```
---
@title[NPM]
### NPM 
- NPM is a package manager for Node.js packages, or modules
- www.npmjs.com hosts thousands of free packages to download and use.
- Download a Package
- Using a Package

```sh
C:\Users\Your Name>npm install upper-case
```

```js
var uc = require('upper-case');
```
---

@title[Node.js MongoDB]
### Node.js MongoDB
- Install Mongo
- Install MongoDB Driver

```sh
C:\Users\Your Name>npm install mongodb
```
- Creating a Database
- Creating a Collection

+++ 

@title[Creating a Database]
### Creating a Database 
- MongoDB will create the database if it does not exist, and make a connection to it.

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/mydb";

MongoClient.connect(url, function(err, db) {
  if (err) throw err;
  console.log("Database created!");
  db.close();
});
```
+++ 

@title[Creating a Collection]
### Creating a Collection
- To create a collection in MongoDB, use the createCollection() method:

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/mydb";

MongoClient.connect(url, function(err, db) {
  if (err) throw err;
  db.createCollection("customers", function(err, res) {
    if (err) throw err;
    console.log("Collection created!");
    db.close();
  });
});
```
---
@title[Node.js - Express Framework]
### Node.js - Express Framework
- Allows to set up middlewares to respond to HTTP Requests.
- Defines a routing table which is used to perform different actions based on HTTP Method and URL.
- Allows to dynamically render HTML Pages based on passing arguments to templates.

```sh
$ npm install express --save
```
+++ 

@title[Hello world Example]
### Hello world Example

```js
var express = require('express');
var app = express();

app.get('/', function (req, res) {
   res.send('Hello World');
})

var server = app.listen(8081, function () {
   var host = server.address().address
   var port = server.address().port
   
   console.log("Example app listening at http://%s:%s", host, port)
})
```
+++
@title[Basic Routing]
### Basic Routing

```js
var express = require('express');
var app = express();

// This responds with "Hello World" on the homepage
app.get('/', function (req, res) {
   console.log("Got a GET request for the homepage");
   res.send('Hello GET');
})

// This responds a POST request for the homepage
app.post('/', function (req, res) {
   console.log("Got a POST request for the homepage");
   res.send('Hello POST');
})

// This responds a DELETE request for the /del_user page.
app.delete('/del_user', function (req, res) {
   console.log("Got a DELETE request for /del_user");
   res.send('Hello DELETE');
})

// This responds a GET request for the /list_user page.
app.get('/list_user', function (req, res) {
   console.log("Got a GET request for /list_user");
   res.send('Page Listing');
})

// This responds a GET request for abcd, abxcd, ab123cd, and so on
app.get('/ab*cd', function(req, res) {   
   console.log("Got a GET request for /ab*cd");
   res.send('Page Pattern Match');
})

var server = app.listen(8081, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("Example app listening at http://%s:%s", host, port)
})
```
+++

@title[Serving Static Files]
### Serving Static Files
- Express provides a built-in middleware express.static to serve static files, such as images, CSS, JavaScript, etc.

```js
var express = require('express');
var app = express();

app.use(express.static('public'));

app.get('/', function (req, res) {
   res.send('Hello World');
})

var server = app.listen(8081, function () {
   var host = server.address().address
   var port = server.address().port

   console.log("Example app listening at http://%s:%s", host, port)

})
```