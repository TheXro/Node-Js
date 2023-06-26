# Node-Js
# Node.js

node is writen in c++ so v8 is wrapped in it.

It can connect to a server for content

connect to a database

read and write files on a computer

## Why Node.js?

Same language for backend and frontend

Massive community  

Can share code between frontend and backend

Huge amount of third party packages and tools to help

## The Global Object in Node

run console.log(global);

```jsx
<ref *1> Object [global] {
  global: [Circular *1],
  queueMicrotask: [Function: queueMicrotask],
  clearImmediate: [Function: clearImmediate],
  setImmediate: [Function: setImmediate] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  structuredClone: [Getter/Setter],
  clearInterval: [Function: clearInterval],
  clearTimeout: [Function: clearTimeout],
  setInterval: [Function: setInterval],
  setTimeout: [Function: setTimeout] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  atob: [Getter/Setter],
  btoa: [Getter/Setter],
  performance: [Getter/Setter],
  fetch: [AsyncFunction: fetch],
  crypto: [Getter]
}

here  are all the function that we use in global object
```

As it is global object we don’t need to specify it to use the functions

```jsx
// console.log(global);

setTimeout(() => {
    console.log('in the timeout');    //runs after 3 seconds 
    clearInterval(int); //clears the interval as soon as the timeout is done 
}
    , 3000);

const int = setInterval(() => { console.log('in the interval') }, 1000);    //runs every second

console.log(__dirname); //gives the directory name
console.log(__filename); //gives the file name
```

We cant access Window Object as node is not in browsers 

so document.(anything) will give error

## Importing and Exporting files

### require

```jsx
//const xyz = require('./people');

//people is another js files in the same dir

// to use people as it is we use 
const { people, ages } = require('./peole');

console.log(people,ages);
```

It doesn’t give access to the variables of the file people and you can’t access them 

it return an empty object 

For accessing the variables we use export.

### Export

```jsx
//in the people file
const people = ['John', 'Beth', 'Mike'];
const age = [20, 30, 40];

//module.exports = "hello"; //exports the string hello to the oht.js file

// module.exports = people;
//exports the people array to the module.js file

//you can export anything here we are exporting object which contains both people and age
module.exports = {
    people,age
};

```

Node has prebuilt objects like ‘os’

you can use them if needed

```jsx
  const os = require('os');
  console.log(os.platform(), os.homedir());

//output : linux /home/thexro
```
