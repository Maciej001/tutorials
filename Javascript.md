# Javascript programming with safaribooksonline

```
var msg = document.getElementById("message”);
msg.textContent = output;
```

add HTML to element
`msg.innerHTML += "<p><strong>Original order:</strong> [" + v + "]<p>";`


## Conditions

### if statement
``` 
	if (condition) {}
	else if {}
	else {}
```

### for loop

```
for (var i = 2, output = 1; i <= num; i++) {
	output *= i;
}
```

### while loop

Make the num at least characters long with leading zeros

```
while (num.length < 8) {
	num = "0" + num;
}
```

or

This one will execute at least one time, as the condition is checked at the end.
num will always have at least one leading zero.

```
do {
	num = "0" + num;
} 
while (num.length < 8) 
```

bonus: the same without a loop

```
	num = ("00000000" + num).substr(-8) / last 8 charachters
```


## Functions

Function with 'a' parameter set to a or if a is undefined to ""

```
function showMessage(a, b, c) {
	a = a || "";    
}
```

### special variable -> arguments

holds all the arguments of the function
```
function showMessage() {
	arguments[1]    // second argument passed to the function
	arguments.length // number of arguments
}
```

## Arrays

define array:
`var v = [];`

`push` 		- adds element to the end 
`pop` 		- removes last element and returns it 
`unshift` - adds element at the end
`shift` 	- removes and returns first element of the array

`array3 = array1.concat(array2)`

avoid using:
`delete v[4]`    deletes 5th element of the array and sets it to undefined but lenght of array does not change.

`v.reverse();`   reverses the array
`new_v = v.slice(2,4);`	 slices out few elements starting at index 2 ending at index 4. v array is left untouched
`new_v = v.slice(2);`    returns all the elements from index 2 to last element
`new_v = v.slice(2, -1);`  slice from index 2 to last -1 index

splice changes the original array!
`splice(index, howMany, comma-separated-list-of-elements)` - removes items from array, from index, howMany, and 
adds in their place coma-separated-list-of-elements.

`v.join("-")` takes every element and joins them using '-' as separator

`v.sort()` - without arguments it sorts elements if these were strings
`v.sort(function(a,b) {return a-b;});` sorts an array by comparing elements as numbers
remember to pass function to sort without calling it function instead of function()

sort by length
```
new = array.(SortByLength)

function SortByLength(a, b) {
	return a.length - b.length
}
```


## Objects

`var car = {};`  // will destroy any car variable elsewhere in the program

`var car = car || {};`  // bit better 

```
car.make = "Ford";
car.color = "blue"; // or
car["color"] = "red";

car.display = function() {
	console.log("Car color is " + this.color);
}

car.display();			// or
car["display"]();
```

better

```
var car = car || {
	make: "Ford", 
	model: "Mustang",
	color: "blue",
	display: function() {
		console.log("Car color is " + this.color);
	}
};
```

### Defining constructor

Initializer:
```
function car(make,model,color) {
	this.make  = make || "Uknown";  // setting default
	this.model = model;
	this.color = color;
	this.display = function() {
		console.log("This make is " + this.make);
	}
}

// create objects

var c1 = new car("Ford", "Mustang", "blue");
c1.display();
```

Every time you create new instance variable, it will have new .display() method. It's waist of resources.
Instead we should create prototype functions: 

```
function car(make,model,color) {
	this.make  = make || "Uknown";  // setting default
	this.model = model;
	this.color = color;
}

car.prototype.display = function() {
		console.log("This make is " + this.make);
}

// create objects

var c1 = new car("Ford", "Mustang", "blue");
c1.display();
```

Every car is an Object so you could write

`Object.prototype.display = function() {}` and it would work for any object created.

You can add methods to any Javascript Object. Let's define reverse method for String.

```
String.prototype.reverse = function() {
	this.split("").reverse().join("");
}
```

## Math functions

`Math.PI`
`Math.round(9.5);`  // 10
`Math.ceil(9.5);`  // 10
`Math.floor(9.5);` // 9
`Math.abs(-9.5);`  // 9.5
`Math.pow(10,2);`  // 100 - power of
`Math.min(0, 9);`
`Math.max(0, 10);`
`Math.random();`		 // 0 - 1
`Math.floor(Math.random() * 10 + 1);` // random number 1 - 10

all trygonomical functions take radians. So you have to transform degrees into radians using:
```
function degrees(x){
	return x/360 * 2 * Math.PI;
}

Math.sin(degrees(90));      // 1 wow!
```

