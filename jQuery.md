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

### Wrapping elements

```
// wrap div around every paragraph
$("p").wrap("<div>");

// put all paragraph child nodes into an em
$("p").wrapInner("<em>");

// put all paragraphs into a single section
// it scans the whole website for paragraphs and puts all of them in one section, then it places
// the section where the first paragraph was
$("p").wrapAll("<section>");
```

### Cloning elements

Can be useful for cloning HTML table rows when dynamically created

```
// clone elements
var p = $("footer p").clone();

// and place elsewhere
$("header").append( p );
```

### Removing elements 
```
// remove elements and all children
$("footer").remove();

// remove child nodes but retain selected elements
$("article").empty();

// remove parent (container) node. Wrapper is remove but content remains
$("h1").unwrap();
```


## Events

Event handler is a function that runs as soon as the event occurs
Event handler is passed just one event object.

### When DOM loads

`$(Setup);` - once the DOM is ready run the function Setup or 
```
$(function(){
	do something
});
```
`$('#my_image').load(function() { do something });` // execute the function after image has been loaded

### Bind events

```
// change class when mouse moved over/out
// bind allows to specify more then one event 
$("#e1").bind("mouseenter mouseleave", function(e) { 
	$(this).toggleClass("over");
});

$("#e1").mouseenter(function(){})  // do something on mouseenter

```

`mouseenter` and `mouseleave` don't fire the event when the mouse hovers over child element

```
// disable a link click
$("a#google").click(function(e) {
	this.href = "http://bing.com";  // why this not $(this)
});

// check a form on submit
$("#myform").submit(function(e) {
	var n = $("#yourname").val();
	if (n == "") {
		alert("Please enter your name...");
	}
	else {
		alert("Hello "+n+"!");
	}
	return false;
	});
```
#### Difference between $(this) and this

`$(this)[0] === this`  // jQuery returns set of elements
`$()` is jQuery constructor function. 
`this` is a reference to the DOM element of invocation.
So passing `this` to `$()` as parameter so that you could call jQuery methods and functions

### Event object

```
e.target 	 // element that triggered the event even if it had to bubble higher to get serviced
e.currentTarget  // element that the event is attached originally 

e.preventDefault()  // prevents default behaviour, eg. redirection by a element
e.stopPropagation() // stops the event from bubbling higher in DOM

return false  is equivalent to preventDefault + stopPropagation at the same time
```


### Delegation live events

When you attach event handlers to elements in DOM structure they exists only on elements that
where in DOM when the website opened. So how to add event handlers to elements that hass been attached 
dynamically.

```
$('ul#list li').click(function(e){
	var ul = $(this).parent();
	ul.append("<li>New item " + ul.children().length+1 + "</li>");
});

// using live method
// live method is a bit inefficient because it attaches itself to the root document!
$('ul#list li').live("click", function(e){
		var ul = $(this).parent();
		ul.append("<li>New item " + ul.children().length+1 + "</li>");
	});

// often better option is to use delegate method
// bind it to parent element and pass the context 'li' in the function
$('ul#list').delegate("li","click", function(e){
		var ul = $(this).parent();
		ul.append("<li>New item " + ul.children().length+1 + "</li>");
	});
```

### Triggering events

```
$('#list').trigger('click');
```

### Deregistering Events
```
// run when DOM is ready
$(function() {

	// prevent link click
	$("a#google").click(GoogleClick);
	
	function GoogleClick(e) {
		alert("Try again...");
		
		// deregister event
		$(this).unbind("click", GoogleClick);

		return false;
	}


	// attach event to all existing and new list items in ul#list
	$("ul#list").delegate("li", "click", ListItemClick);
	
	function ListItemClick(e) {
		var ul = $(e.target).parent();
		var c = ul.children().length+1;
		ul.append("<li>new item "+c+"</li>");
		if (c > 4) {
		
			// deregister event
			$(ul).undelegate("li", "click", ListItemClick);
			
		}
	}
	
});


// to unbind all events:
$('*').unbind();

```

## jQuery Array methods
```
var a = [1,2,3];

$.isArray(a);		// check if is array?

$.inArray(1,a); // check if 1 is in a; if successful returns index, if not returns -1

// create an array from collection of node elements
var p = document.getElementByTagName('p');
var myArray = $.makeArray(p);

$.merge(a, b);		// merges second array into the first, duplicates are maintained
$.extend(a, b);		// merges second object or array into the first, but duplicates are overwritten!

$("p").each( function(index, element) {
	console.log( "paragraph ", index, "element: ", element);
});

$.each( [1,2,3], function(index, element) {
	console.log( "item at index ", index, " is ", element );
});

var a = ['a', 'b', 'c'];
var b = $.map(a, function(index, element){
	return element+index;
});
```


