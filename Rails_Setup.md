# How to set up a Rails API  

This readme assumes that you have the proper environment set up with `rvm`, Rails, and Ruby installed. It also assumes that you have used ActiveRecord in Mod 1 of the Flatiron School Curriculum.  

### Step 1: Creating a new Rails API  

First you will want to create a new instance of rails using the command line. Navigate to the folder you want the project folder to live in, and type into the command line:  

`rails new <project-name> --api`  

where `<project-name>` is your project's name. The `--api` option tells rails that we don't necessarily want to use the .erb files to display webpages, and that this project is basically just a back-end of a website or app.  

This command will generate a lot of folders & files that allows Rails to operate.

### Step 2: Adding models & controllers  

Great! We have an API. But we need to populate it with something for it to be useful. Rails comes with generators that will do a lot of work for us. Some we will be using will be the model generator and controller generator.  

The model generator will create a migration file (to create the table for the object), a model file (to store the object class for Ruby). To generate your model, first we need to get into the directory that you created in Step 1. In the command line, type:  

`cd <project-name>`  

Excellent, now we are in the directory and all of these generators will actually work. Then to generate your model, type in the command line:  

`rails g model <model-name>`  

You can also include attribute names if you don't want to edit the migration file later on. I will give an example at the bottom of this file to demonstrate this, but basically, you would append `model-attribute1 model-attribute2` at the end of the above command. If you want the attribute to be a specific type, you need to include this after a colon. For example, `model-attribute2:integer`. The default data type is a string, which holds only 255 characters. The `text` type allows for many more characters. Feel free to look up more data types based on your database. This tutorial assumes `sqlite3`.  

After hitting enter, this command should generate several files for you, namely: the migration file and the model file. If you didn't include attributes above when generating your model, now is a good time to edit this file and add those attributes in. It should be located in the `db/migrate` folder within your project directory. You can leave your model file alone for now.  

Awesome, now we have a model file and a migration for that model. Let's add a controller so that we can access this model using the API.  

To generate a controller file, type into the command line:  

`rails g controller <plural-model-name>`  

This will generate our controller. It needs to be the plural of whatever your model name is. That's because the controller is in charge of dealing with all of the models of that name and accesses the database looking for a table that will generate with that plural. For example, if I have a Pirate model and a pirates table, my controller will need to be called 'Pirates_Controller' and not 'Pirate_Controller'. This is a Rails convention.  

Press enter and voila! We should have a controller. We've got all the files we need to make our API function. Time to dig in to the actual code with an editor. I use VS Code so my command is `code .`. Substitute 'code' for whatever editor you use to look at the files.  

### Step 3: Creating the route  

If you haven't opened the editor until this point, you will notice there are a metric butt-load of files that Rails generated. We can ignore most of these - we are only interested in the files that we generated.  

First we need to set up the route so that our API properly redirects us to the correct controller. Inside the `config` folder is a file called `routes.rb`. Open that in your editor. You'll notice there are no routes. Let's change this so that when people go to your server they will find what they are looking for.  

Add the following to your `routes.rb` file, inside the method it is providing:  

`resources :model_plural`  

This will provide routes for every kind of request for your model: GET, POST, PUT, PATCH, DELETE. You can see this by typing `rails routes` in the command line.