## Strings functions

convert to String
```
var a = [1,2,3];
var s = a.toString();    / "1,2,3"
```
or 

```
var i = 99;
var s = String(i);
```

string from Unicode values
`var s = String.fromCharCode(65,66,67);`    // "ABC"

`"abcde".length`  // 5

`s.toLowerCase();`
`s.toUpperCase():`

joining strings:
```
var s = "abcde";
var i = "12345";

var n = s + i;    // abcde12345

var n = s.concat(i);  // abcde12345
```

to check character at given index or it's Unicode value:
```
var s = "abcde"

s.charAt(0);  // "a"
s.charCodeAt(0);  // 97
```

searching for substrings within a string:
```
var s = "abracadabra";

s.indexOf("ab");     // 0 or -1 if there is no match

s.lastIndexOf("ab");  // identical, but works from the end
```

splitting string into an array:

```
var s = "one,two,three"

s.split(",");   // ["one", "two", "three"], pass "" to separate all characters into an array

s.split("", 3); // ["o", "n", "e"] - second param sets max size of an array
```


## Date and time

Month is 0-11 not 1-12

```
var d = new Date();   // inializes a new Date object and sets it to current time/date

var d = new Date("31 Dec 2012 23:59:59 GMT");

var d = new Date(2012,11,31, 23,59, 59);

var d = new Date(1000);    // 1000 milliseconds from 01/01/1970
```

Date and time is taken from the computer, not necessarily rite. Additionaly it will be for the given timezone.

```
var = new Date();

d.setFullYear(2012);
d.setMonth(11);				// 0-11
d.setDate(31);

d.setHours(23);
d.setMinutes(59);
d.setSeconds(59);
d.setMilliseconds(0);

// set function take more arguments

d.setFullYear(2012,11,31);  	// year, month, date
d.setMonth(11,31);						// month, date

d.setHours(23, 59, 59, 0);		// hour, minute, seconds, milliseconds
d.setMinutes(59, 59, 0);
d.setSeconds(59, 0);

// UTC date and time - synonymous with GMT, does not take daytime savings

d.setUTCFullYear(2012);
d.setUTCMonth(11);				// 0-11
d.setUTCDate(31);

d.setUTCHours(23);
d.setUTCMinutes(59);
d.setUTCSeconds(59);
d.setUTCMilliseconds(0);

// dates can be offset from UTC

// get computer time

d.getFullYear(2012);
d.getMonth(11);				// 0-11
d.getDate(31);

d.getHours(23);
d.getMinutes(59);
d.getSeconds(59);
d.getMilliseconds(0);


// there are equivalent methods for UTC

d.getUTC...();

d.toString(); 			// outputs standart UTC time

d.toLocaleString();  // uses pc local conventions

// other useful

d.getTimeZoneOffset();		// returns difference UTC - local time in minutes

Date.parse('Jan 1, 2020');	// milliseconds since midnight 01/01/1970 
Date.UTC('Jan 1, 2020');		// milliseconds according to UTC

```

// Example date arithmetic
```
// JavaScript Date Arithmetic
// Calculates Number of days till 2020 and date in 7 days tim
// JS automaticly converts date 31/12/2012 + 7 days = 07/01/2013
var msg = document.getElementById("message");

var dateNow = new Date();
var date2020 = new Date(2020,0,1);

var days2020 = Math.round(( date2020 - dateNow) / 86400000);

console.log(dateNow);
var date7days = new Date( 
													dateNow.getFullYear(), 
													dateNow.getMonth(), 
													dateNow.getDate() + 7
												).toLocaleString().slice(0,-12);	// slice removes last 12 characters;
msg.innerHTML += "<p>Days remaining to 2020: "+ days2020 +"</p>";
msg.innerHTML += "<p>Date in 7 days: "+ date7days +"</p>";
```

## Anonymous self-executing functions  - don't have a name and execute immediately

Self-executing function prevents us from overriding existing function elsewhere in global scope. 
Function has to be wrapped in brackets, otherwise JS would expected it to have a name!
```
(function() {

	// format a number
	function Format(num) {
		return Math.floor(num);
	}

	// output message
	ShowMessage("You are viewing a lesson in section " + Format(9.1));

}());
```

## Closures - function that returns function, still var message is available anywhere

```
function CreateFunction() {

	var message = "I was created by CreateFunction()";
	return function() { alert(message); }

}

var f = CreateFunction();
f();
```

## Modules - module is collection of functions and variables

