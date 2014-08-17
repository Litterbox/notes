## Models and Validation

.yml - YAML, YAML Ain't Markup Language (recursive definition and a joke)

## Rake

Rake is a simple ruby helper program. It helps us to perform tasks by running scripts. A typical rake command works like rake and then a space, followed by whatever task we'd like it to perform. We can also write our own tasks and if we did, those would go inside the lib tasks folder, which is here. We can see which tasks are available, both the Rails default tasks and any custom tasks from the command line.

In terminal you can type type rake -T. That's going to return a list of the tasks that we have available. It returns a long list of all the tasks. Notice in particular, that some of these tasks have db in front of them. There's quite a few of them that are used for working with the database. If we want to see just those listings, you can amend your last command so that it's rake -T db.

## Migrations

Once you create a database and configure your Rails project to connect to it, you need to add tables. One way to do this is by writing Rails migrations. A migration is a set of database instructions. Those instructions are Ruby code, which migrates our database from one state to another. Essentially they describe database changes. In our migration we can create a table, add a column, change the name of a column, drop a table and much more. A migration will contain both the instructions for moving up to a new state, and also instructions for moving back down to the previous state.

If a migration has instructions to create a table when moving forward or up, it will also include the instructions to allow it to move back down by dropping the table. If you move up by adding three columns to the table then you'll also have instructions to move back down by removing those three columns. Being able to move in both the directions like this allows us to migrate in both directions. We can migrate our database to the newest version or migrate back to a previous version. Why use migrations? Migrations maintain our database schema with our application code.

## Generating migrations

These reside in our db directory and to create one we use

```rails generate migration MIGRATION_NAME```

This comes with a change method which is a shortcut, so instead let's build it out the long and short way using up and down.

When you generate a model in rails it will generate a matching migration

```rails generate model MODEL_NAME```

use create_table and drop_table to remove tables
we use a code block to add columns
```t.column "first_name", :string, :limit => 50```
or
```t.string "first_name", :limit => 50```

Table column types

```
binary
boolean
date
datetime
decimal
float
integer
string
text
time
```

Table column options

```
:limit => size
:default => value
:null => true/false
:precision => number
```

Also note that Rails automatically adds an ID column

## Running migrations

``` rake db:migrate RAILS_ENV=_____``` (by default it is development)

Rails will run all migrations that have not been run with rake db migrate

To go back

```rake db:migrate VERSION=0```

To get the ID for jumping back and forth use 

```rake db:migrate:status```

Then
```rake db:migrate VERSION=ID```

Or
```rake db:migrate:up VERSION=X```
```rake db:migrate:down VERSION=X```

## Migration methods

```
drop_table(table)
rename_table(table, new_name)
add_column(table, column, type, options)
remove_column(table, column)
rename_column(table, column, new_name)
change_column(table, column, type, options)
add_index(table, column, options)
execute("any SQL string") - rare
```

What does `change` do? It knows how to go up and down
Sometimes you can not reverse things with change like when you remove a column

## ActiveRecord

ORM that makes our objects intelligent without using SQL
```
user = User.new
user.first_name = "Elie"
user.save
user.delete
```

## Creating a model

`rails generate model CamelCaseName`

- This creates a migration file
- It also creates a model_name.rb file
- File names, class names and table names really matter!

## CRUD in Rails Console

- to enter, go to terminal and in the root of your rails app type - `rails console or rails c`
- this is IRB with your rails app loaded in

#### Creating

2 Different ways

##### New/save

1. Instaniate an object
2. Set values 
3. Save

- user = User.new
- user.new_record? returns true or false if it exists in the DB
- user.first_name = "Elie"
- user.first_name -> returns "Elie"
- user = User.new(:first_name => "Elie", :last_name => "Schoppik")
- user.save -> saves to the DB
- user.id -> 1


##### Create

1. Do all in 1 step

- user = User.create(:first_name => "Elie", :last_name => "Schoppik") 

#### Updating

2 Different ways

Find/save
1. Find - user = User.find(1)
2. Set - user.first_name = "Taco"
3. Save - user.save

Update
1. user = User.find(1)
2. user.update_attributes(:first_name => "taco")

#### Delete

Find/destroy
1. Find - user = User.find(1)
2. Destroy (not delete, delete bypasses some rails features stick with destroy)- user.destroy

You still have this when it's deleted you just can't change anything

#### Finding

1. Primary key finder (use when it's expected to exist)
 - User.find(number)
2. Dynamic Finder
	- User.find_by_id(number) -> returns nil instead of error
	- User.find_by_first_name(string) -> returns nil instead of error
3. User.all -> returns an array of objects
4. User.first -> finds first
5. User.last -> finds last

#### Query methods - conditions

Search using conditionals:

Where(conditions)
	- User.where(:first_name => "Elie")
	- this returns an ActiveRelation object and can also be chained
	- can pass in a hash, string or array
		- User.where("first_name" = "Elie")
		- User.where(["first_name" = ?, "Elie"]) - SQL injection safe	
	- use .first to get the object instead of array

#### Query methods - order, limit and offset

- order (table_name.column_name ASC/DESC)
- limit (integer)
- offset (integer)

- these can be chained together 

## Validations

#### Validation methods

for all of these validations you can pass in an error message of - :message => "Something error related" 

- validates_presense_of - attribute must not be blank
- validates_length_of - must have a length of x. Pass in a hash with (:is, :minimum, :maximum, etc.) 
- validates_numericality_of - attribute must be an integer or float (can pass in :equal_to)
- validates_inclusion_of - attribute must be in a list of choices 
- validates_exclusion_of - attribute must be in a list of choices 
- validates_format_of - attribute must match a regular expression (pass in :with)
- validates_uniqueness_of - attribute must be unique
- validates_acceptance_of - makes sure an attribute is accepted (a TOS is agreed)
- validates_confirmation_of - attribute must be confirmed (type in password twice). Rails will only run this if the attribute is set to something
- validates_associated - validates associated objects (validate options in associated relationships)

- can pass in (:on => :save/:create/:update) to specify when to validate
- can also pass in :if => :method / :unless => :method to help with determining when to validate (only check email if user wants to be identified by email)

#### Using validation methods

- Before you even start - think and ask yourself what should I validate?
- Add the validations after your associations in the model
- in rails console you can run s.valid? to see if it's valid and then s.errors to see what's wrong if there is a problem.

#### Validates Method

- shortcut for validations 
- wrap these all up in a hash

```
validates :COL_NAME, :presence => true, 
										:length => {:maximum => 50}, 
										:numericality => false, 
										:uniqueness => true
```

#### Custom validations
```
validate :custom_method

def custom_method
	# some validation goes here
end
```

example: 

```
FORBIDDEN_USERNAMES = ["taco", "Elie"]
validate :username_is_allowed

def username_is_allowed
	if FORBIDDEN_USERNAMES.include?(username)
		errors.add(:username, "this is a restricted usernmae")
	end
end
```

https://github.com/wdi-sf-march-2014/notes/blob/master/IntroRailsRelated/ModelsInRails/rails_models.md
