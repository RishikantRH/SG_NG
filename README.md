# Angular Training

Banuprakash C

Full Stack Architect,

Co-founder Lucida Technologies Pvt Ltd.,

Corporate Trainer,

Email: 
banu@lucidatechnologies.com; 
banuprakashc@yahoo.co.in

https://www.linkedin.com/in/banu-prakash-50416019/

https://github.com/BanuPrakash/SG_NG
----------------------------------------------------------

Softwares Required:
1) Visual Studio Code.
2) Chrome Web Browser
3) NodeJS Latest LTS
----------------------------------------------------
Day 1) JS, ES2015/ ES6, NodeJS, Webpack and TypeScript
Day 2 and 3) Angular
-------------------------------------------------------
JavaScript: Scripting language, loosely typed
Runs on JS engine [developed using C++] ==> V8 [google], SpiderMonkey, Chakra, NashHorn, ...

myFile.js
var g = 100;

function add(x, y) {
    var result = x + y;
    return result;
}
var res = add(4,5);
console.log(res);

Execution Context: Global Creation Phase, Global Execution Phase, Function Creation Phase & execution Phase
-----------------------------------------------------------------

var g = 100;
function doTask() {
    var a = 10;
    if( g > a) {
        var b = 20;
        c = 50;
    }
    console.log(g,a,b,c)
}
doTask();

console.log(g,a,b,c);
-------------------------------------

function add(x,y) {
    return x + y;
}

console.log(add(4,5)); // 9

-------------
Engine introduces semi-colon when before performing AST 
function add(x,y) {
    return 
        x + y;
}

console.log(add(4,5)); // undefined
------------------------------------------------------------

JS is single threaded and event-loop based

console.log("Hi");

setInterval(function dotask(){
    comsole.log("Time out!!)
}, 10);

$("#btn").click(function clicked() {
    console.log("clicked!!!);
});


console.log("Bye");
-------------------------------


psuedocode for event loop
var pendingTimers = [];
var pendingCallbacks= [];
var pendingOsTasks = [];

function shouldContinue() {
    return pendingTimers.length >0 || pen dingCallbacks > 0 ...
}
while(shouldContinue()) {

}
setInterval(function dotask(){
    another();
}, 10);


function another() {
    second();
}

function second();
---------------------------------------------------

OOP with JS

1) function constructor with class owned instance methods

function Person(name, age) {
    this.name = name; //state
    this.age = age; // state
}
//instance methods
Person.prototype.getName = function() {
    return this.name;
}
Person.prototype.getAge = function() {
    return this.age;
}
//static methods
Person.getCount = function () {
    return 100;
}

var p1 = new Person("Raj", 34);
p1.getName();
p1.getAge();
Person.getCount();
-----------

1) function constructor with object owned instance methods

function Person(name, age) {
    this.name = name; //state
    this.age = age; // state
    this.getName = function() {
        return this.name;
    }
    this.getAge = function() {
        return this.age;
    }
};

var p1 = new Person("Raj",55);
var p2 = new Person("Smitha",21);

p1.getName();
p1.getAge();
========================

JSON ==> JavaScript Object Notation  {} ==> usually used to represent state ==> carriers of data

var obj = {}; // object

var person = {
	"id": 1,
	"name" : "Smith",
	"age" : 32,
	"getAge": function() {
		return this.age;
	}
};

person.age;

person.getAge();

=================
understanding "this" and bind()

var obj = {
	"age" : 100
};

var person = {
	"id": 1,
	"name" : "Smith",
	"age" : 32,
	"getAge": function() {
		return this.age;
	},
	"getName" : function() {
		return this.name
	}
};

var ref = person.getAge;

ref(); // undefined ==> Context is lost ==> this refers to "window"


ref = person.getAge.bind(person); // when reference is taken copy "person" context as "this"
ref(); // 32

ref = person.getAge.bind(obj); // when reference is taken copy "person" context as "this"

ref(); // 100
================

function add(x,y) {
	return x + y;
}

var add = new Function("x", "y", "return x + y");
======================================================
call & apply

function updateAge(age) {
	this.age = age;
}


var obj = {
	"age" : 100
};

var person = {
	"id": 1,
	"name" : "Smith",
	"age" : 32
}

updateAge.call(obj,99);
obj.age; // 99

updateAge.call(person,55);
person.age; // 55
-------------------------------------------------------------

Functional Programming with JS
------------------------------

OOP ==> methods() ==> thightly coupled to state of object
	Account ==> credit() and debit() => uses "balance" state

functional style of programming -=> functions which can be used on any type of data [ objects, prmitives,..]
	Example: filter, iterate, map,...

	Functional style of Programming uses High Order Functions:
		1) functions which accept function as argument
		2) function which returns a function
		==> treat function as first-class members [ primitive , object]

	var x = 10;

	x = function() {

	}

	x = {}
