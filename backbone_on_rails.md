# Backbone on rails with Upcase.com

After creating of new rails app run

- remove turbolinks from both application.js and gemfile
- remove turbolinks from views/layouts/application.html.haml(erb)
- `rails generate backbone:install`
- don't forget to add haml gem to gemfile

main .coffee file has the application name and is in `assets/javascript` main directory

add route: `root to: 'application#index'`
add `views/application/index.html.haml`

After creating simple model and controler for notes in rails add notes for `:show` and `:index` actions in rails.
Create corresponding views `views/index.html.haml` and `views/show.html.haml` and remove those created in application
folder before.

## Create Backbone routes

In `assets/javascript/routers` create file `scratch_pad_router.js.coffee` that creates class ScratchPadRouter

```
class App.Routers.ScratchPadRouter extends Backbone.Router
	routes:
		# emtpy string for index
		'': -> alert 'hello from index page router!'

		'/notes/:id': 	'showNote'

		showNote: (id) ->
			alert "You requested a note with id of #{id}"
```

Initialize routers in main backbone file `scratch_pad.js.coffee`

```
window.ScratchPad =
  Models: {}
  Collections: {}
  Views: {}
  Routers: {}
  initialize: -> 
  	# initialize App.Routers
  	new @Routers.ScratchPadRouter
  	Backbone.history.start()
```