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
## File System

**Reading files**

Ability to read files from the filesystem using the fs module is a fundamental part of Node.js. and can't be done in the browser

For this we use one of the core module in js called **fs** module.

 hello.txt contents👇👇👇 

```
hello my name is thexro
```

```jsx
const fs = require('fs');

fs.readFile('hello.txt', (err, data) => {
    if (err) {
        console.log(err);
    }
    console.log(data.tostring()); //using tostring() as we get the data in buffer
});

//output : hello my name is thexro
```

**Writing files**

if overwrites the contents of the file 

```
//writing files

fs.writeFile('hello.txt', 'Hello World!', (err) => {
    if (err) {
        console.log(err);
    }
    console.log('File written!');
}
);
```

if a file doesn’t exist it will create a new file

**Directories**

```jsx
//directories
fs.mkdir('tutorial', (err) => {
    if (err) {
        console.log(err);
    }
    console.log('Folder created!');
}
);
```

the above function will give error if the folder already exist so we use `existsSync`

```jsx
if (!fs.existsSync('./tutorial')) {
    fs.mkdir('tutorial', (err) => {
        if (err) {
            console.log(err);
        }
        console.log('Folder created!');
    });
}
```

### Deleting files

to delete a file we use `fs.unlink` method

Sample code to delete a file named `deleteme` 

```jsx
//deleting files
if (fs.existsSync('deleteme')) {
    fs.unlink('deleteme', (err) => {
        if (err) {
            console.log(err);
        }
        console.log('File deleted!');
    }
    );
}
```

### Streams

Start using the data before it has finished loading.

For example we could wait for the data to fully loaded or we just load small amounts of data at a time without waiting.

**Read and Write streams** 

```jsx
const fs = require('fs');

const readStream = fs.createReadStream('./example.txt' , { encoding : 'utf8' });
const writeStream = fs.createWriteStream('example2.txt');
readStream.on('data', (chunk) => {
    console.log('New chunk received:');
    console.log(chunk);
    writeStream.write('\nNew chunk received:\n');
    writeStream.write(chunk);
}   
);
```

the above code creates a readstream and a writeStream into a new file

### Piping

Doing above thing but less code

```jsx
const fs = require('fs');

const readStream = fs.createReadStream('./example.txt' , { encoding : 'utf8' });
const writeStream = fs.createWriteStream('example2.txt');

readStream.pipe(writeStream);

# Module

```jsx

```

encapsulated code only sharing minimum 

# Communication between server and browser

first browsers sends a request and the servers looks the requests and decide what to send back

it could be html page, images , json etc 

How does browsers know which to send request to 

for this lets look on ip addresses 

i we want to connect to a server we need a ip address of the server 

we use domain name as ip address are complex to learn

## GET Requests

when the browsers send request to the server when we type domain name and hit enter we are sending a GET request that will give something back

the communication occurs via HTTP 

## Creating a server

For creating a server we use http module 

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
	console.log("Request Made");
}
);

server.listen(3000);

```

The request object

## The Request Object

It contains loads of stuff like url `req.url`, method used `req.method`  etc.

```jsx

const http = require('http');

const server = http.createServer((req, res) => {
    //set header content type
    res.setHeader('Content-Type', 'text/plain');
    res.write('Hello World');
    res.end();

}
);

server.listen(3000 , () => {console.log('listening on port 3000');});

```

we can use html also 👇👇👇

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
    //set header content type
    res.setHeader('Content-Type', 'text/html');
    res.write('<h1>Hello World</h1>');
    res.end();
}
);

server.listen(3000 , () => {console.log('listening on port 3000');});
```

the browser will automatically make the body head tags

but this is not the ideal way to send html

the best way is to make separate files and use the fs module

```jsx
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    //set header content type
    res.setHeader('Content-Type', 'text/html');

    //send a html file
    fs.readFile('./views/index.html', (err, data) => {
        if(err){
            console.log(err);
            res.end();
        }else{
            // res.write(data);
            // res.end();
            //or as one one thing is being sent we can use end
            res.end(data);
        }
    })
})
;

server.listen(3000 , () => {console.log('listening on port 3000');});
```