# 	JavaScript Intensiv: Sprache, Tools, Testing, Build

## 2. Tools
    * NodeJs & Npm
    * Rest API with Express
    * Npm Scripts
    * Unit testing with Jest
    * API test with Supertest
----

## Node.js
### What is Node.js
> 
Asynchronous event-driven runtime for network application. Using Javascript.
 ```JavaScript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');

  // if (req.method == 'GET') 
  res.end('Server is there!');
});

server.listen(3000, '127.0.0.1', () => {
  console.log(`Server running at http://127.0.0.1:3000/`);
});
 ```

>
## Npm
* Node package manager
* It is a **Free**, **Open-source**, and the largest Software Registry.

> Installing dependencies 
* npm install <PackageName> [ --save | --save-dev ]

## Npm Scripts
Npm can access the `scripts` property of `package.json` and therefore there is some handy commands that can help running the setting up the app.
> Running Scripts
* npm run `<script>`
```json
{
  "scripts": {
    "prestart": "echo\'before running your app!\'",
    "start": "node index.js",
    "poststart": "echo\'after running your app!\'"
  }
}
```
list of available [options](https://docs.npmjs.com/cli/v7/using-npm/scripts)


## ExpressJS
> Fast, unopinionated, minimalist web framework for Node.js.
[Express](https://expressjs.com/en/starter/installing.html)
 ```JavaScript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
 ```

 ### Middleware functions
 > are functions that have access to the request object (req), the response object (res), and the next middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named next.

### Using middleware functions
```javascript 
app.use((req, res, next) => {
  //some code here
  next();
})
```
### List of [middlewares](https://github.com/senchalabs/connect#middleware)



## Unit testing with Jest
> Jest is a JavaScript testing framework made at Facebook 

> It works with Babel, TypeScript, Node.js, React, Angular, Vue.js, etc..

#### Simple setup
```json
{
  "scripts": {
    "test": "jest"
  }
}
```
supports all common test syntaxes 

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});

// OR like this
//https://mochajs.org/#getting-started
describe('some test suite', () => {
    it('should sum 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3);
    })
})
```
#### Helper functions
> Global jest Methods [reference](https://jestjs.io/docs/api#reference) 
```javascript
afterEach(() => {
  // do something
});
```

## API test with Supertest & Jest
> A JS library to help testing HTTP APIs in very easy and simple approach.

```javascript
const app = require('../express/app.js');
const supertest = require('supertest');
const request = supertest(app);

describe('GET /get-user', () => {
  it('should return user', async () => {
    // call the API
    const response = await request.get('/get-user?name=jim');
    
    // test the response! 
    expect(response.body.name).toBe('jim');
    expect(response.body.email).toBe('jim');
  });
});
```
