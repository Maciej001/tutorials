#jQuery by Craig Buckler

## Basics

`$('p').css({"color": "red", "font-style" : "italic"});`  - change css property
`$("h1").css("color", "blue").text("Hello");`

## Selectors

`p + p`  - find paragraph that has before sibling paragraph, so if you have 3 paragraphs 
only the 2nd and 3rd will be selected. First paragraph does not have any prev paragraphs

`p:first-child` - paragraph that is the first paragraph of it's container

!!!Important - wherever possible use ID selectors and not class selectors. When you use
class selector it searches the whole DOM on the page.

jQuery finds elements from right to left. 
`$('p#main em')` means that jQ will find first ALL em elements, so it slows down your website.

`$('p#main').find('em');` - better

`$("em", $("p#main"));`  - it's starts finding #main id and then only all em-s within

###Traversing Filtering

`$('p').first();`		- selects all paragraphes, discards all except of first element
`$('p').last();`		- selects all paragraphes, discards all except of last element

`$('p').eq(1);`			- selects all and grabs only the second one from an array [0, n]
`$('p').eq(-1);`		- returns last item
`$('p').slice(2,4)`	- elements from index 2 to 4
`$('p').slice(1)`		- all elements from 2nd to the end of array

.filter

```
$("p").filter(".myclass"); 	// only element with class "myclass"
$("p").filter(":even"); 		// even numbered items
$("p").filter( $("p.myclass") );	// elements which appear in both sets
$("p").filter(function(i) { return (i % 3 == 0) });		// every third item

$("p").not(".myclass"); // elements without class "myclass"
$("p").not(":even"); // odd numbered items

```	

#### Sibling traversal

```
$("#p2").prev(); // previous sibling (#p1)
$("#p2").next(); // next sibling (#p3)

$("#p1").prevAll(); // all previous siblings (none)
$("#p1").nextAll(); // all next siblings (#p2, #p3)

$("#p2").prevUntil("div"); // all previous siblings until div
$("#p2").nextUntil("div"); // all next siblings until div

$("#p2").siblings(); // all siblings (#p1, #p2)
```

#### Parent traversal

```
$("#i1").parent(); // immediate parent (ol)
$("#i1").parent("div"); // immediate div parent (none)

// closest positioned parent (CSS relative, absolute, fixed)
$("#i1").offsetParent();


<html>
	<div>
		<ol>
			<li id="i1">item 1</li>
			<li id="i2">item 2</li>
			<li id="i3">item 3</li>
		</ol>
	</div>
</html>

$("#i1").parents(); // all parent elements to <html>
$("#i1").parents("div"); // all div parent elements to <html>
$("#i1").parentsUntil("article"); // all parents up to but not including <article>

// all div parents up to but not including <article>
$("#i1").parentsUntil("article", "div");

$("#i1").closest("div"); // closest div parent
```

#### Child traversal

```
$("div").children(); // immediate child elements (ol)
$("div").children("p"); // immediate child p elements (none)
$("div").find(); // all descendant elements
$("div").find("li"); // all descendant li elements
```

#### Other 

```
$('div').add('ol');  // all divs and ol, same as $('div, ol');
$('#i1').siblings().andSelf()  // contains all siblings 'li' and the li #i1 itself
```

##Animation
```
var a = $('h2');

a.hide();	// hides element
a.hide(1000); // hide over 1000ms - changes opacity and dimensions
a.hide('slow'); // use the jQuery default

// or define your own speed
$.fx.speeds['very-slow'] = 3000;
a.hide('very-slow');

a.show(1000); // shows an element

a.toggle(1000); // toggles visibility of an element

a.fadeOut(1000); // fades out opacity of an element
a.fadeIn(1000);  // fades in an element
a.fadeTo(1000, 0.7)  // changes opacity to 0.7 over 1000 miliseconds

a.slideUp(1000);   // reduces the height of an element
a.slideDown(1000); // opposite
a.slideToggle(1000); // toggles visibility sliding up or down

// animate - you can only animate properties with numeric values
a.animate({
	"font-size": "16px",  // final css properties
	"width": "250px",
	"left": "50px",
	"top": "50px"
}, 1000);

to change eg. width by 60px:

"width": "-=60px"

// instead of passing just duration to animation we can pass an object

a.animate({
	"left": "0px"
},
{
	duration: 3000,
	easing: "swing"    // standard easing; other: linear
});


// define your own easing function

$.easing["myfunc"] = function(i){
	return i*i;
}
```

### Animation queue

```
// delay waits certain time before the animation is run
a.fadeOut(1000).delay(2000).fadeIn(1000);  // insert a 2sec pause between effects

// stop method stops the animation and clears the queue
// it will stop animation immediately after it starts, so if you want to stop it after 800milliseconds only 
a.stop()

// instead write and pass it .stop as the function and indicate that after 800 milliseconds
setTimeout(function(){ a.stop(); }, 800);

```


## Page manipulation

