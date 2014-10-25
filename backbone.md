# Backbone.js

## Components

* Models - store data
* Views - display model data onto a web page
* Collections - a groupo of models, really a JS array
* Events - bind custom events to our code
* Routers - create navigation in our web app
* Sync - maps Backbone data to the server-side

All components are build using JS objects - simple key/value pairs of JS methods & properties

```
class Person extends Backbone.Model
	defaults: ->
		name: "Guest User"
		age: 23
		occupation: "Worker"

	validate: (attrs) ->
		return 'Age must be positive.' if attrs.age < 0
		return 'Person must have a name' if !attrs.name

	work: ->
		console.log @get('name') + ' is working.'  # get is a backbone function
```

accessing attributes:

Instead of `person.name` use `person.get('name')` or `person.set('name')`
to get all attributes: `person.toJSON` will return JSON object

`validate` is triggered by `.set` or `.save`. If you want `validate` to be triggered with `.set`, 
you need to include `{validate: true}`:

`dog.set('name', 'a', {validate: true})`

### Views 

You can bind your view's `render` function to the model's "change" event - and now everywhere that
model data is displayed in UI, it is always immediately up to date.

`initialize` method is called automaticaly. You can pass options that can be attached to the view:
`model`, `collection`, `el`, `id`, `className`, `tagName`, `attributes` and `events`

`el` is created from view's `tagName`, `className`, `id` and `attributes`, if specified. If not, 
`el` is an empty `div`.

```
# MODEL
class Person extends Backbone.Model
	defaults: 
		name: "Guest User"
		age: 23
		occupation: "Worker"

	validate: (attrs, options) ->
		return 'Age must be positive.' if attrs.age < 0
		return 'Person must have a name' if !attrs.name

	work: ->
		console.log @get('name') + ' is working.'  # get is a backbone function


# VIEW

class PersonView extends Backbone.View	
	tagName: 'li'	 # defaults to div if not specified
	className: 'person'  # optional, can also set multiple like 'person european'

	events: 
		'click':					'alertTest'
	
	initialize: (options) ->
		@render()		# render is an optional function that defines the logic for rendering a template

	render: -> 
		@$el
			.html @model.get('name') + ' is ' + @model.get('age') + ' years old and works as ' + @model.get('occupation') 
			.appendTo $('#container')

	alertTest: ->
		alert 'klikles!'

$ ->
	person = new Person
	personView = new PersonView model: person
```

## Collections
Collections are sets of Models and are created by extending `Backbone.Collection`

`add()` adds element to the collection and `remove()` removes
`Collection.get()` - retrieves model from a collection
`resets()` - updates collection if you pass arguments or clears collection when used without arguments

#### forEach()
```
todos.forEach(function(model){
	console.log(model.get('title'))
})
```

`<%= %>` - variable interpolation 
`<%- %>` - interpolate variable and have it HTML-escaped
`<% %>` - execute arbitrary javascript code





