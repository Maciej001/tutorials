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



