```
$('img').attr('width');  // attr returns just one value
$('img').attr('width', '330');  // set attr value

$('a').attr('href', 'http://google.com');


// class names

// add "bright" class to header
$("header").addClass("bright");

// has "bright" class been applied?
console.log( "bright class is applied: ",$("header").hasClass("bright") );

// remove "bright" class from header
$("header").removeClass("bright");

// has "bright" class been applied?
console.log( "bright class is applied: ",$("header").hasClass("bright") );

// add/remove "bright" class as necessary
$("header").toggleClass("bright");

```

##Forms
```
<form id="myform" action="#" method="get">
	<fieldset>
		<legend>My Form</legend>
	
		<label for="name">Name</label>
		<input type="text" id="name" name="name" value="Craig Buckler" />

		<label for="comments">Comments</label>
		<textarea id="comments" name="comments" rows="2" cols="18">Are you enjoying this video course?</textarea>

		<label for="skills">Primary skills</label>
		<select id="skills" name="skills">
			<option value="none">please select&hellip;</option>
			<option value="html">HTML</option>
			<option value="css">CSS</option>
			<option value="js">JavaScript</option>
		</select>
		
		<label><input type="checkbox" id="like" name="like" checked="checked" /> I like jQuery</label>
		
		<p>Age group:</p>
		<label><input type="radio" id="age0" name="age" value="-30" /> under 30</label>
		<label><input type="radio" id="age1" name="age" value="30-50" checked="checked" /> 30 to 50</label>
		<label><input type="radio" id="age2" name="age" value="50-" /> over 50</label>
	
	</fieldset>
</form>


$("#name").val()  // value of the field #name
$("#name").val("My name");  setting the value

// inspect individual select box optis
$("#skills option[value=js]").prop("selected");
$("#skills option").eq(3).prop("selected");

// change the prop
$("#skills option[value=js]").prop("selected", true);

// change skills select box
$("#skills").val("js");

// is checkbox checked
$("#like").prop("checked");

// uncheck checkbox
$("#like").prop("checked", false)

// inspect individual radio buttons
console.log( $("#age0").prop("checked") );
console.log( $("#age1").prop("checked") );
console.log( $("#age2").prop("checked") );

// find value for checked radio button
$("input[name=age]:checked").val();

// check a radio button
$("#age0").prop("checked", true);

```


##Text

```
var p = $('#p1');


// shows the text of a paragraph
p.text()

p.text("Hello world"); // sets the text of a paragraph

.text allows also to pass functions!
// pass a function that adds numbers to every li element 
$("li").text(
	function(i, text) {
		return (i+1)+". "+text;
	}
);

p.html();  //returns everything within the  paragraph in html form
p.html("<em>Hello</em>")  // to insert the html

```

## HTML5 data

```
<article>

	<div
		id="element" 
		data-name="myelement" 
		data-type="standard" 
		data-counter="0"
	>Element used for data storage.</div>

</article>

// JS

var e = $("#element");

// display initial values
e.data("name");
e.data("type");
e.data("counter");
e.data("test"); // undefined

// update a value
e.data("counter", 1);
e.data("counter"); // 1

// set a new value
e.data("test", 2);
e.data("test"); // 2

// reset values to original
e.removeData("counter");
e.removeData("test");
e.data("counter"); // 0
e.data("test"); // undefined
```

### get/set position

```
	<article style="position:relative;border:1px solid #000;">
	
		<div id="moveme">Element to Move</div>
	
	</article>

var e = $("#moveme");

// location on page(browser window). Returns an object that has two properties: top and left
e.offset()

// location in relation to offset parent
e.position()

// change location
e.offset( {top:50, left:100} );

// change element dimensions
e.width(500);
e.height(150);

// element width/height
e.width()
e.height()

// element width/height plus padding
e.innerWidth()
e.innerHeight()

// element width/height plus padding and borders
// (pass true to include margins)
e.outerWidth()
e.outerHeight()

// document dimensions, even if part is hidden
$(document).width()
$(document).height()

// browser window dimensions - actual viewport dimensions
$(window).width()
$(window).height()

</script>
```

## Manipulating HTML

```
	<article>
	
		<p>In this chapter we will discover how to get and set:</p>
		<ul>
			<li>attributes</li>
			<li>CSS properties</li>
			<li>form values</li>
			<li>element text</li>
			<li>HTML5 element data</li>
			<li>element positions</li>
		</ul>
		
		<p>as well as:</p>
		<ul>
			<li>wrapping HTML elements</li>
			<li>copying HTML elements</li>
			<li>deleting HTML elements</li>
		</ul>
	</article>

	<footer>
		<p><a href="http://www.infiniteskills.com/">&copy; InfiniteSkills</a></p>
		<p><a href="http://craigbuckler.com/">By Craig Buckler</a></p>
	</footer>

<script src="../resources/script/jquery.js"></script>
<script>

// add new paragraph as last child node
$("article").append("<p>A new paragraph!</p>");

// add new paragraph as first child node
$("article").prepend("<p>A new paragraph!</p>");

// add new item after second list item
var a = $("article ul:first li").eq(1);
a.after("<li>CSS positions</li>");

// add new item before second list item
a.before("<li>CSS positions</li>");

// replace second list item
a.replaceWith("<li>CSS positions</li>");

</script>
```



























