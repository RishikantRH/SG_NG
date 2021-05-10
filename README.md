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
(5) ["GOld", "green", "blue", "orange", "pink"]
ref
(5) ["GOld", "green", "blue", "orange", "pink"]



Clone using spread operator:
var colors = ["red", "green","blue","orange","pink"];

let clone = [...colors];
clone[0]="Magenta"
"Magenta"
clone
(5) ["Magenta", "green", "blue", "orange", "pink"]
colors
(5) ["GOld", "green", "blue", "orange", "pink"]
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

