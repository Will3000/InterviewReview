# Interview Review

# JavaScript

## "use strict"
Strict mode makes it easier to write "secure" JavaScript.
1. Variables can't be used without declaration. Avoid accidentally create a global variable.
2. Avoid `this` refering to window object if the object context is undefined.
3. Any assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object, will throw an error.

## Hoisting
Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope. A variable can be used before it has been declared.
```Javascript
  x = 5; // Assign 5 to x
  console.log(x);
  var x; // Declare x
```

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
      console.log(this);
    }
    sayHi(); // refers the window object
  }
}

person.sayHello();
```
## Apply, Call, Bind

```Javascript
var square = {
  nums: [5,1,3]
}

function sum(arg1) {
  return arg1 + this.nums.reduce((result, current) =>{
    return result + current;
  });
}

sum.apply(square, [2]);
sum.call(square, 2);
```

## ES6
### Arrows 
It allows inner function gain access to the same lexical `this`.
```Javascript
let list = [2,3,5];
let nums = list.map( (v,i) => v+i );

//statment block
() => {
  console.log('function');
}

// Lexical this
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}

bob.printFriends();
```

### String template

```Javascript
var name = 'Wilson';
console.log(`hello my name is ${name}`);
```

### let && const

```Javascript
// var variables can be accessed in the local function scope
for(var i = 0; i<5; i++) {
  setTimeout( function() {
    console.log(i);
  } , i * 1000 );
}

// let and const variables can be accessed in the code block scope including if and loop.
for(let i = 0; i<5; i++) {
  setTimeout( function() {
    console.log(i);
  } , i * 1000 );
}

const gender = 'male';
gender = 'female'; // throws error for reassignment

```

### Modules

```Javascript
//math.js
export function sum(x,y) {
  return x + y;
} 
export var pi = 3.1415926;

//app.js
import * as math from "math";
console.log(math.sum(3,6));

//alternative way
import {sum, pi} from "math";
console.log(sum);
```
### Class

```Javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Developer extends Person {
  constructor(name) {
    super(name);
    this.type = "developer";
  }
  static isDeveloper(object) {
    return (object.type === "developer");
  }
}

```

## Functional Programming
1. First class functions: The ability to use functions as variable: pass them as parameters, return result, object properties.
2. Anonymous functions and conise lambda syntax: `x=> x * 2`
3. Closuers

### Pure functions
1. Given the same input, will always return the same output.
2. Produces no side effects.

### Impure functions
1. Output maybe vary even with the same input.
2. It relies on other functions or global variables.
3. Produces side effects.

## Object Oriented Programming
ES6 class syntax or prototype. Class is like a blue print and object is the instance being made following the instructions.
1. Encapsulation
2. Override && Overload
3. Polymorphism
```Javascript
  function Person(name) {
    this.name = name;
  }
  var wilson = new Person("Wilson");
  Person.prototype.sayHello = function() {
    console.log("Hello my name is " + this.name);
  }
  wilson.sayHello();
```
```Java 
  public class Person() {
    private String name;
    public Person(String name) {
      this.name = name;
    }
    public void sayHello() {
      System.out.println("Hello my name is " + name);
    }
  }
  
  public class Man extends Person() {
    public Man(String name) {
      super(name);
    }
    public void sayHello() {
      super.sayHello();
    }
    public void sayHello(Person person) {
      System.out.println("Hello " + person.name + ". It\'s nice to meet you.");
    }
  }
```
# Data Structure
## BST
```Java
  public class BST {
    private Node root = null;
    public int length = 0;
    public BST () {
      
    }
    
    public static void main(String args[]) {
        BST bst = new BST();
        bst.insert(3);
        bst.insert(5);
        bst.insert(1);
        bst.display();
    }
    
    class Node {
      public int data;
      public Node left;
      public Node right;
      public Node (int data) {
        this.data = data;
        this.left = null;
        this.right = null;
      }
    }
    
    public void insert(int data) {
      if (this.root == null) {
        this.root = new Node(data);
      } else {
        insertRecur(this.root, data);
      }
    }
    
    private void insertRecur(Node node, int data) {
      if (node.data < data) {
        if(node.right != null) {
            insertRecur(node.right, data);
        } else {
            node.right = new Node(data);
        }
      } 
      else {
        if(node.left != null) {
            insertRecur(node.left, data);
        } else {
            node.left = new Node(data);
        }
      }
    }
    
    public void display() {
      displayRecur(this.root);
    }
    
    private void displayRecur(Node node) {
      if ( node != null ) {
        displayRecur(node.left);
        System.out.println("The data is: " + node.data);
        displayRecur(node.right);
      }
    }
  }
  
```
## LinkedList
```Java
public class LinkedList {
  private Node root;
  class Node {
    private Node next;
    private int data;
    Node(int data) {
      this.data = data;
      this.next = null;
    }
  }
  public void push(int data) {
    
  }
  private void pushRecur(Node node. int data) {
    
  }
}
```
## Double LinkedList

## Queue && Stack

# Sorting

## Insertion
```Javascript
  function insertionSort( arr ) {
    for(var i = 0; i < arr.length; i++) {
      var selectedValue = arr[i];
      for(var j = i-1; j > -1 && arr[j] > selectedValue; j--) {
        arr[j+1] = arr[j];
      }
      arr[j+1] = selectedValue;
    }
    return arr;
  }
```
## Selection
```Javascript
function selectionSort(arr) {
  for( var i=0; i< arr.length; i++) {
    var minIndex = i;
    var min = arr[i];
    for(var j=i+1; j<arr.length; j++) {
      if (arr[j] < min) {
        min = arr[j];
        minIndex = j;
      }
    }
    if (minIndex != i) {
      var temp = arr[i];
      arr[i] = min;
      arr[minIndex] = temp;
    }
  }
  return arr;
}

```
## MergeSort

```Javascript
function mergeSort(arr) {
  if(arr.length == 1) return arr;

  var mid = arr.length/2;
  var arrayLeft = mergeSort(arr.slice(0, mid));
  var arrayRight = mergeSort(arr.slice(mid));
  return merge(arrayLeft, arrayRight);
}

function merge(arr1, arr2) {
  var i = 0;
  var j = 0;
  var result = [];
  while( i < arr1.length && j < arr2.length ) {
    if( arr1[i] < arr2[j] ) {
      result.push(arr1[i]);
      i++;
    } else {
      result.push(arr2[j]);
      j++;
    }
  }
  
  while( i < arr1.length ) {
    result.push(arr1[i]);
    i++;
  }
  
  while( j < arr2.length ) {
    result.push(arr2[j]);
    j++
  }
  
  return result;
}

```

# REST APIs
* Resource is an object or representation of something, which has some associated data with it and there can be set of methods to operate on it. Posts, Users are resources and create, read, update, delete are operations to be performed on these resources.
* URL (Uniform Resource Locator) is a path through which a recource can be located and some actions can be performed on it.

## Endpoint
* `GET /posts` get the list of all posts
* `GET /posts/2` get the post with id 2
* `DELETE /posts/2` delete the post with id 2
* Methods `GET, POST, PUT, DELETE`

## HTTP response status codes
* 200 OK 
* 301 Redirect
* 400 Bad Reuqest, 401 Unauthorized, 403 Forbidden, 404 Not Found
* 500 Internal Server Error, 503 Server Unavailable

## Passing Data

* `GET /posts?sort=rank_asc&category=technology`


