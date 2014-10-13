#Coffescript

`coffee` - starts coffeescrip console

`$.each [1,2,3,4], (index, value) -> alert(index + ' is ' + value)`

basic file structure

-public
|   |_css
|   |_js
|   |_index.html
|
|_src <- where coffescript file sits

Basic compiling command:
`coffee -co public/js -w src/`

To start the server
`http-server`

and your page should be on `localhost:8080` hosting all files from the public folder

##  Handlebars

3 steps:

1. get a content in var content
2. compile var renderer = Handlebars.compile(content)
3. var result = renderer(jsonObject with data to be included in template)


## class definition
```
class Photo
	constructor: (url) ->
		@url = url 				//  @ means this.url 

// you can shorten to:

class Photo 
	contructor: (@url) ->
```

## inheritance

```
class Thumbnail extends Photo
	createElement: ->
		$el = super				 // create original behavior from Photo class
		$el.height = 100
```

## Bound functions

```
class PersonView
	constuctor: ( @person, @el ) ->

request: ->
	$.get @person.url, (data) => 
		$(@el).html data 		// in javascript @el == this.el would lose meaning b/c this would be lost
		// in coffeescript using => you still can keep 'this'

```

```
class personView
	constructor: (@person, @el) ->
		$(@el).bind 'click', @showName

	showName: =>
		$(@el).html @person.name
```

## conditionals

```
@request() if @isActive()

return unless $('li').length   // unless is opposite of if

result + 10 if result?  // checks if result is null or undefined

// soak operator

@panel?.restore() // if pannel is null the restore function will not be executed

// assignments

@panel.url ?= window.location  // set it if url is undefined/null so it has not been set yet

```

## destructuring assignments

```
// instead of 

name = person.name

// write
{name} = person  

// with multiple properties
{name, age} = person

// u can use it with arrays

[first, last] = person.name.split " "
```

## Compiling

`coffee -cwo public/js - w src/` - compiles src/ folder into public/js with the whole folders' structure

























