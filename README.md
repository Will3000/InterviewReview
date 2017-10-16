# Interview Rview

# JavaScript

## Closure

A closure is an inner function that has access to the variables in its local, parent and global scope.
```Javascript
function outerFunction() {
  var a = "outter";
  function innerFunction() {
    console.log(a);
  }
  innerFunction();
}
outerFunction();
```

## Callback && Event Loop

Synchronous programming means that, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.
A callback function is an asynchronous function which executes the code contained within the function at a certain time (not in a sequential order). Event loop will carry out the call back queue if main stack is empty. So it won't block the application.

```Javascript
$.ajax({
  url: 'www.dev.com',
  action: 'get',
  success: function(res) {
    console.log(res); // the code is executed when the ajax call is completed
  }
});

setTimeout( function(){ console.log(1)}, 200);
console.log(2);
setTimeout( function(){ console.log(3)}, 0);

```

## Promise
Promise design is one way to avoid callback hell.
 ```Javascript
 var pr1 = function(res=[]) {
  return  new Promise( (resolve, reject) => {
   setTimeout( ()=>{ 
     console.log('1');
     res.push('resolved1');
     resolve(res); 
   } , 3000);
 });
 }
 
 var pr2 = function(res) {
  return new Promise( (resolve, reject) => {
   setTimeout( ()=>{ 
     console.log('2');
     res.push('resolved2');
     resolve(res); 
   } , 3000);
 });
 }
 
 var pr3 = function(res) {
 return  new Promise( (resolve, reject) => {
   setTimeout( ()=>{
     console.log('3');
     res.push('resolved3');
     resolve(res); 
   } , 3000);
 });
 }

 // chain promises in sequential order
 pr1()
   .then(pr2)
   .then(pr3)
   .then( result => console.log(result))
   .catch( error => console.log(error));
 
 // wait for all promises finish before excecute the code
 Promise.all([pr1(), pr2(), p3()])
   .then( result => console.log(result));
 ```

## Kewword `this`
Calling `this` inside a object function will refer to the object else it refers to the window object in browser. Node server doesn't have window object.

```Javascript
var person = {
  name: 'Wilson',
  sayHello: function() {
    console.log(this); // refers to person object
    function sayHi() {
      console.log(this)
    }
    sayHi(); // refers the window object
  }
}

person.sayHello();
```

## ES6
### fat arrow function 
() => {
  console.log('function');
}

### string template using

```Javascript
  var name = 'Wilson';
  console.log(`hello my name is ${name}`);
```


## Functional Programming
1. First class functions: The ability to use functions as variable: pass them as parameters, return result, object properties.
2. Anonymous functions and conise lambda syntax: `x=> x * 2`
3. Closuers

### Pure functions
1. 

## Object Oriented Programming