## AJAX

```
$('element').ajax();  // rarely to be used
$('element').load(url); // url is the url + query; as response you will get eg. html

// Ajax call
	$.getJSON(ws, args, Process);   // webservice url, list of arguments and callback function


// parse Ajax response
function Process(data) {

	var html = "";
	$.each(data, function(index, value) {
		html += "<p><strong>"+index+"</strong>: "+value+"</p>";
	});
	
	$("#output").empty().append(html);
	
	console.log( "kph: ", data.kph );

}

```

### Ajax errors
 
When doing ajax request you should show gif spinner, so the user knows, he waits for something.
In most cases it will be very quick delivery, so the user even does not notice the delay, 
but somtimes, server will not respond or it will time out.

```
$(document).ajaxError(Failure);

// ajax failure
function Failure() {

	$("#output").empty().append("<p>An Ajax error occurred.</p>");
}
```

If you want to controll error more precisely you have to use .ajax funtion

```
// Ajax call (setting error handler)
$.ajax(ws, {
	data: args,
	dataType: format,
	success: Process,
	error: Failure				// error handler function
});

```

## Plugin

```
/*
 * jQuery text reversing plugin
 * usage: $(selector).reverseText();
 * optional arguments:
 *		min: ignore shorter text strings
 *      max: ignore larger text strings
 * e.g. $(selector).reverseText({ min:5, max:10});
 * You can also apply class="reverse" to any HTML element.
 */
 
(function($) {

	// define new plugin function
	// expecting single parameter params we expect javascript object (key, value)
	$.fn.reverseText = function(params) {
	
		// override default parameters
		// and overwrite our defaults with users' choices
		params = $.extend( { min: 0, max: 99999 }, params);
		
		// iterate all elements; each is the jQuery object that was passed, eg. all paragraphs
		this.each(function() {
		
			var e = $(this);  // this is every single elemnt that we loop through
			var txt = e.text();
			
			if (txt.length >= params.min && txt.length <= params.max) {
			
				// reverse the text
				e.text( txt.split("").reverse().join("") );
			
			}
		
		});
		
		// return jQuery object
		return this;
	
	};

	// auto-run
	// you don't have to call the function on collection on elements
	// just add .reverse class and the plugin will check it automaticaly and call the 
	// reverseText function on each elements that contain .reverse class!!!
	
	$(".reverse").reverseText();
	
})(jQuery);
```


# jQuery from novice to ninja

## Building elements

```
// add image after link was clicked
$('<img>')
	.attr('src', $(this).attr('href'))
	// load fires when image is fully loaded
	.load(function(){
		positionLightboxImage();
	})
	// remove image
	.click(function{
		removeLightbox();
	})
	.appendTo('#lightbox');

// alternative way
$('<img>', {
	src: $(this).attr('href'),
	load: function() {
		positionLightboxImage();
	}
	click: function(){
		removeLightbox();
	}
}).appendTo('#lightbox');

return false; // to prevent the default behavior

```

### Fade one image into the other

```
<span id="fader">
  <img id="glenda" src="../../images/glenda_200.jpg" alt="Glendatronix"/>
  <img class="to" src="../../images/fader_200.jpg" />
</span>

$(function(){
	$('#fader').hover(function(){
		// stop - stops the animation
		// stop uses 2 params: clearQueue and goToEnd. 
		// clearQueue == true clears all the queued animatinos on the element
		// goToEnd == true moves immediately the animation state to the end.
		$( this ).find( 'img:eq(1)' ).stop( true, true ).fadeIn( 250 );
	},
	function(){
		$( this ).find( 'img:eq(1)' ).fadeOut( 250 );
	});
});
```


### Fade in collection of images

bit abrupt


```
<div id="photos">
  <img alt="Glendatronix" class="show" src="../../images/glenda_200.jpg" />
  <img alt="Darth Fader" src="../../images/fader_200.jpg" />
  <img alt="Beau Dandy" src="../../images/beau_200.jpg" />
  <img alt="Johnny Stardust" src="../../images/johnny_200.jpg" />
  <img alt="Mo' Fat" src="../../images/mofat_200.jpg" />
</div>

$(function(){
	slideShow();
});

function slideShow() {
	var current = $('#photos .show');
	// if next() exists (has length?) fine if not take the first element
	var next = current.next().length ? current.next() : current.siblings().first();

	current.hide().removeClass('show');
	next.fadeIn(1000).addClass('show');

	setTimeout(slideShow, 1000);
}

```