```
// module.js

var Lib = Lib || {};

// we then reference Lib.Output.function
// all functions returned will work 

Lib.Output = (function() {

	// define output element
	var element = document.getElementById("message");
	var color = "#000";

	// write message
	function Write(msg) {
		element.innerHTML += FormatMessage(msg);
	}

	// set color
	function SetColor(col) {
		color = col;
	}

	// clear all messages
	function Clear() {
		element.innerHTML = "";
	}

	// format a number
	function FormatMessage(msg) {
		return '<p style="color:'+color+'">'+msg+'</p>';
	}

	return {
		Write: Write,
		$: Write,
		SetColor: SetColor,
		Clear: Clear
	};

}());

// now you can use it elsewhere eg:

Lib.Output.Write("This is my message");

// but FormatMessage will not work because it's not returned

```

## Function arguments

Below function is OK, but it has fixed number of arguments

```
// My JavaScript Module

// if Lib exists don't change it, otherwise create new Object
var Lib = Lib || {};

Lib.Output = (function() {

	// write message, msg can be an array of strings
	// element either node or string that we will find
	// start - first element of msg array to be printed
	// end - last element
	// optional color

	function Write(msg, element, start, end, color) {
		
		msg = msg || [];   // if not set set to empty array
		if (msg.constructor != Array) msg = [msg]; // if msg was created using new Array()...
		element = element || "message"; // if element does not exist we assume it should have id #message

		// if passed element is not of DOM node type, find the element
		if (!element.nodeType) element = document.getElementById(element);  

		// if there is no element or msg to be written is empty -> return
		if (!element || msg.length == 0) return;
		
		start = Math.max(0, Math.min(start, msg.length-1));
		end = (end ? Math.max(0, Math.min(end, msg.length-1)) : msg.length-1);
		color = color || "#000";
	
		element.innerHTML += '<p style="color:'+color+'">'+msg.slice(start,end+1).join(" ")+'</p>';
	}

	return {
		Write: Write,
		$: Write
	};

}());
```

This function is much more flexible:

```
// calling function from module Lib

Lib.Output.Write({
	msg: ["Hello", "world", 2, "from", "JavaScript"],
	end: 2,
	color: "#C00"
});


// My JavaScript Module
var Lib = Lib || {};

Lib.Output = (function() {

	// write message
	// write uses single parameter opt so optional set of arguments

	function Write(opt) {
		
		// check if Object has been passed. If not it's probably a string, so we create new 
		// object literal opt which has msg as key, and value opt
		// so function will just operate on string	
		if (opt.constructor != Object) opt = { msg: opt };


		// Extend opt, by adding default values. Extend function is defined at the bottom
		opt = Extend({
			element: "message",
			msg: [],
			start: 0,
			end: null,
			color: "#000"
		}, opt);
		
		// if message is not array, so string most probably, convert it to an array
		if (opt.msg.constructor != Array) opt.msg = [opt.msg];
		opt.element = opt.element || "message";
		if (!opt.element.nodeType) opt.element = document.getElementById(opt.element);
		if (!opt.element || opt.msg.length == 0) return;
		
		opt.start = Math.max(0, Math.min(opt.start, opt.msg.length));
		opt.end = (opt.end ? Math.max(0, Math.min(opt.end, opt.msg.length)) : opt.msg.length);
	
		opt.element.innerHTML += '<p style="color:'+opt.color+'">'+opt.msg.slice(opt.start,opt.end+1).join(" ")+'</p>';
	}
	
	// extend default parameters
	function Extend(obj1, obj2) {
		// compare new default object(obj1) with opt (obj2)
		// we return opt1 with default values unless obj2[prop] exists
		// than we overwrite obj1[prop] with obj2[prop
		]
		for (var prop in obj2) {
			if (obj2.hasOwnProperty(prop)) obj1[prop] = obj2[prop];
		}
		
		return obj1;
	}

	return {
		Write: Write,
		$: Write
	};

}());

```

## Recursion
We have an array, that's element can be either numbers or other arrays. 

```
var n = [
	[1,2,3],
	4,
	[
		[5,6],
		7
	],
	[8,9]
];


Lib.Array.Recurse(n);

// My JavaScript Module
var Lib = Lib || {};

Lib.Array = (function() {

	// define output element
	var element = document.getElementById("message");

	// loop through an array
	function Recurse(a) {
	
	// gets deeper into the structure until a.constructor is String
	// then it uses else option

		if (a.constructor == Array) {
			for (var i = 0; i < a.length; i++) {
				Recurse(a[i]);   
			}
		}
		else element.innerHTML += a + "<br />";
	
	}

	return {
		Recurse: Recurse
	};

}());

```

