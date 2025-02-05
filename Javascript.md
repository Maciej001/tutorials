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

Event handler is a function. One event object is passed to this function. You need to analyse the object and
perform the relevant actions.

Event handle may execute other function:
* prevent default action, eg. clicking link, prevents redirecting to the new page
* prevent event to "bubble up"
* deregister event, so it will never run again

You can assign as many event to the single element as you wish

#### Event delegation

If parent has 100 child elements it doesn't make much sense to attache click event handler to every single 
one of them. So it's better if the child gets clicked the event 'bubbles up' and reaches parent, so the event
handler can be run and event object tells which of child elements got clicked.

```
// find first link on the page
var link = document.getElementsByTagName("a")[0];

// delegate event handler
link.addEventListener( "click", MyEventHandler );

// event handler
function MyEventHandler(e) {

	alert("ouch!");
	e.preventDefault();    // e.currentTarget <- object that was had event applied, eg. clicked
												 // e.target -> element, the current event is applied to 
}
```


Multiplication table
```
// find table
var table = document.getElementById("multiplication");
var tcols = table.getElementsByTagName("col");

// delegate event handler
table.addEventListener( "mouseover", TableHandler );
table.addEventListener( "mouseout", TableHandler );

// event handler
function TableHandler(e) {

	var t = e.target;
	if (t.nodeName != "TD") return;    // we are interested only in cells, multiplication results
	
	var cName = ( e.type == "mouseover" ? "active" : "");  // assign class
	t.parentNode.className = cName;		// parent node is the whole row
	tcols[ t.cellIndex ].className = cName;   // cellIndex returns column number

	
	// the same as 3 lines above, just a bit shorter oneliner
	// t.parentNode.className = tcols[ t.cellIndex ].className =
	// ( e.type == "mouseover" ? "active" : "");
	
}
```

## Forms

### Form events

Can be used for validation of the forms data before submission

IE9 and below does not offer any HTML5 form support at all

``` 
// form submission event
// HTML5 browsers will not trigger this event if the form is invalid
form.addEventListener('submit', validationFunction);    

// form change event is applied to each individual form field
form.addEventListener('change', validationFunction);    

// key presses - you can prevent user from entering certain characters
form.addEventListener('keypress', validationFunction);    
```

### Client side form validation

```
HTML ************************************


		// to remove HTML5 standard form validation use instead of 'required', 'novalidate'

		<fieldset>
			<legend>Register</legend>
		
			<!-- email -->
			<label for="email">email:</label>
			<input type="email" id="email" name="email" autofocus required />

			<!-- passwords -->
			<label for="pass1">password:</label>
			<input type="password" id="pass1" name="pass1" required />
			
			<label for="pass2">again:</label>
			<input type="password" id="pass2" name="pass2" required />

			<button type="submit">Register</button>
		
		</fieldset>


Javascript ************************************

// form validation

// DOM nodes
var form = {
	register:	document.getElementById("register"),
	message:  document.getElementById("error_message"),
	email:		document.getElementById("email"),
	pass1:		document.getElementById("pass1"),
	pass2:		document.getElementById("pass2"),
	strength:	document.getElementById("strength")
};


// form submit
form.register.addEventListener( "submit", CheckForm );


// check email field
form.email.addEventListener( "change", function(e) {
	if (e.target.value == "") alert("You forgot the email!");
} );


// stop space character
form.pass1.addEventListener( "keypress", NoSpaces );
form.pass2.addEventListener( "keypress", NoSpaces );
form.email.addEventListener( "keypress", NoSpaces );

// password strength

form.pass1.addEventListener( "keyup", PasswordStrength );

var strtext = ["weak", "average", "strong"];
var strcolor = ["#c00", "#f80", "#080"];

function PasswordStrength(e) {
	var pass = form.pass1.value;

	// count uppercase
	var uc = pass.match(/[A-Z]/g);  // check if contains uppercase - returns array of matching characters
	uc = (uc && uc.length || 0); // if exists and has length returns 1 else 0

	// count numbers
	var nm = pass.match(/\d/g);
	nm = (nm && nm.length || 0);

	// count symbols
	var sb = pass.match(/\W/g);
	sb = (sb && sb.length || 0);

	// password strength
	var s = pass.length + uc + 2*nm + 3*sb;

	// if password is 50 long than floor will give us 5, but we need to know if its strong = 2, or not
	// below we always will get 0,1 or 2
	s = Math.min(Math.floor(s/10), 2);
	console.log(form.pass1.value);

	form.strength.textContent = strtext[s];
	form.strength.style.color = strcolor[s];
}


// stop spaces being entered
function NoSpaces(e) {
	if (e.charCode == 32) e.preventDefault();
}


// form submit validation
var reEmail = /^[a-z0-9._%-]+@[a-z0-9.-]+\.[a-z]{2,4}$/;
function CheckForm(e) {

	var msg = "";

	// check email
	if (!reEmail.test(form.email.value)) {  // validates if email.value fullfils requirements of reEmail regex
		msg += "<p>your email address</p>";
	}

	// check passwords
	if (form.pass1.value == "" || form.pass1.value != form.pass2.value) {
		msg += "<p>your passwords</p>";
	}

	// complete message
	if (msg != "") {
		msg = "<p>Please check:</p>"+msg;
	}
	else {
		msg = "Form is valid!\nSubmitting...";
	}

	e.preventDefault();
	form.message.innerHTML = msg;

}
```