-------------------------------

Without HOF:

var data = [6,41,2,11,77];

for(var i = 0; i < data.length; i++) {
	console.log(data[i]);
}

for(var i = 0; i < data.length; i++) {
	alert(data[i]);
}

With HOF:

function forEach(elems, action) {
	for(var i = 0; i < elems.length; i++) {
		action(elems[i]);
	}
}

forEach(data, console.log);
forEach(data, alert);

function someTask(elem) {
		writeToFile(elem)
}
forEach(data, someTask);
--------------------------------------------

Commonly used HOF:
filter, map, reduce, forEach, flatMap, skip, limit,..

	filter ==> subset 
	map ==> transform
	reduce ==> aggregate [ sum, ,max, avg, count] 
	forEach --> iterate
	flatMap => convert one type of stream to another type of stream

 var products = [
       {"id":1,"name":"iPhone","price":124447.44,"category" : "mobile"},
       {"id":2,"name":"Onida","price":4444.44,"category" : "tv"},
       {"id":3,"name":"OnePlus 6","price":98444.44,"category" : "mobile"},
       {"id":4,"name":"HDMI connector","price":2444.00,"category" : "computer"},
         {"id":5,"name":"Samsung","price":68000.00,"category" : "tv"}];


         function filter(elems, predicateFn) {
         	create array
         		loop thro elem in elems
         			if predicateFn(elem)
         				add to array
         		end loop
         	return array
         }
-----------------------

  function map(elems, transformFn) {
         	create array
         		loop thro elem in elems
         			add to array transformFn(elem)
         		end loop
         	return array
 }
---------------
https://rxmarbles.com/
---------------------------------------------------

HOF 2: functions returning functions ==> Closure

without closure:
// pure function
function greeting(msg, name) {
	return msg + " " + name;
}

greeting("Good Morning", "Geetha");
greeting("Good Morning", "Sita");
greeting("Good Morning", "Harry");


With Closure using HOF:

function greeting(msg) {
	return function(name) {
		return msg + " " + name;
	}
}

var mg = greeting("Good Morning");


mg("Geetha");
mg("Sita");

Closure is a concept wherein inner function has an access to members of outer functions

===========

Implementing Memoziation design pattern with Closure [ cache]

getEmployee(24); ==> REST call to server get JSON

subsequent calls to getEmployee(24); should get from cache

getEmployee(2); ==> REST call for different employee

===========

Without memoization:
function fibanocci(no) {
            return no == 0 || no == 1 ? no : fibanocci(no - 1) + fibanocci(no - 2);
        }

        console.time("first");
         console.log(fibanocci(34));
        console.timeEnd("first");

        console.time("second");
         console.log(fibanocci(34));
        console.timeEnd("second");

------------

With memoization:


function memoize(fn) {
            var cache = {};
            return function(arg) {
                if(!cache[arg]) {
                    cache[arg] = fn(arg);
                }
                return cache[arg];
            }
        }
        function fibanocci(no) {
            return no == 0 || no == 1 ? no : fibanocci(no - 1) + fibanocci(no - 2);
        }
        var memFib = memoize(fibanocci);

        console.time("first");
         console.log(memFib(34));
        console.timeEnd("first");

        console.time("second");
         console.log(memFib(34));
        console.timeEnd("second");
------------------------------------------------
ES 5 is supported by almost all current browsers

ES 2015 / ES 6
ECMAScript

Development can happen in ES6, we use Transcompiler to convert to lower version ==> ES5

Transcompiler , Transpiler ==> Babel, Traucer

Babel is a free and open-source JavaScript transcompiler that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript.

New Features of ES 2015 / ES 6
1) scope variables [ let and const]


var g = 100;
function doTask() {
    var a = 10;
    if( g > a) {
        let b = 20; // scope is within block; with "var" hoisted to function scope
        c = 50;
    }
    console.log(g,a,b,c); // b is not visible
}
doTask();

console.log(g,a,b,c);
---------

const PI = 3.14159; // constant 

2) Arrow Operator ==> Lambda expression and default values

function add(x,y) {
	return x + y;
}

with Arrow operator

let add = (x,y) => {
	return x + y;
}

also

let add = (x,y) => x + y;

also

let add = (x = 0, y = 0) => x + y;

add(); // 0
add(5); // 5
add(4,5); // 9

without default and arrow:

function add(x,y) {
	x = x || 0;
	y = y || 0;
	return x + y;
}
--------------

https://caniuse.com/

