web-template-rest
===

## Description

This template provides simple way to wrap RESTful service as JavaScript API.

Keywords:
* rest
* template-rest

After cloning this template, you can test first.

1. Modify endpoint in `test/FetchTemplateWebService-testx.js`.
```js
var endpoint = "http://address:port/yourapp/api/subjectName"; // modify here
var serv = new rest.FetchTemplateWebService(endpoint);
serv.queryAll(result => console.log(result));
```

2. Make sure that __endpoint__ is a `GET` API without any parameters.

3. Test.
```
npm run testfetch
```

4. Build.
```js
npm run build
```
__template-rest.js__ and __template-rest.min.js__ are outputed  to __dist__ folder.

## How It Works
### Abstract Web Services of Fetch & XHR
All implement simple __GET/POST/PUT/DELETE__ methods.

#### FetchWebService.js
* Use __Fetch__ to send request.
* Use __Promise__  to handle response.

#### XHRWebService.js
* Use __XMLHttpRequest__ to send request.
* Use __callback function__ to handle response.


### Templates of Web Service
The template provides default implementation of
* insert
* update
* delete
* queryAll
* queryOne

#### FetchTemplateWebService.js
* Extend from __FetchWebService__.

#### XHRTemplateWebService.js
* Extend from __XHRWebService__.


## Try It

### Naming Your Project
#### rollup.config.js
```js
export default {
  output: {
    name: "rest"    // define namespace
  }
};
```
#### package.json
```js
{
  "name": "template-rest" // define output file name
}
```

### Create New Web Service
* COPY, PASTE one template and RENAME to your service name.
* Modify __this.url__ in the file to actual endpoint.
* Add new methods based on your API.
* Test.

### What Different
#### Before
```js
var apiURL = "http://localhost:8080/some-app/api/v1";
var xhr = new XMLHttpRequest();
xhr.open("GET", apiURL + "/subjects");  // nightmare if subjects changed
xhr.setRequestHeader('Content-type', 'application/json; charset=utf-8');
xhr.onload = function() {
    var result = JSON.parse(xhr.responseText);
    // do something
}
xhr.send();
```
#### After - XHR
```js
var apiURL = "http://localhost:8080/some-app/api/v1";
new XHRTemplateWebService(apiURL).queryAll(
    (result) => {
        // do something
    });
```
#### After - Fetch
```js
var apiURL = "http://localhost:8080/some-app/api/v1";
new FetchTemplateWebService(apiURL).queryAll()
    .then(result = > {
        // do something
    })
    .catch();
```


## Known Issues
* require("xmlhttprequest").XMLHttpRequest can not be used in the browser.