## Animation

### Timer and animation

```
// bouncing ball using setTimeout
var
	body = document.getElementsByTagName("body")[0],
	ball = document.getElementById("ball");
var
	bx = ball.offsetLeft, by = ball.offsetTop, 
	bw = ball.offsetWidth, bh = ball.offsetHeight,
	dx = 5, dy = 5, active = true;


// move ball	
function AnimateBall() {

	bx += dx;
	by += dy;
	ball.style.left = bx + "px";
	ball.style.top = by + "px";
	
	if (bx + dx < 0 || bx + bw + dx > body.offsetWidth) dx = -dx;
	if (by + dy < 0 || by + bh + dy > body.offsetHeight) dy = -dy;
	
	if (active) setTimeout(AnimateBall, 10);
	
}

// start animation after 1 second
var st = setTimeout(AnimateBall, 1000);

// stop ball on click, passing the st variable, that was returned by setTimeout
ball.addEventListener( "click", function() { clearTimeout(st); active = false; } );
```

Instead of calling the function every 10ms use setInterval, so it gets called every 10ms

```
// bouncing ball using setInterval
var
	body = document.getElementsByTagName("body")[0],
	ball = document.getElementById("ball");
var
	bx = ball.offsetLeft, by = ball.offsetTop, 
	bw = ball.offsetWidth, bh = ball.offsetHeight,
	dx = 5, dy = 5, active = true;


// move ball	
function AnimateBall() {

	bx += dx;
	by += dy;
	ball.style.left = bx + "px";
	ball.style.top = by + "px";
	
	if (bx + dx < 0 || bx + bw + dx > body.offsetWidth) dx = -dx;
	if (by + dy < 0 || by + bh + dy > body.offsetHeight) dy = -dy;
	
}

// start animation
var st = setInterval(AnimateBall, 10);

// stop ball on click
ball.addEventListener( "click", function() { clearInterval(st); } );
```

## Ajax

Asynchronous JavaScript and XML

XML - Extensible Markup Language, losing popularity

most common technique is XMLHttpRequest introduced in IE5. For security reasons it only alows you to contact
server that is on the same domain.

another funcion is XMLHttpRequest2 that allows you to check the progress bar.


### Form with ajax html response

Below form sends the request to the server and once the server responds with simple html it just 
displays the simple html on the page.

