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