### Simple menu slide down sublist and slide up 

```
<div id="celebs">
	<h2 class="heading">Our Celebrities</h2>
	<p class="info">
		We have an ever changing roster of newly chipped celebrities. But it can take as little as a week for the little critters to realise they've been tagged - so you have to be fast! 
	</p>
  <ul id="accordion">
  	<li class="active">
  		A-List Celebrities
  		<ul>
  			<li><a href="#">Computadors</a> &nbsp;New!</li>
        <li><a href="#">Johny Stardust</a></li>
  		  <li><a href="#">Beau Dandy</a></li>
      </ul>
  	</li>
  	<li>
  		B-List Celebrities
  		<ul>
  			<li><a href="#">Sinusoidal Tendancies</a></li>
  			<li><a href="#">Steve Extreme</a></li>
  		</ul>
  	</li>
  	<li>
  		Has Beens
  		<ul>
  			<li>Duran Duran Duran</li>
  			<li>Mike's Mechanic</li>
  		</ul>
  	</li>
  	<li>
  		Barely Famous Celebrities
  		<ul>
  			<li>Lardy Dah</li>
  			<li>Rove Live</li>
  		</ul>
  	</li>
  </ul> 
</div>

$(function(){
  $('#celebs ul > li ul')
    .click(function(){
        // after it's down we don't want ul to be clickable and pass the click to it's parrent
        $(this).stopPropagation();
      })
    // filter out first element; first submenu should be open and all other hidden
    // filter - any elements that match the criteria are discarded
    // $(':not(p)') - all not paragraphs
    // $('p:not(.active)')
    // or function
    // we have access to zero based index of each element in the collection
    // $('p').filter(function(index) {
    //    return index == 2 || $(this).hasClass(.active);
    // })
    .filter(':not(:first)')
    .hide();
    
  $('#celebs ul > li').click(function(){
    // let's store if clicked li > ul is already visible
    var selfClick = $(this).find('ul:first').is(':visible');

    if (!selfClick) {
      // so we clicked other then visible, let's hide all other visible first
      $(this)
        .parent()
        .find('> li ul:visible')
        .slideToggle();
    }

    $(this)
      .find('ul:first')
      .slideToggle();
  })
})
```

### Simple Tabs

```
<ul id="info-nav">
  <li><a href="#intro">Intro</a></li>
  <li><a href="#about">About Us</a></li>
  <li><a href="#disclaimer">Disclaimer</a></li>
</ul>
<div id="info">
	<p id="intro">
		Welcome to <strong>StarTrackr!</strong> the planet's premier celebrity tracking and monitoring service. Need to know where in the world the best bands, musicians or producers are within 2.2 square meters? You've come to the right place. We have a very special special on B-grade celebs this week, so hurry in!		
	</p>
  <p id="about">
    StarTrackr! was founded in early 2009 when a young entrepreneur from Los Angeles discovered a way to tag people with GPS-enabled RFID tags without their knowledge. Being from LA, his first thought was to use this technology to enable fans to track and locate their favourite celebrities. And thus the phenomenon was born!
  </p>
	<p id="disclaimer">
		Disclaimer! This service is not intended for the those with criminal intent. Celebrities are kind of like people so their privacy should be respected.
	</p>
</div>

$(function(){
	$('#info p:not(:first)').hide(); // hide all paragraphs other then first one

	$('#info-nav li').click(function(e){
		e.preventDefault();

		$('#info p').hide();		// hide all paragaraphs
		$('#info-nav .current').removeClass('current');
		$(this).addClass('current');	// add current class to li from navigation

		var clicked = $(this).find('a:first').attr('href');  // find href attribute of clicked link
		$('#info ' + clicked).fadeIn('fast');		// fade in paragraph with id = clicked

	}).eq(0).addClass('current');
});
```

### Slide down and up Login Panel

```
<div id="login">
  <a href="#">Log in</a>
  <form action="">
    <div>
      <label for="username">Username:</label>
      <input name="username" id="username" type="text"/>
    </div>
    <div>
      <label for="password">Password:</label>
      <input name="password" id="password" type="password"/>
    </div>
    <div>
    	<input type="submit" value="Log in!" />
  	</div>
  </form>
</div>

$(function(){
  $('#login form').hide();

  $('#login a').toggle(function(){
    $(this)
      .addClass('active')
      .next('form')
      .slideDown();
  },
    function(){
      $(this)
        .removeClass('active')
        .next('form')
        .slideUp();
    }
  );  // end of toggle

  $('#login form :submit').click(function(){
    $('#login a form').slideUp();
  });
});
```
