HTML
```
<form id="speedform" action="http://localhost/js/speedconvert.php" method="get">
	<fieldset>
	<legend>Speed conversion</legend>
	
	<label for="speed">Speed:</label>
	<input type="text" id="speed" name="speed" value="0" />
	
	<select type="text" id="unit" name="unit">
		<option value="mph">miles per hour</option>
		<option value="kph">kilometers per hour</option>
		<option value="fps">feet per second</option>
		<option value="mps">meters per second</option>
	</select>
	
	<input type="hidden" name="format" value="html" />
	
	<button type="submit">Convert</button>
	
	</fieldset>
</form>

<div id="output">

	<table>
		<tr><th>mph</th><td>0.00</td></tr>
		<tr><th>kph</th><td>0.00</td></tr>
		<tr><th>fps</th><td>0.00</td></tr>
		<tr><th>mps</th><td>0.00</td></tr>
	</table>

</div>
```

Javascript
```
// XMLHttpRequest
var Lib = Lib || {};

Lib.Ajax = (function() {

	// hijack form
	// Hijack digests the data from form, creates the args array and calls Call function that
	// actually executes ajax request

	function Hijack(form, callback) {
	
		var args = {};
		
		for (var i = 0; i < form.elements.length; i++) {
			var f = form.elements[i];
			if (f.name) args[f.name] = f.value;
		}

		// make Ajax call
		Call(form.action, args, form.method, callback);
	
	}

	// call web service - executes ajax request by building the list of all necessary parameters
	function Call(url, args, type, callback) {

		// check type (GET or POST) and  if empty use GET
		type = (type || "GET").toUpperCase();
	
		// create argument list
		args = args || {};   // empty object if no args delivered
		var arglist = "";
		for (var n in args) {   // equivalent of each, loops thru all arguments in args array
			arglist += "&" + n + "=" + escape(args[n]);
		}

		// why do we take the first argument only?
		// arglist is a string "...&1=argrument&2="

		if (arglist.length > 0) arglist = arglist.substr(1);  // substr removes first &
		
		// append args to GET URL
		if (type == "GET") {
			url += "?" + arglist;
			arglist = null;
		}
		
		// XMLHttpRequest object
		var xhr = new XMLHttpRequest();
		xhr.open(type, url, true);
		
		// callback function
		if (callback) {
			xhr.onreadystatechange = function() {
				if (xhr.readyState == 4 && xhr.status == 200) {    // 200 server answers OK!
					callback(xhr.responseText);
				}
			};
		}
		
		// open request and sets headers
		xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded; charset=UTF-8");
		xhr.setRequestHeader("X-Requested-With", "XMLHttpRequest");

		// finally sends request. server responds with just html
		xhr.send(arglist);

	}

	return {
		Hijack: Hijack,
		Call: Call
	};

}());

// start
var
	speedform = document.getElementById("speedform"),
	output = document.getElementById("output");

// form submit - direct to Ajax call
speedform.addEventListener("submit", function(e) {
	e.preventDefault();
	Lib.Ajax.Hijack(speedform, function(r) {
		
		output.innerHTML = r;
		
	});
});

```

or if you would like to parse the returned data as jason 

```
// start
var
	speedform = document.getElementById("speedform"),
	output = document.getElementById("output"),
	td = output.getElementsByTagName("td");

// form submit - direct to Ajax call
speedform.addEventListener("submit", function(e) {
	e.preventDefault();
	Lib.Ajax.Hijack(speedform, function(r) {   // function is run when the data is returned
		
		r = JSON.parse(r);
		td[0].textContent = r.mph;
		td[1].textContent = r.kph;
		td[2].textContent = r.fps;
		td[3].textContent = r.mps;
		
	});
});
```

## HTML5 API

IE8 and below do not support HTML5

Apple chose h.264 as standard video codec

### Creating customer controlled buttons for VIDEO play and pause

