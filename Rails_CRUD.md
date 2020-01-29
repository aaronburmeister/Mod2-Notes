# CRUD using Rails API  

By the end of this note, you should be able to: Write Rails Actions for CRUD Methods  
HTTP Requests come in to the Router, which looks for the Method and the Path.  
The Router redirects incoming requests based on the method (GET, POST, etc.) and the Path (url).  
It redirects to a controller action (create, destroy, etc.). The controller interacts with the database using the model. The action completes and sends an HTTP Response back.

MVC = Model View Controller  

ReST

Method | Path | Action  
--------|-------------|----------
GET | "users" | index  
GET | "users/:id" | show  
POST | "users" | create  
PUT/PATCH | "users/:id" | update  
DELETE | "users/:id" | destroy  

`rails new truck-stop --api`  
to routes.rb, add `get "trucks", to: "trucks#index"`  
command line: `rails g controller trucks`  
to trucks_controller.rb, add
```ruby
def index
  @trucks = Truck.all
  render json: @trucks
end
```  
in command line: `rails g model truck`  
in migration file, add attributes  
run `rails db:migrate`  
create seeds  
run `rails db:seed`  
run `rails s` to start server. check out http://localhost:3000/trucks  
All your seeds should be displayed in json.  

### Now to add other methods! C, U, and D.  
#### Show  
To router add: `get "trucks/:id", to: "trucks#show"`
To controller add:  
```ruby
def show
        @truck = Truck.find(prams[:id])
        render json: @truck
    end
```  
#### Create  
To router add: `post "trucks", to: "trucks#create"`  
To controller add:  
```ruby
def create
        @truck = Truck.create(make: params[:make], model: params[:model])
        render json: @truck
end
```  

#### Update  
To router add: `put "trucks/:id", to: "trucks#update"`  
To controller add:  
```ruby
def update
        @truck = Truck.find(prams[:id])
        @truck.update(make: params[:make], model: params[:model])
        @truck.save
        render json: @truck
end
```  

#### Delete  
To router add: `delete "trucks/:id", to: "trucks#destroy"`  
To controller add:  
```ruby
def destroy
        @truck = Truck.find(prams[:id])
        @truck.destroy
        render status: :no_content
end
```  

`resource "trucks"` wraps all of the router additions we just added  


#### Adding new column  

`rails g migration add_color_to_truck`  
in migration file, `add_column :trucks, :color, :string`  
Then you can update seeds