3) Destructing arrays

	var colors = ["red", "green","blue","orange","pink"];

	ES 5:
		var r = colors[0];
		var g = colors[1];

	with ES 6:

	let [r,g,b,...others] = colors;

	r will be red
	b is blue
	others  will be ["orange","pink"];


[...] spread operators

4) Destructing objects

let p = {"id":1,"name":"iPhone","price":124447.44,"category" : "mobile"};


// Traditional way:
console.log(p.name, p.age); // iPhone

// ES6:
let {name,price} = p;
console.log(name, price ); // iPhone, 124447.44

or
let {name:n,price:amt} = p;
console.log(n, amt ); // iPhone, 124447.44

5) new way to clone 

var colors = ["red", "green","blue","orange","pink"];
 
let ref = colors;
 
ref[0] ="GOld"
"GOld"

colors
(5)??["GOld", "green", "blue", "orange", "pink"]
ref
(5)??["GOld", "green", "blue", "orange", "pink"]



Clone using spread operator:
var colors = ["red", "green","blue","orange","pink"];

let clone = [...colors];
clone[0]="Magenta"
"Magenta"
clone
(5)??["Magenta", "green", "blue", "orange", "pink"]
colors
(5)??["GOld", "green", "blue", "orange", "pink"]
---------------------------------------------------

6) Template Literals

ES5: strings can be in "Hello" or 'Hello'

ES6: `tick operator`

var name = "Peter";

var msg = `Welcome ${name},
to Angular Training
Virtual Training`


var elem = `<div>
<h1>${customer.firstName}</h1>
<h2>${customer.lastName}</h2>
<p> Welcome to Angular</p>
</div>`

--------------------------

7) Promise API ==> Asynchronous code execution ==> execute side effects
	Promise => resolve , reject
	Java: Future and Callable

	fetch('https://jsonplaceholder.typicode.com/users/1')

	synchronous method calls:

	let res = doTask();
	console.log(res); // this code executes only after doTask() is complete

	Promise APIs: assume doTask() is promise based
	doTask()
		.then(
			(data) => console.log(data) /*resolved code */,
			(err) => cosole.log(err) /* rejected code */);

	console.log("Hello"); // executes before doTask() completes

	-----
	doTask()
		.then(
			(data) => console.log(data) /*resolved code */,
			(err) => console.log(err) /* rejected code */)
		.catch(ex) {
			console.log(ex)
		};
--------------

8) async and await for Promise API to avoid nested callbacks
-------------

9) Generators are functions with multiple return values
	
	function* saga() {
		console.log("task1");
		console.log("task2");
		yield "result 1";
		console.log("task3");
		console.log("task4");
		yield 100;
	}

	let iter = saga();
	iter.next(); 
	iter.next();
-----------------------------
10) Module System and class
	
	Prior to ES 6: IIFE was used as module system ()();
	Immediate Invoke Function expression
	let customerModule = (function () {
		let g = 100; // private to customerModule
		function one() {
			console.log(g);
		}

		function two() {
			console.log(g);	
		}
	})();

	let orderModule = (function () {
		let g = 500;
		function three() {
			console.log(g);
		}

		function two() {
			console.log("SS", g);	
		}
	})();
-----------

	ES 6 Module System and class

	person.js
	export class Person {
		 constructor(name, age) {
		 	this.name = name;
		 	this.age = age;
		 }

		 getName() {
		 	return this.name;
		 }
	}

	other.js
	import {Person} from './person';

	let p = new Person("Sam", 43);

	=============

	lib.js

	export add = function(x, y) {
		return x + y;
	}

	export sub = function(x, y) {
		return x - y;
	}

	let mul = function(x,y) {
		return x * y;
	}

	other.js
	import {add, sub} from './lib';
	console.log(add(5,6));
	================================

	person.js
	export default class Person {
		 constructor(name, age) {
		 	this.name = name;
		 	this.age = age;
		 }

		 getName() {
		 	return this.name;
		 }
	}

	other.js
	import Person from './person';

	let p = new Person("Sam", 43);
===================

Node.js, webpack and TypeScript 
===============================

Node.js ==> an environment with V8 JavaScript engine
	Why Node.JS?
		1) To build realtime streaming API [ for Java: Netty with WebFlux]
			build RESTful web services/ GraphQL
		2) To build standalone application
		3) as build environment for client-side web applications

	As Build environment for client-side applications with the help of build tools:
		* code might be written in TypeScript, ES6, CoffeeScript, LiveScript
		 Transpile thme to ES5 to make it portable across browser
		* We might use Module systems, which are not understood by browsers, we might need
			to bundle them [ Browserify]
		* minify, uglify to reduce payload	
	-------------------------
	WebAPI ==> Libuv [ C++ library]

	Node.js when started loads many pre-defined modules [ fs, http, crypto, repl, cluster]
	NPM / YARN ==> Node Package Manager is handle 3rd party modules
			* download, update, upload

	Project specific modules
		npm install react
	executable modules
			npm install -g json-server

	Every node.js project has "package.json" ==> pom.xml used by Maven
	1) package.json
	{
		"dependencies": {
			"@angular/core": "^8.0.1"
		}
		"devDependencies": {
			"jest": "~26.6.3"
		},
		"scripts": {
			"start" : "ng  serve --port 1234",
			"test": "mocha --spec line"
		}
	}

	npm start

	2) "node_modules" folder
		place where dependencies are downloded for the project