## Passing functions

Instead of browsing all elements and printing their value only, we could pass to Recurse a function
that would do specific task on every element.

Let's pass the function that sums all the elements

```
var n = [
	[1,2,3],
	4,
	[
		[5,6],
		7
	],
	[8,9]
];


var sum = 0, e = 0;

// function that we pass adds every element's value to sum and counts total number of elements
Lib.Array.Recurse( n, function(x) { e++; sum += x; } );

document.getElementById("message").innerHTML +=
	"<p>Array sum = " + sum + "</p>" +
	"<p>Average = " + (sum/e) + "</p>";


// Changed function

// My JavaScript Module
var Lib = Lib || {};

Lib.Array = (function() {

	// define output element
	var element = document.getElementById("message");

	// loop through an array
	function Recurse(a, action) {
	
		if (a.constructor == Array) {
			for (var i = 0; i < a.length; i++) {
				Recurse(a[i], action);
			}
		}
		else action(a);
	
	}

	return {
		Recurse: Recurse
	};

}());

```

## Browser API

### Window object

Everything lives in window

`alert("hello!")` is identical to `window.alert("hello!")`

Most importan functions of window object

```
// window object

// show message
function ShowMessage(msg) {
	document.getElementById("message").innerHTML += "<p>"+msg+"</p>";
}

ShowMessage("window.name: "+window.name);
ShowMessage("window.innerWidth: "+window.innerWidth);
ShowMessage("window.innerHeight: "+window.innerHeight);
ShowMessage("window.outerWidth: "+window.outerWidth);
ShowMessage("window.outerHeight: "+window.outerHeight);
ShowMessage("window.screenX: "+window.screenX);	// location of window on screen
ShowMessage("window.screenY: "+window.screenY);
	
window.scrollTo(0, 100);
ShowMessage("window.pageXOffset: "+window.pageXOffset);
ShowMessage("window.pageYOffset: "+window.pageYOffset);

var n = window.prompt("What is your name?");
ShowMessage("Hello "+n);

// print dialog
// window.print();

// open a new window, that is used very often for popups!!!
// first argument is window address, if you don't want to go anywhere leave it blank, ie. ""
// second: window name
var win = window.open("", "newwin", "width=300,height=300,menubar=0,toolbar=0,resizable=0,screenX=2000,screenY=200");

win.document.body.innerHTML = "<p>Hello World!</p>";
```

### Location Object

Location is child of a window Object

```
// location object

// show message
function ShowMessage(msg) {
	document.getElementById("message").innerHTML += "<p>"+msg+"</p>";
}

ShowMessage("window.location: "+window.location);

ShowMessage("window.location.protocol: "+window.location.protocol);  // http or https
ShowMessage("window.location.hostname: "+window.location.hostname);  // bbc.co.uk
ShowMessage("window.location.port: "+window.location.port);		// in most cases 80
ShowMessage("window.location.pathname: "+window.location.pathname); // path + file name being run
ShowMessage("window.location.search: "+window.location.search); //
ShowMessage("window.location.hash: "+window.location.hash); // location where we should be jumping

if (window.confirm("Open Google?")) {
	window.location = "http://www.google.com/";
}
```

## The DOM

document is one of the window object core properties

```
// Document Object Model selectors

console.log( "intro ID", document.getElementById("intro") );  // finds #intro

console.log( "p tags", document.getElementsByTagName("p") );  // returns collection of p nodes in an array

// if you need just first one use:
document.getElementsByTagName("p")[0];

console.log( "highlight class", document.getElementsByClassName("highlight") ); // all elements witha a given class as an array

// for querySelector use css syntax. It returns only first node found
console.log( "ul > li", document.querySelector("ul > li") );

// as above but returns collection of all matching nodes
console.log( "ul > li", document.querySelectorAll("ul > li") );

var header = document.getElementsByTagName("header")[0];
var ptags = header.getElementsByTagName("p");
console.log( "header p", ptags );
```

Collections are live:
If you have a collection of p tags and you add one, the collection gets automaticaly updated