```
	<article>

		<video id="bunny" poster="videos/bunny.jpg">  // controls="controls" adds standard HTML5 controls
			<source src="videos/bunny.mp4" type="video/mp4" />
			<source src="videos/bunny.webm" type="video/webm" />
		</video>

		<div id="controls">
			<a id="play" href="#">Play</a>
			<span id="timer">0%</span>
		</div>

	</article>

<script>
var
	video = document.getElementById("bunny"),
	play = document.getElementById("play"),
	timer = document.getElementById("timer"),
	update;

video.addEventListener("click", PlayVideo, false); // will play video when the video itself is clicked
play.addEventListener("click", PlayVideo, false);  // will play video when play button is clicked

// play or pause video
function PlayVideo(e) {

	e.preventDefault();

	if (video.paused) {

		video.play();
		play.textContent = "Pause";

		update = setInterval( function() {
			timer.textContent = Math.round(video.currentTime / video.duration * 100) + "%";
		}, 500);

	}
	else {

		video.pause();
		play.textContent = "Play";

		if (update) clearInterval(update);

	}

}
</script>
```


### Canvas

```
<article>

		<canvas id="mycanvas" width="300" height="300"></canvas>

	</article>

<script>
var canvas = document.getElementById("mycanvas");

if (canvas.getContext) {

	var cxt = canvas.getContext("2d");

	// define default styles
	cxt.lineWidth = 6;
	cxt.strokeStyle = "#333";
	cxt.fillStyle = "#c00";

	// lines
	// below methods set the path but only .stroke() draws it
	cxt.beginPath();
	cxt.moveTo(0,0);
	cxt.lineTo(150,150);
	cxt.lineTo(100,200);
	cxt.bezierCurveTo(300,150,0,0,200,300);
	cxt.stroke();  

	// clear top-left square
	cxt.clearRect(0,0,50,50);

	// circle
	cxt.beginPath();
	cxt.arc(200,80,50,0,Math.PI*2);
	cxt.fill();
	cxt.stroke();

}

</script>
```

#### Canvas rain

```
	<article>

		<canvas id="mycanvas" width="1000" height="800"></canvas>

	</article>

<script>
var canvas = document.getElementById("mycanvas");
if (canvas.getContext) {

	// start animation
	var cxt = canvas.getContext("2d");
	cxt.fillStyle = "rgba(255,255,255,0.5)";
	
	setInterval(function() {
		var	x = Math.round(Math.random()*canvas.width), 
			y = Math.round(Math.random()*canvas.height),
			e = 20 + Math.round(Math.random()*100),           // e = <0,50>
			s = 0;
		
		(function() {
			s++;
			if (s <= e) {
				setTimeout(arguments.callee,s);
				var c = 255-(e-s)*3;
				cxt.strokeStyle = "rgb("+c+","+c+","+c+")";
				cxt.beginPath();
				cxt.arc(x,y,s,0,Math.PI*2,true);
				cxt.fill();
				cxt.stroke();
			}
		})();
	},100);

}
</script>
```

### SVG - Scalable Vector Graphics

SVG are great for charts, diagrams and logos

You can create them in any external program like inkScape

Every SVG is XML document, so it exposes the DOM which you can manipulate by changing attributes
of DOM elements.

```
<article>

		<object id="mysvg" type="image/svg+xml" data="images/image.svg"></object>

	</article>

<script>
var mysvg = document.getElementById("mysvg");
var svg = mysvg.contentDocument;

var line = svg.getElementById("line");

// animate line
var y = 10;
(function() {
	y += 2;
	line.setAttributeNS(null,"y1",y);
	line.setAttributeNS(null,"y2",300-y);
	if (y < 290) setTimeout(arguments.callee, 20);
}());

// create rectangle
var rect = svg.createElementNS("http://www.w3.org/2000/svg", "rect");

rect.setAttributeNS(null,"x",100);
rect.setAttributeNS(null,"y",125);
rect.setAttributeNS(null,"width",100);
rect.setAttributeNS(null,"height",50);
rect.setAttributeNS(null,"fill","#393");

svg.getElementById("main").appendChild(rect);

</script>
```


### Geolocation

