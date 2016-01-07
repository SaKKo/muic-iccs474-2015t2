# ICCS474
## Internet Programming

### HTTP

Hyper Text Transfer Protocol

HTTP functions as a request-response protocol in the client-server computing model

A web browser is a good example example of a user agent (UA). Other types of user agent include
    - the indexing software used by search providers (web crawlers)
    - mobile apps
    - other software that accesses, consumes, or displays web content.

The requests are made from user-agent to the server then back to the browser.

Web browser -> Web Server -> Web browser

Together we will demonstrate how to track these requests by using python simple http server.

First we will create a new folder in our workspace. I will call it `http-python`.

```bash
$ cd ~/_workspace
$ mkdir http-python
$ cd http
```

With our new folder, we will try to serve every static files hosted in this server.

Simply create files with any text content inside.

```bash
$ touch index.html
$ echo 'hello index' > index.html
$ touch about.html
$ echo 'hello about' > about.html
$ touch contact.html
$ echo 'hello contact' > contact.html
```

Then host them using this command.

```bash
$ python -m SimpleHTTPServer 8888
```

Then open your favorite browser let's investigate what happened under `http://localhost:8888`

> - What is localhost?
> - What file will be served when you open `http://localhost:8888`?
> - Does server needs to know what is inside `index.html`?
> - Who actually use `index.html`?
> - But the content of `index.html` is not html. Why did it worked?
> - What is HTML?

#### HTTP Request methods

or HTTP Verbs are for User Agent to indicate the desired action to be performed on the identified resource.
The few most basics verbs are `GET` `POST` `PUT` `PATCH` `DELETE`, read more from the link below.

> https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

In order to see how these request methods works, we will be using nodejs `expressjs` library. http://expressjs.com/

First ensure that you have `nodejs` install on your computer. Then run this command.

```bash
$ sudo npm install express --save
```

Using nodejs on a Mac or Ubuntu is simple.

Let's start again by creating a new folder called `http-nodejs`

```bash
$ cd ~/_workspace
$ mkdir http-nodejs
$ cd http
```

create a file called `app.js` with this content.

```js
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!');
});

var server = app.listen(3000, function () {
  var host = server.address().address;
  var port = server.address().port;

  console.log('Example app listening at http://%s:%s', host, port);
});
```

start the server with this command.

```bash
$ node app.js
```

Then browse to `http://localhost:3000`

#### using curl
It's more complicated to test other request methods on the browsers. But, we don't always have to use browser to get html content. Let's do things by command line using `curl`.

```bash
$ curl -X GET http://www.google.com
```

#### GET

```js
app.get('/users', function (req, res) {
  res.send('User1, User2, User3');
});
app.get('/users/1', function (req, res) {
  res.send('User1');
});
```

```bash
$ curl -X GET http://localhost:3000/users
```

#### POST

```js
app.post('/users', function (req, res) {
  res.send('Create User');
});
```

```bash
$ curl -X POST http://localhost:3000/users
```

#### PUT

```js
app.put('/users/1', function (req, res) {
  res.send('Modify User 1');
});
```

```bash
$ curl -X PUT http://localhost:3000/users/1
```

#### PATCH

```js
app.patch('/users/1', function (req, res) {
  res.send('Partially Modify User 1');
});
```

```bash
$ curl -X PATCH http://localhost:3000/users/1
```

#### DELETE

```js
app.delete('/users/1', function (req, res) {
  res.send('Delete User 1');
});
```

```bash
$ curl -X DELETE http://localhost:3000/users/1
```