```
// Document Object Model navigation

console.clear();
var n = document.getElementsByTagName("ul")[0];
console.log( "ul node", n);

console.log( "nodeName", n.nodeName );
console.log( "nodeType", n.nodeType );  // nodeType == 1 means real element and not whitespace

console.log( "parentNode", n.parentNode );

console.log( "childNodes", n.childNodes );

// .lenght not only grabs <li> elements  but also all whitespaces
// so if your <ul> element has 3 <li> elements, you will get .length = 7 
// instead of expected 3!

// to solve this puzzle check the ElementNodes function at the bottom

console.log( "childNodes.length", n.childNodes.length );

console.log( "li childNodes", n.getElementsByTagName("li") );

console.log( "real childNodes", ElementNodes(n.childNodes) );


// previousSibling and nextSibling are in most cases whitespaces
// this is why you have to write your own function Sibling to extract approperiate nodes
// console.log( "previousSibling", n.previousSibling );
// console.log( "nextSibling", n.nextSibling );

console.log( "real previousSibling", Sibling(n, "previousSibling") );
console.log( "real nextSibling", Sibling(n, "nextSibling") );


// return real DOM nodelist 
function ElementNodes(nodelist) {
	var eNodes = [];

	for (var i=0, j=nodelist.length; i < j; i++) {
		if (nodelist[i].nodeType == 1) {  // meaning node is a real node and not the whitespace
			eNodes.push(nodelist[i]);
		}
	}

	return eNodes;
}


// return real sibling (or null)
function Sibling(node, type) {

	do {
		node = node[type];
	} while (node && node.nodeType != 1);

	return node;

}
```

### Changing styles

```
var e = document.getElementById("myelement")

// use camel case instead of dashes, eg. text-align: 
e.style.textAlign = "center";

//assigning class .animate

e.setAttribute("class", "animate");  // 1 method
e.className = "animate";  // 2 method

```

### Changing content

```
<p id="myelement"> the paragraph </p>

var p = document.getElementById('myelement');

// p has childNodes and the first node is the text inside so to retrieve the text:

p.childNodes[0].nodeValue    // 'the paragraph' or equivalent
p.firstChild.nodeValue       // 'the paragraph'

p.firstChild.nodeValue = "I've just changed!"  // to change 'the paragraph'

// Modern browsers provide 

p.textContent = "Yet another change!";  
p.innerHTML = "Next change!";  // same as above but innerHTML accepts also ... HTML
p.innerHTML = "<div>Next change!</div>";  // exchanges <p> into new <div> tag

p.outerHTML = "";
```

### Adding and cloning elements

```
// Creating new nodes
var article = document.getElementsByTagName("article")[0];

// append an empty p element. appendChild returns the node that's been just added
var p = article.appendChild( document.createElement("p") );

// append text
p.appendChild( document.createTextNode("My "));  // or use just p.textContent = "My "

// append a strong element with text
p.appendChild( document.createElement("strong") ).appendChild( document.createTextNode("third") );

// append text
p.appendChild( document.createTextNode(" paragraph.") );

// modify attributes
p.id = "p3";
p.setAttribute("style", "font-style:italic;");


// It's highly inefficient to add element one by one. The better method is to create the whole structure
// and then append it to the DOM

// create document fragment
var f = document.createDocumentFragment();
var q = f.appendChild( document.createElement("p") );
q.appendChild( document.createTextNode("My "));
q.appendChild( document.createElement("strong") ).appendChild( document.createTextNode("fourth") );
q.appendChild( document.createTextNode(" paragraph.") );
q.id = "p4";

// append fragment as first child
article.insertBefore(q, article.firstChild);

// clone node and children and modify
// passing the true argument means you want to clone all the children nodes as well

var r = q.cloneNode(true);
r.id = "p5";
r.appendChild( document.createTextNode(" Again.") );

// append before third p tag
article.insertBefore(r, article.getElementsByTagName("p")[2]);
```

There is a trick. Can you insert the same element from memory in multiple places? No you can't.
Once you insert the element as first paragraph, and then insert as third paragraph, you actually move the 
element from first to third paragraph.
But you can do it by cloning the element first. 


### Removing DOM elements

```
var p1 = document.getElementById("p1");  // lets chose first paragraph

p1.parentNode.removeChild(p1);

// you could remove all children eg. of an article -> a

while (a.childNodes.length) {
	a.removeChild( a.lastChild );
}
```

Replacing nodes 

```
var p1 = document.getElementById("p1");
var p2 = document.getElementById("p2");

var article = document.getElementsByTagName("article")[0];

article.replaceChild(p2, p1);  // p2 - new node, p1 - the node we want to replace
```

What happens is that we are left only with node p2, that replaced p1. As any node cannot in exist in two places
p2 is the only node left.


## Event handlers






