--------------------------------------------------------------------
	Person.js
	babel Person.js ==> Person.js with ES5

	JavaScript build tools ==> to automate tasks like : transcompiler, lint, testing, uglify,
	minify, bundle


	1) Grunt
	2) Gulp
	3) Webpack

	Grunt is a JavaScript task runner, a tool used to automatically perform frequent tasks such as minification, compilation, unit testing, and linting. 


	CommonJS module system

	lib.js

	module.exports.add = function(x,y) {..}

	module.exports.sub = function(x,y) {..}	


	other.js

	let lib = require('./lib');

	console.log(lib.add(4,5));
----------------
index.html

<script src="funcs.js"></script>
<script src="Person.js"></script>
<script src="index.js"></script>
======================================================
 "bootstrap": "^4.6.0",
  "font-awesome": "^4.7.0",

@import 'bootstrap/dist/css/bootstrap.min.css';

@import 'font-awesome/css/font-awesome.css';

npm i -g @angular/cli@latest
ng --version

npx -p @angular/cli ng new customerapp
npx ng g c 
========================



Day 1 Recap: 
JS, Execution Context, Event loop, callbacks, Functional style of programming, 
HOF, Closures, memoize pattern, ES 6 features, ES 6 module system [ exports and import],
Node.JS as build environment, webpack JavaScript Build tool 


Day 2
------
JavaScript ==> loosely typed and dynamically typed

TypeScript => datatypes for JavaScript

JS engine

ESNext, TypeScript, CoffeeScript, DART, LiveScript are used only in development stage
these are transcompiled into JS for production.

ESNext or ES6 we use babel
babel a.js

TypeScript
npm i -g typescript

Person.ts

tsc Person.ts ===> Person.js [ production]

TypeScript datatypes:

1) Number
	
	let x:number = 10;
	x = "A"; // error

2) String
	let name:string = "Peter";

3) boolean
	let flag:boolean = true;

4) Array type

	let data:number[] = [5,3,62];

	or

	let data:Array<number> = [5,326,2];

5) any

	let data : any;

	data = doTask(); // not sure what type of data this method returns

	// allows to use behaviour on return type

	data.toUpperCase(); // runtime
	data.firstName; // valid for tsc
6) unknown

	let data : unknown;

	data = doTask();

	data.toUpperCase(); //error
	or
	data.firstName; // error

7) enum
	enum Priority {
		LOW, MED, HIGH
	};

	let bug:Priority = Priority.HIGH;

8) void

9) interface
		8.1 ) to define a shape

			interface Person {
					id:number,
					name:string,
					address?: string
			}

			function addPerson(person: Person): void {

			}

			addPerson({"id":2,"name":"Priya"}); // valid
			addPerson({"id":2,"name":"Priya", "address": "some address"}); // valid

			addPerson({ "name":"Priya", "age": 23}); // invalid

		8.2) to define a contract
			interface Flyable {
				fly(): void
			}

			class Bird implements Flyable {
				//

				fly(): void {

				}
			}
9) Tuple
	
	let x:[string,number] = ["Hello", 5];

10) never

	function doTask(): never {
		throw new Error("Boom :-(")
	}
=============

	TSX ==> TypeScript and XML

	function Welcome(props) {
		return(
				<div>
						<h1> {props.name} </h1>
				</div>
			)
	}
===================

TypeScript Decorators [ metadata] @decoratorName

Metdata can be placed on class, function, fields ...

@Component({
	"selector": "<product>",
	"templateUrl" : `<div>....</div>`
})
public class ProductComponent { 
	products:Product[] = []; //state

	deleteProduct(id:number):void { // behaviour

	}
}

HTML
	<product></product>

@Component({
	"selector": "<customer>",
	"templateUrl" : `<div>....</div>`
})
public class CustomerComponent { 
	customers:Customer[] = []; //state

	deleteCustomer(id:number):void { // behaviour

	}
}

Object.defineProperty(CustomerComponent.prototype, "selector", {value : "<customer>"});

const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});

object1.property1 = 77;
// throws an error in strict mode

console.log(object1.property1);
// expected output: 42


============

Creating Decorators is using HOF using Closure
==================================================