```
	<article>

		<div id="geo"></div>

	</article>

<script src="http://maps.google.com/maps/api/js?sensor=false"></script>
<script>
var geo = document.getElementById("geo");

// do geolocation
if (navigator.geolocation) {
	// pass success function and fail function when browser does not support geolocation or user declined the request
	navigator.geolocation.getCurrentPosition(geoSuccess, geoFailed);
}
else {
	geo.textContent = "Sorry - your browser does not support geolocation.";
}

// geolocation successful
function geoSuccess(position) {
	/*
		latitude = position.coords.latitude
		longitude = position.coords.longitude
		accuracy (meter radius) = position.coords.accuracy
	*/
	
	var latlng = new google.maps.LatLng(position.coords.latitude, position.coords.longitude);
	var mapOpts = {
		zoom: 13,
		center: new google.maps.LatLng(position.coords.latitude, position.coords.longitude),
		mapTypeControl: false,
		navigationControlOptions: { style: google.maps.NavigationControlStyle.SMALL },
		mapTypeId: google.maps.MapTypeId.ROADMAP
	};
	var map = new google.maps.Map(geo, mapOpts);

}

// geolocation failed
function geoFailed() {
	geo.textContent = "Sorry - geolocation failed.";
}
</script>
```


### Files upload

```

	<article>
	
		<form id="upload" action="#" method="get">

			<fieldset>

				<div>
					<label for="fileselect">Files to upload:</label>
					<input type="file" id="fileselect" name="fileselect[]" multiple="multiple" />
				</div>
				
				<div id="filedrop">or drop files here</div>

			</fieldset>

		</form>
	
		<h2>File information:</h2>
		<div id="output"></div>

	</article>

<script>
// output information
function Output(msg) {
	var m = document.getElementById("output");
	m.innerHTML = msg + m.innerHTML;
}


// drop box hover effect
function FileHover(e) {
	e.preventDefault();
	e.target.className = (e.type == "dragover" ? "hover" : "");
}


// file selection
function FileSelect(e) {
	FileHover(e);
	
	// file select box returns targe.files property and dropbox .dataTransfer.files list
	var files = e.target.files || e.dataTransfer.files;

	// process all files and pass each file reference to ParseFile
	for (var i = 0, f; f = files[i]; i++) {
		ParseFile(f);
	}

}


// output file information
function ParseFile(file) {

	// file information
	Output(
		"<p>File information: <strong>" + file.name +
		"</strong> type: <strong>" + file.type +
		"</strong> size: <strong>" + file.size +
		"</strong> bytes</p>"
	);

	// display an image
	// check if file is an image
	if (file.type.indexOf("image") == 0) {
		var reader = new FileReader();   // and instantiate FileReader object
		reader.onload = function(e) {    // when the file is loaded to the memory
			Output(
				"<p><strong>" + file.name + ":</strong><br />" + 
				'<img src="' + e.target.result +
				'" /></p>'
			);
		}
		reader.readAsDataURL(file);
	}

	// display text - identical to the above code. The only difference is that we read the file as text
	if (file.type.indexOf("text") == 0) {
		var reader = new FileReader();
		reader.onload = function(e) {
			Output(
				"<p>" + file.name +
				": <p><pre>" + e.target.result +
				"</pre>"
			);
		}
		reader.readAsText(file);
	}

}


// initialization
// let's check if the below objects are available. If not there is no point to continue
if (window.File && window.FileList && window.FileReader) {
	
	// select box used
	var fileselect = document.getElementById("fileselect");
	fileselect.addEventListener("change", FileSelect, false);
	
	// drop box used
	var filedrop = document.getElementById("filedrop");
	filedrop.addEventListener("dragover", FileHover, false);
	filedrop.addEventListener("drop", FileSelect, false);
	
}
</script>
```

### Webworkers 

Webworkers are JS equivalents of threading
They don't work in IE9 and below. Additionally they cannot axess the DOM

You can communicate with webworker by sending only single parameter. It can be an object or an array.


## Persistence and Storage

### Cookies

Web is stateless. Every request is independent. Cookies allow as to save state.
Cookies are domain specific. So one domain cannot access cookies of the other domain

Session cookies are deleted after the session is closed. If you don't save time for cookies to expire they 
automatically become session cockies.

You cannot delete cookies in JS, but you can set expiry time.
Each domain can have upto 20 cookies 4k max each.

Better use jQuery
























