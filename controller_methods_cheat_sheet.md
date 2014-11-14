# Starting Steps
* In routes.rb add:
    
    resources :teams do 
       resources :players
    end

This is because the resource players belongs to teams. Players are now "nested" inside players.

* Now:
```
rake routes
```
This generates a table that shows all the paths and controller actions.

* Now generate models.
* Generate controllers.
* Now look at rake routes and copy the controller/actions to the controllers:

```
     def index
     end

     def create
     end

     def new
     end

     def edit
     end

     def show
     end

     def update
     end

     def destroy
     end
```

# Controller Actions
## index
This is for generating a home or "starting" page with a list of items from the models. For example, to list all the teams in a football team manager, you would use this method:
``` 
def index
	@teams = Team.all
end
```
Make sure to create a corresponding view for displaying the teams. Make index.html.erb. In the file write a loop to display all the teams:
```
<% @teams.each do |t| %>
	<h2><%= t.name %>, <%= t.country %></h2>
	<% t.players.each do |p| %>
		<p><%= p.name %></p>
	<% end %>
<% end %>
```
## show
The show method is used to display information about an individual database record. In the football app example we have:
```
def show
	@team = Team.find(params[:id])
end
```
This creates an array that displays all the fields for a particular team having a specific id. In the views file we have:
```
<h2><%= @team.name %>, <%= @team.country %></h2>
```


## new
This method displays the form needed to create a new record. It doesn't actually create the record, though. The create method below handles the creation. In the football app example, we used this:
```
def new
	@team = Team.new
end
```
And in the views file we used:
```
<%= form_for @team do |f| %>
	<%= f.text_field(:name, placeholder: "Team name") %>
	<%= f.text_field(:country, placeholder: "Country") %>
	<%= submit_tag("Submit New Team") %>
<% end %>
```


## create
This is tied to the new method above. Once we get the data from the view containing the data, create creates the database record. In the controller:
```
Team.create(team_params)
```
team_params in this case equals 
```
params.require(:team).permit(:name, :country)
```

## edit
This method displays the form needed to edit an existing record. It pulls data out of the database and populates a form. It does not change the record in the database.

## update
This method updates a database record once receieved from the form. It usually works in tandem with the edit method above

## delete
This deletes a record in the database. CAREFUL!
