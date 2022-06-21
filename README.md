- [CRUD and scaffold generators - Text directions, references and code](#crud-and-scaffold-generators---text-directions-references-and-code)
  - [One line Scaffold Generation in Rails](#one-line-scaffold-generation-in-rails)
- [Chpt 76 Introduction to Section 4: Tables, migrations and naming conventions](#chpt-76-introduction-to-section-4-tables-migrations-and-naming-conventions)
  - [This Section of the Complete ROR Dev Course Looks at Manually Creating all the Functionality that the one line Scaffold Generator Creates](#this-section-of-the-complete-ror-dev-course-looks-at-manually-creating-all-the-functionality-that-the-one-line-scaffold-generator-creates)
  - [Resource: Articles](#resource-articles)
    - [Rails naming conventions - Articles resource](#rails-naming-conventions---articles-resource)
    - [Database Amendment - Preferred method of amendment](#database-amendment---preferred-method-of-amendment)
- [Notes from Chpt 77](#notes-from-chpt-77)
  - [Details](#details)
- [chpt 78 Models and rails console](#chpt-78-models-and-rails-console)
  - [Create](#create)
  - [Chpt 80 Read, Update, Delete](#chpt-80-read-update-delete)
    - [Getters](#getters)
    - [Setters](#setters)
    - [Delete](#delete)
    - [Note](#note)
    - [Chpt Summary](#chpt-summary)
  - [Chpt 82 Validations](#chpt-82-validations)
    - [Validation further](#validation-further)
  - [Chpt 84 Show articles (route, action and view)](#chpt-84-show-articles-route-action-and-view)
    - [Config routes.rb](#config-routesrb)
    - [Config controller](#config-controller)
    - [Create instanced variable](#create-instanced-variable)
    - [Display instanced variable](#display-instanced-variable)
  - [Chpt 85 Show articles feature - text references and code](#chpt-85-show-articles-feature---text-references-and-code)
  - [Chpt 86 Articles Index](#chpt-86-articles-index)
    - [build the route](#build-the-route)
  - [Chpt 88 Forms - Building New Article Creation Form](#chpt-88-forms---building-new-article-creation-form)
    - [Building the Form](#building-the-form)
  - [Chpt 90 Create Action - Save newly created articles](#chpt-90-create-action---save-newly-created-articles)
    - [Adjustment from Text & Video](#adjustment-from-text--video)
    - [What happens after the creation?](#what-happens-after-the-creation)
  - [Chpt 92 Messaging - Validation and Flash Messages](#chpt-92-messaging---validation-and-flash-messages)
    - [Using Flash to Show the Article has been Saved to the Database](#using-flash-to-show-the-article-has-been-saved-to-the-database)
  - [Chpt 94 Edit and Update Existing Articles](#chpt-94-edit-and-update-existing-articles)
  - [Chpt 96 Delete Article](#chpt-96-delete-article)
    - [Embedded Ruby html linking](#embedded-ruby-html-linking)
    - [Edit Article Link](#edit-article-link)
  - [Chpt 98 User Interface - Layout Links](#chpt-98-user-interface---layout-links)
    - [Link on Articles Listing Page to Create a new Article](#link-on-articles-listing-page-to-create-a-new-article)
    - [Add "confirmation action" when deleting](#add-confirmation-action-when-deleting)
    - [Heroku Database](#heroku-database)
  - [Chpt 100 DRY (Don't Repeat Yourself) - code refactoring & partials](#chpt-100-dry-dont-repeat-yourself---code-refactoring--partials)
    - [Views](#views)
      - [Let's create the partial for "new" & "edit"](#lets-create-the-partial-for-new--edit)
  - [Chpt 102 Production Deploy to Heroku](#chpt-102-production-deploy-to-heroku)
    - [verify Gemfile](#verify-gemfile)
- [Section 5 STYLING](#section-5-styling)
  - [Introduction](#introduction)
  - [Chpt 106 Install Bootstrap on Rails](#chpt-106-install-bootstrap-on-rails)
    - [Nav Bar Test](#nav-bar-test)
    - [GoRails](#gorails)
    - [Installing Yarn via npm](#installing-yarn-via-npm)
    - [Sync with GIT](#sync-with-git)
    - [Install Bootstrap](#install-bootstrap)
      - [Updating npx](#updating-npx)
    - [Back to installing Bootstrap](#back-to-installing-bootstrap)

# CRUD and scaffold generators - Text directions, references and code
Query language to communicate with database: SQL (Structured Query Language)

CRUD actions:

C - Create

R - Read

U - Update

D - Delete

## One line Scaffold Generation in Rails
Scaffold generator command to create an article model (with two attributes), articles controller, views for articles and migration file to create articles table:

rails generate scaffold Article title:string description:text

Command to see routes presented in a viewer-friendly way:

rails routes --expanded

The line resources :articles in the config/routes.rb file provides the following routes:

- index of articles (GET request)

- new article (GET)

- create article (POST)

- edit article (GET)

- update article (PUT and PATCH)

- show article (GET)

- delete article (DELETE)

From UI perspective ->

- index lists all the articles in the articles table in the database of the app

- new article deals with the form to enter in new article details

- create handles the submission of the items in the new article form

- edit article deals with the form to enter edited information for an existing article

- update article deals with the submission of the edit article form

- show article displays an individual article based on selection

- delete article deletes an article from the articles table

In preparation for the next section, learn and practice SQL here: https://www.w3schools.com/sql/
# Chpt 76 Introduction to Section 4: Tables, migrations and naming conventions
## This Section of the Complete ROR Dev Course Looks at Manually Creating all the Functionality that the one line Scaffold Generator Creates

Rails naming conventions - Articles resources
- model
- Table
- controller
- views
## Resource: Articles
The resource will have an articles model, articles table, articles controller, and also views that allow us to perform all the CRUD actions from the front end. Let's start by looking at the Model and Table.
### Rails naming conventions - Articles resource
- Model name: article (Rails will define an article (singular))
- Article model file name: article.rb
- Article model class name: Article
- Table name: articles (Rails will maintain articles (plural))
We will start by building the table.

![articles table](articles_table.png)

1. The id column will be automatically generated by Rails. It will be the primary key of this table.
2. title property will be string (255 character limit)
3. description property will be text (as provides for more text than string)

To generate a table we need a migration file. In your project directory create a migration file called "create_articles"
```
rails generate migration create_articles
```
We use the generator to create migration files as Rails automatically appends a time stamp (see the string of numbers in the filename). This becomes important as we create or append migration files.

Rails creates the table (as one doesn't exist), and we need to add the title attributes. For now we just put in the article title attribute (we'll do details later).
```ruby
  t.string :title
```  
I noted that my Rails already had:
```ruby
  t.timestamps
```
Whereas Mushrur's video did not show this. I presume this is because I'm using a later version of Rails.

Now we will run this migration file. Note that Rails only runs migration files that have never run before.
```
rails db:migrate
```
You can see the newly minted table in the db folder, schema.rb

Rails only runs the migrate command on files that have never been migrated. If there are no new migrate files then nothing will happen.

If you want to update or append an existing table you have to rollback the previous migration, and run rails migrate again. Of course it is not the preferred way to create a database table.

To rollback (or undo) the last migration, do:
```
rails db:rollback
```
You can then go to the last migration creation file and update it to what you wanted.
```ruby
class CreateArticles < ActiveRecord::Migration[7.0]
  def change
    create_table :articles do |t|
      t.timestamps
      t.string :title
      t.text :description
    end
  end
end
```
The schema file will now have the updated attributes.

However, as mentioned, rollback is not the preferred method to deal with amending a table.

E.g. When coding in a team, if you used rollback on your version and then uploaded the code changes, another team member couldn't run the same migration file as it would already have run. So the code bases will be different.

### Database Amendment - Preferred method of amendment
Create a new migration file to reflect any changes to the database. That way, in a team a team member will see there is a new migration file.

E.g. A new migration file:
```
rails generate migration add_author_to_articles #note that Mashrur had add timestamps here instead of author, but the latest Rails automatically adds timestamps, so there is no need to do that.
```
The syntax for adding to an existing table is:
```ruby
  add_column :[name of table], :[title of attribute], :[datatype]
```
So my change showed:
```ruby
class AddAuthorToArticles < ActiveRecord::Migration[7.0]
  def change
    add_column :articles, :author, :string
  end
end
```
Now that we have our table, we'll need our model (or articles model) to work with this table.
# Notes from Chpt 77
## Details

Model name: article

Class name: Article -> Capitalized A and singular, CamelCase

File name: article.rb -> singular and all lowercase, snake_case

Table name: articles -> plural of model name and all lowercase

Additional example:

Model name: user

Class name: User -> Capitalized U and singular, CamelCase

File name: user.rb -> singular and all lowercase, snake_case

Table name: users -> plural of model name

Generate a migration to create a table (in this example articles):

rails generate migration create_articles

To add attributes for the table in the migration file, add the following inside create_table block:
```
t.string :title
```
To run the migration file, run the following command from the terminal:
```
rails db:migrate
```
The first time you run the migration file, it will create the database, the articles table and a schema.rb file.

To rollback or undo the changes made by the last migration file that was run, you may use the following command:
```
rails db:rollback
```
If you have run the rollback step, then you can update the previous migration file and add the following line to add a description attribute (column) to the articles table:

    t.text :description

To run the newly edited migration file again, you can run
```
rails db:migrate
```
Note: This above line will only work if you had rolled back the prior migration.

To generate a new migration file to add or make changes to your articles table you can generate a new file:
```
rails generate migration name_of_migration_file
```
Then within the def change method in the migration file you can add the following lines:

    add_column :articles, :created_at, :datetime
    add_column :articles, :updated_at, :datetime

You can run the newly created migrations file by running rails db:migrate from the command line and check out the schema.rb file to check that the changes were reflected properly.
# chpt 78 Models and rails console
First we create article.rb in the App > Model folder. Every model we make will be based on the ApplicationRecord < ActiveRecord base. In the article.rb file we write:
```ruby
class Article < ApplicationRecord

end
```
That is all that's needed in order to communicate with the database. This gives us Getters and Setters to interact with the articles in the database, through the Rails Console (IRB).

We can access the console by typing ```rails console``` or ```rails c``` in our terminal.

To see all our articles in the database we type the Class then all:
```ruby
Article.all
```
## Create
To create table entries directly, we:
```ruby
Article.create(title: "first article", description: "description of first article", author: "Draco Satiric")
```
A preferred way of doing it in the console is through using variables.
E.g.
```ruby
article = Article.new
```
Then it is easy to ascribe properties:
```ruby
article.title = "second article"
article.description = "description of second article"
article.author = "Blazmer Mahmoud"
```
However, up to this point the object is not saved in the database. It is only in the console. If you look you'll see that the id, created at, and updated at, fields are all "nil"
```ruby
irb(main):009:0> article
=>
#<Article:0x00007f0e3b6925f8                                                    
 id: nil,                                                                       
 created_at: nil,                                                               
 updated_at: nil,                                                               
 title: "second article",                                                       
 description: "description of second article",                                  
 author: "Blazmer Mahmoud">                                                     
irb(main):010:0>
```
The way to "hit" the article database table is:
```ruby
article.save
```
A third way to enter an object into the database is to put the properties all on one line:
```ruby
article = Article.new(title: "third article", description: "description of third article", author: "Shysna Pzycq")
```
Now there will be 3 articles in the articles table.
## Chpt 80 Read, Update, Delete
To search for a specific object in the table if you know the id:
```ruby
Article.find(2) #where 2 is the object id
```
If you wish to change something about an object then it is better to create a variable linked to an article object.
E.g.
```ruby
article = Article(2)
```
### Getters
Now when I call article I will get the 2nd article. If I just wanted to see the title of the second article then I can use the variable as a Getter, i.e.
```ruby
article.title
article.description
article.author
```
### Setters
How about using Setters? What if we wanted to update the description of the 2nd article?
```ruby
article.description = "edited - description of second article"
```
However, this has not hit the database table. As you can see if you type in:
```ruby
Article.find(2)
=>
#<Article:0x00007f0f296f1a28                                                    
 id: 2,                                                            
 created_at: Tue, 24 May 2022 06:42:46.650887000 UTC +00:00,       
 updated_at: Tue, 24 May 2022 06:42:46.650887000 UTC +00:00,       
 title: "second article",                                          
 description: "description of second article",                     
 author: "Blazmer Mahmoud">  
 ```
To reflect the change in the database table we must save it:
```ruby
article.save
```
### Delete
How do we delete an object in the database table? Let's do it with the last article in the table.
```ruby
article = Article.last
```
We delete the article by using "destroy",
```ruby
article.destroy
```
Now, note that this hits the database immediately. There is no need to save.
```ruby
irb(main):014:0> article.destroy
  TRANSACTION (0.2ms)  begin transaction
  Article Destroy (1.3ms)  DELETE FROM "articles" WHERE "articles"."id" = ?  [["id", 3]]                                                           
  TRANSACTION (103.1ms)  commit transaction                        
=>                                                                 
#<Article:0x00007f0f2972acb0                                       
 id: 3,                                                            
 created_at: Tue, 24 May 2022 07:14:31.993903000 UTC +00:00,       
 updated_at: Tue, 24 May 2022 07:14:31.993903000 UTC +00:00,       
 title: "third article",                                           
 description: "description of third article",                      
 author: "Shysna Pzycq">                                           
```
### Note
If we look at the model (app>models>article.rb) there are no restrictions to what can be created. We could create one with no title and no description and it will still hit the table. We don't want this as it ruins the integrity of the table. We want to put in restraints to what can be added. That is, add validations.

### Chpt Summary
To find an article by id you can use the find method like below:
```ruby
Article.find(1) # replace 1 with id of article you want to find
```
You can save this to a variable and use it like below
```ruby
    article = Article.find(1)
    article.title # to display (get) the title
    article.description # to display (get) the description
```
You can use the methods below to view the first and last articles of the articles table:
```ruby
    Article.first # display the first article in the articles table
    Article.last # display the last article in the articles table
```
You can update an article by finding it first and then using setters for the attributes that the model provides like below:
```ruby
    article = Article.find(id of article you want to edit)
    article.title = "new title"
    article.description = "new description"
    article.save
```
You can delete an article by using the destroy method. A sample sequence could be like below:
```ruby
    article = Article.find(id of article you want to delete)
    article.destroy
```
## Chpt 82 Validations
First, we wish to ensure that an object in the table (an article) can only be added if it has a title. We update the article.rb file:
```ruby
class Article < ApplicationRecord
  validates :title, presence: true
end
```
This change won't take effect until we reload the Rails Console. This can be done by exiting and restarting, or by:
```ruby
reload!
```
Now if an object with no title has a save attempt, it will result in the flag "false", of which details can be seen with:
```ruby
article.errors
```
And to see the full details of an error:
```ruby
article.errors.full_messages
```
### Validation further
Currently the validation would allow useless information such as just "a" or "b". This would corrupt our data within the table. We need to enforce minimum lengths for these properties.

We do that by adjusting the validates :title line in the article.rb file:
```ruby
validates :title, presence: true, length: ( minimum: 6, maximum: 100 )
```
I noted that the validation is not retroactive, that is, the validations do not effect existing table entries.
## Chpt 84 Show articles (route, action and view)
![](rails_front_back_ends.png)

For this lesson it is important to remember that the items covered here can be automatically generated in Rails. We are hand coding it to help our understanding.

So, showing an individual article the request goes to the routes.rb file where it will get the 'show' route, and then to the controller to get the 'show' action. Then the show action interacts with the database with the help of the model, and then send the information back to the controller who'll send it to the 'show' view.

### Config routes.rb

So first step is to create the show route in the config>routes.rb file.
Adding:
```ruby
resources :articles
````
will give all the routes we need to access the articles. In the terminal you can see all the routes expanded with:
```
rails routes --expanded
```  
For the lesson Mushrur just wants to focus on the 'show' action, and so changed the routes.rb file as:
```ruby
resources :articles, only: [:show]
```
### Config controller
Add new file "resources" for the new routing; new filename will be articles_controller.rb
```ruby
class ArticlesController < ApplicationController

end
```
It is easy to hand code, and follows the same format as the PagesController. If you try to go to localhost:3000/articles/1 then you'll now get the error that the action 'show' is missing. So now we build that in the controller we just created:
```ruby
class ArticlesController < ApplicationController
  def show

  end
end
```
First, there is no 'aricles' folder under views. So we need to add that folder first. Second, we add the show.html.erb page.

Now, that show.html.erb page is currently just static. We want to pull the appropriate article and show the details on this page. We do that by fleshing out the 'show' action in the ArticlesController.

The id of the article (which is the last part of the url) is passed in via the params hash: params (short for parameters), it's a hash data structure. The way we enter that is:
```ruby
params[:id]
```
However, if we def show as:
```ruby
def show
  article = Article.find(params[:id])
end
```
it won't work as the variable "article" is not carried to the pages view. To do that, we need to create an instanced variable.
### Create instanced variable
to create an instanced variable we just add '@' in front, i.e. @article.
```ruby
class ArticlesController < ApplicationController

  def show
    @article = Article.find(params[:id])
  end

end
```
Now that it is an instanced variable it is available in the 'show' view.
### Display instanced variable
To use Ruby code within the show html file we need to use embedded ruby tags.
```html
<p><strong>Title: <%= @article.title %> </strong></p>
<p><strong>Description: <%= @article.description %></strong></p>
```
Note, that without the '=' within the embedded ruby tag, the code would just be evaluated, it would not show. You need the '=' to show it.

We can run a debugger which is built in to Rails (gem = debug) by putting:
```ruby
class ArticlesController < ApplicationController

  def show
    debugger
    @article = Article.find(params[:id])
  end

end
```
Then when refreshing a webpage you can go step by step in the rails server terminal.

During the debugging you can type 'params' to see what parameters are being taken, and to can also be specific e.g. params[:id] will return the id of the article of the currently called page.

To get out of the debugging console type 'continue'.
## Chpt 85 Show articles feature - text references and code

You can find all the code added for the show feature for our articles resource here: https://github.com/udemyrailscourse/alpha-blog-6/commit/7304bca894202f78535b4abdc870d42f6a254967

Show actions are usually used to display individual items in a resource. For example:

- a specific article from an articles table

- a specific user's profile from a social media app

- details of a specific stock from a stocks table

- a specific recipe from a list of recipes

The steps are to -

1) Have a route for it

2) Have the corresponding controller/action that the route directs the request to

3) Have a corresponding view to display to the user who makes the request

The code details for each step are in the link provided at the beginning of this text resource. As a reminder: the red highlighted area are removals and the green highlighted area are additions.

## Chpt 86 Articles Index
Objective is to have the webpage home/articles, with a listing of all the articles available to view.

Request comes for a list of articles, it goes via routing to our listing controller (an index action). From this action we'll use the Article model which will interact with the database and grab a listing of all the article titles with an instance variable, and make it available to our index action in the controller. Then use a view and iterate through each article and list their title in the view. 
### build the route
Looking at
```
rails routes --expanded
```
We see that url for index is /articles and the controller#action is articles#index.

So in routes.rb we add :index to the resources line:
```ruby
  resources :articles, only: [:show, :index]
```
Then we need to add an index action to our articles_controller:

```ruby
  def index
  end
```
And then because we have an index action, we need to add an index view under views>articles> index.html.erb

Now we can see our Index page when we navigate to home/articles.

Now we need to add some code to our ArticlesController#index action such that we can list all our articles on the home/articles page.

We go back to our index action in the ArticlesController and:

```ruby
  def index 
    @articles = Article.all
  end
```
Then we go back to our index.html.erb and:

```html
<h1>Articles Index</h1>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Description</th>
      <th>Actions</th>
    </tr>
  </thead>


  <tbody>
    <% @articles.each do |article| %>
      <tr>
        <td><%= article.title %></td>
        <td><%= article.description %></td>
        <td>Placeholder</td>
      </tr>
    <% end %>
  </tbody>

</table>
```
## Chpt 88 Forms - Building New Article Creation Form
When we click on the create article form it will submitting a POST request, not a GET request.

Rails also builds an authentication token to ensure that the form is being submitted from our app and not from a malicious source.

"New" action will enable us to have the form, and "CREATE" action will work behind the scenes (so we won't need a view). So we need to have the "new" and "create" routes.

In our routes.rb file we amend it thus:
```ruby
  resources :articles, only: [:show, :index, :new, :create]
```
when we
```
rails routes --expanded
```
We can see the actions required for new and create, being articles#new and articles#create. so we need to build them in our ArticlesController.

Rails provides "form helpers" to ease the creation of forms https://guides.rubyonrails.org/form_helpers.html

form_with is good but note that it uses Ajax. We will modify it so it uses an HTML post request.

### Building the Form
There are several different ways to do the form, in this case we will start with the scope, which for us is "article", and then we specify the url where the form will be sent 'articles_path'. Then to post the form using standard http post instead of ajax. 

```html
<h1>Create A New Article</h1>

<%= form_with scope: :article, url: articles_path, local: true do |f| %>

  <p>
    <%= f.label :title %></br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :description %></br>
    <%= f.text_area :description %> 
  </p>

  <p>
    <%= f.submit %>

  </p>

<% end %>
```
Now the form is shown and you can interact with the submit button, but nothing is happening. We need to update the create action in the ArticlesController:

```ruby
  def create
    render plain: params[:article]
  end 
```
## Chpt 90 Create Action - Save newly created articles
Here we will change the create action from rendering the article in the screen, to saving the article in the database table. 

We need to pass in the params to the database and can't simply use the :article tag as it isn't whitelisted to use. We need to allow the top level key "article" and the keys underneath that of "title" and "description".

```ruby
  def create
    @article = Article.new(params.require(:article).permit(:title, :description))
  end 
```
### Adjustment from Text & Video
I could not save the article to the database following the instructions above. I then realized it was because in my version I had added an "author" field, and this field was required for any entry to the table to be valid. So I updated the applicable sections in the ArticleController, the form fields (in new.html.erb) and in the index and show views to include the 'Author' field.

### What happens after the creation?
It would be logically to go to the newly created articles 'show' page. 

We add the path within the controller:
```ruby
  def create
    @article = Article.new(params.require(:article).permit(:title, :description, :author))
    @article.save  
    redirect_to article_path(@article)
  end 
```
To get this redirect path, we look again at the rails routes --expanded, and the section for showing the new article. It shows that the path is "article", hence we put 'article_path', and we also need the :id, which is provided by putting (@article).

However, because this type of redirect is so commonly used, we can simply condense it to:
```ruby
redirect_to @article
```
## Chpt 92 Messaging - Validation and Flash Messages
We change the articles controller action under create to an if statement, such that if it doesn't save, then it renders a new form. We want the validation errors to show on this newly rendered form - and we put the code for that in the new.html.erb

```html
<h1>Create A New Article</h1>

<% if @article.errors.any? %>
  <h2>Article Could Not Be Saved</h2>
  <ul>
    <% @article.errors.full_messages.each do |msg| %>
      <li><% msg %></li>
  <% end %>
  </ul>
<% end %>

<%= form_with scope: :article, url: articles_path, local: true do |f| %>
```
However, the very first time we load this page we'll get an error as we don't have a @article defined. So we need to amend the 'new' method in the controller:
```ruby
  def new
    @article = Article.new
  end 
```
After I made the changes the error message didn't come up when I saved the form with all fields blank. After looking at the questions that had come up in the course, I found that this occurred for many people. It was solved with either:
```ruby
render :new, status: :unprocessable_entity
```
In the articles_controller.rb file, or with:
```html
<%= form_with scope: :article, url: articles_path, local: true do |f| %>
```
In the new.html.erb file.

However, then the bullet points were coming up (the black dots) but no text. After searches and comparisons with the work of others I realized I had simply missed an "="! I had <% msg %> instead of <%= msg %>.
### Using Flash to Show the Article has been Saved to the Database
Rails has a helpful "Flash Message". We add this to the create action in the article_controller.rb file. There are two common types of flash messages - notice & alert. Alert being when something goes wrong.
```ruby
    if @article.save  
      flash[:notice] = "Article was successfully created."
      redirect_to @article
```
This creates a flash key, and we need to then decide where to show the key (i.e. have the message show on the screen).

We put it in the application.html.erb file (under app>views>layouts), in the body tag, right above the yield. We use a key-value pair (can call it anything you like):
```html
  <body>
    <% flash.each do |name, msg| %>
      <%= msg %>
    <% end %>
    <%= yield %>
  </body>
``` 
## Chpt 94 Edit and Update Existing Articles
First, add the update and edit routes to routes.rb
```ruby
Rails.application.routes.draw do
  root 'pages#home'
  get 'about', to: 'pages#about'
  resources :articles, only: [:show, :index, :new, :create, :edit, :update]
end
```
Then we add an edit and an update method to our articles_controller.rb file.

Then add an edit.html.erb file under views>articles. Use the information from the "new" html file as a base, and adjust the form field (as we will be using an instance of the article variable as the model).

If we run the edit file we'll get a "NoMethodError in Articles#edit", as to properly display the edit form we need to instantiate the article being edited. Next step is to define this method in the controller. We can just copy the same code we used for the "show" action:
```ruby
  def edit
    @article = Article.find(params[:id])
  end
```
Now the article details appear in the edit form. The next step is to define the "update" action in the controller so that the updated article can be saved to the database table.

```ruby
 def update
    @article = Article.find(params[:id])
    if @article.update(params.require(:article).permit(:title, :description, :author))
      flash[:notice] = "Article was successfully updated."
      redirect_to @article 
    else
      render 'edit'
    end 
  end 
```
## Chpt 96 Delete Article
First we need to add destroy to our routes.rb file
```ruby
resources :articles, only: [:show, :index, :new, :create, :edit, :update]
```
However, adding destroy will result in all the default routes being in place, so we can delete the 'only' tag and be left with the default routes setting:
```ruby
resources :articles
```
by doing this we also expose all the restful routes for our articles resources. 

REST - Representational state transfer - mapping HTTP verbs (get, post, put/patch, delete) to CRUD actions. 

Resources provides REST-ful routes to Rails resources. Mapping all the front-end routes needed to handle requests coming in, and mapping them to applications. 

As per Rails routes, the URI is /articles/:id, and the Controller#action is articles#destroy.

The controller action is:
```ruby
  def destroy
    @article = Article.find(params[:id])
    @article.destroy 
    redirect_to articles_path 
  end 
```
However, we now need to consider how we get to the destroy option. We need to add a link in the "Action" column of our articles index. 
### Embedded Ruby html linking
The code template to use is: <%= link_to '[text to show]', '[path]' %>

So the code for the link in our index file for the specific article is:
```html
<td><%= link_to 'Delete', article_path(article) %></td>
```
Then, since this is the same path for "show", we need to indicate the method we want is delete, by:
```html 
<td><%= link_to 'Delete', article_path(article), method: :delete %></td>
```
By the way, the default method is 'show', so if you want that action you do not need to specify the method.

### Edit Article Link
Looking at the rails routes --expanded entry for editing an article, the prefix is 'edit_article'. Therefore the correct entry for the edit link in the index.html.erb file is:
```ruby
        <td><%= link_to 'Edit', edit_article_path(article) %></td>
```
## Chpt 98 User Interface - Layout Links
Changed the table column 'Action' to span the 3 columns with Show, Edit and Delete.
```html
<th colspan="3">Actions</th>
```
### Link on Articles Listing Page to Create a new Article
```html
<%= link_to 'Create New Article', new_article_path %>
```
Links on Individual Article Page:
```html
<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Delete', article_path(@article), method: :delete %> |
<%= link_to 'Return to Articles Listing', articles_path %>
```
### Add "confirmation action" when deleting
We add a confirmation by using some javascript: data: { confirm: "Are you sure?" }
```html
<%= link_to 'Delete', article_path(@article), method: :delete, data: { confirm: "Are you sure?" } %> 
```
So, the link to delete didn't work for either the articles page or the show page. When clicking delete it would just show the article. Looking on the ROR website questions, this issue has come up for several people. I implemented this and it worked from the articles page to delete, but not the show page:
```html
<td><%= link_to 'Delete', article_path(article), method: :delete, data: { "turbo-method": :delete, "turbo-confirm": "Are you sure?" } %></td>
```
When I try this on the 'show' page with:
```html
<%= link_to 'Delete', article_path(@article), method: :delete, data: { "turbo-method": :delete, "turbo-confirm": "Are you sure?" } %> 
```
(note that this page uses @article instead of article), and when I try to delete the article I get the confirmation message (do I really want to delete it) and on clicking Yes I get the error: 
![error](error1.png)

For some reason the pathway is following the "show" action instead of the "delete" action when running from the 'show' page.

I ensured Yarn was updated (as someone said this helped them), but no luck.

Then I found another person who had the same issue and asked the question about how to solve it. They did by adding "status: :see other' to the delete method in the controller as follows:
```ruby
  def destroy
    @article = Article.find(params[:id])
    @article.destroy 
    redirect_to articles_path, status: :see_other
  end 
```
### Heroku Database
After the last change I loaded changes to Heroku via Git, then tried to run the app from the heroku web address but it didn't work. There was no detail in the error message other than something went wrong and to check the logs. By accident I found a comment to ensure that the database was migrated, so I tried it:
```
heroku run rails db:migrate
```
And after this it worked! Although the database table started empty on Heroku, i.e. without any populated rows. But I can add rows fine, Edit etc.
## Chpt 100 DRY (Don't Repeat Yourself) - code refactoring & partials
The line:
```ruby
@article = Article.find(params[:id])
```
Exists in multiple places in articles_controller.rb. So we'll extract it by using it as a method.

We start with 'private' to indicate it is only used in this file. Then we make this method:
```ruby
private

  def set_article
    @article = Article.find(params[:id])
  end
```
Note that private doesn't require an "end".

Then at the top of the file we add "before_action :set_article". What it does is perform that action before any of the methods. However, we don't want it done for all the methods. We just want it for the show, edit, update and destroy actions.
```ruby
class ArticlesController < ApplicationController
  before_action :set_article, only: [:show, :edit, :update, :destroy]
```
Another code repeat in that file in both create and update is:
```ruby
params.require(:article).permit(:title, :description, :author)
```
Note about PRIVATE
It is important to remember:
-private isn't a method, so don't put an "end" for it
-don't put any other methods under it, as they won't be usable by any other files in your app! i.e. they are only available for that specific controller.
### Views
The 'form' code for both new and edit html files are just about identical. We can clean this up by developing a "partial".

To start, let's practice with the 'flash message' code in application.html.erb. Let's cut the code:
```html
    <% flash.each do |name, msg| %>
      <%= msg %>
    <% end %>
```
and paste it into a partial. Create a new file in the same folder, and start it with an underscore. Rails will then know this is a partial. Then we go back to the application.html.erb file and where we copied the code we put this code in its place:
```html
<%= render 'layouts/messages'%>
```
#### Let's create the partial for "new" & "edit"
Cut the entire form from edit and paste it into a new file in the same folder, calling it _form.html.erb

Then in place of the form in the edit file, put:
```html
<%= render 'form' %>
```
Do the same for the create form file.
## Chpt 102 Production Deploy to Heroku
Steps we followed:

### verify Gemfile

Issue the following command in the terminal 
```bash
bundle install --without production
```

Make a commit of code

```bash
git add -A
git commit -m "helpful message depending on what you are committing to your repo"
```
To deploy to heroku:
```bash
git push heroku main
```
To push to GitHub repo:
```bash
git push origin main
```
Since we now have a db component to our application with the articles table, we will need to run migrations in production so the production articles table is created. To run migrations at heroku, you can use the following command:
```bash
heroku run rails db:migrate
```
You can preview your production app by issuing the following command from the terminal:
```bash 
heroku open
```
or,

You can directly pull up a browser window and paste in the name of your application. It'll take the following format:

https://yourappname.herokuapp.com
# Section 5 STYLING
## Introduction
To style our app we are going to use [Bootstrap](https://getbootstrap.com). Some alternatives to Bootstrap are [Semantic UI](https://semantic-ui.com) and [Materialize](https://materializecss.com) (pushed forward by Google).

Prerequisites: 
1. Understanding of HTML and CSS
2. Idea of what you want for your home page

For the first prerequisite, a nice website to refresh your html and css skills is [Shay Howe's Website](https://learn.shayhowe.com/html-css/).

For the second you should build a mock-up. Mushrur uses [Balsamiq](balsamiq.com). 
## Chpt 106 Install Bootstrap on Rails
This looks at installing Bootstrap (5) on Rails 7. Mashrur covers installation onto Rails 5 & 6.

On initial searching, it seems that the easiest method is to install bootstrap at the same time you make a new rails app. Since alpha-blog is already created, this will try and install to an existing project.

This website https://www.bootrails.com/blog/rails-7-bootstrap-5-tutorial/ has as pre-requisites 
``` 
$> ruby -v  
ruby 3.0.0p0 // you need at least version 3 here  
$> bundle -v  
Bundler version 2.2.11  
$> npm -v  
8.3.0 // you need at least version 7.1 here  
$> yarn -v  
1.22.10
$> psql --version  
psql (PostgreSQL) 13.1 // let's use a production-ready database locally  
```
It seems unusual to me as I already mentioned above that I have npm installed for managing NodeJS, and Yarn also does that. Yet this site says you should have both?

First, I think I should sync with Github version. In the directory:
```
git init
```
Then I decided that doing it may cause new problems. Instead I'll proceed with installing Bootstrap.

This comes up in the first page of a web search https://www.uday.net/add-bootstrap-5-to-an-existing-Rails-7-app, but it didn't give me confidence.

Then I found a GoRails [Youtube](https://www.youtube.com/watch?v=EzCl-6etSGI). It was really quick, and the guy just pasted in the Bootstrap CDN link into the application.html.erb file head:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>AlphaBlog</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-pprn3073KE6tl6bjs2QrFaJGz5/SUsLqktiwsUTF55Jfv3qYSDhgCecCxMW52nD2" crossorigin="anonymous"></script>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
    <%= javascript_importmap_tags %>
  </head>

  <body>
    <%= render 'layouts/messages' %>
    <%= yield %>
  </body>
</html>
```
It seems like the functionality for this may be different than that explained by Mashrur where they install Bootstrap gems along with other things into Rails, and don't rely on the CDN. I will install the nav bar CDN into the alpha-blog to see if all Javascript functionality is present with simply copying the CDN links into the application file.

### Nav Bar Test
When I pasted in the Nav Bar code from Bootstrap into the application.html.erb file, it worked right away in my app. The drop-down menus - which rely on Javascript - also worked right away. So it seems using CDN is useful and functional.

### GoRails
For the Nav Bar Test I followed along with the [GoRails](https://www.youtube.com/watch?v=Hj_h2v36e1M) tutorial, and I have to say that it is really easy to follow. They do it a bit different than Mashrur, by adding the Nav bar via partial, which I feel is a great way to do it. They also explain how you can do the links with either html, or ruby - with ruby being preferred since html is hardcoded. 

The explanation regarding using ruby helper instead of html code is wonderful, and even explain how to add in class styling from Bootstrap. The two methods below are equivalent - the first in html and the second in assisted ruby:
```html
  <a class="nav-link" href="/about">About Me</a>
  <%= link_to "About Me", about_path, class: "nav-link" %>
```
I had a look at their website, and found they [have a video](https://gorails.com/episodes/bootstrap-css-bundling-rails?autoplay=1) there on how to install css and JavaScript with Rails. 

### Installing Yarn via npm
https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable
```
npm install --global yarn
```
Check with
```
yarn --version
```
### Sync with GIT
I then did sync with Git, following the directions here http://www.deanbodenham.com/learn/using-git-to-sync-different-computers.html.

So I reverted back to the alpha-blog version before I started upgrading to Bootstrap. I did this as I found out above how I could do it using the CDN copied into the application file, and now want to try installing the Bootstrap gem (CSS and Javascript).
### Install Bootstrap
Then I started to do the update, using the instructions on [Github](https://github.com/rails/cssbundling-rails). At the time of writing this (June 10 2022), the instructions are:

  You must already have node and yarn installed on your system. You will also need npx version 7.1.0 or later. Then:

  Run ./bin/bundle add cssbundling-rails
  Run ./bin/rails css:install:[tailwind|bootstrap|bulma|postcss|sass]
  Or, in Rails 7+, you can preconfigure your new application to use a specific bundler with rails new myapp --css [tailwind|bootstrap|bulma|postcss|sass].

#### Updating npx
I checked my version of npx:
```
npx --version
6.14.4
```
So I needed to update npx first to "npx version 7.1.0 or later". This [website](https://kenanbek.medium.com/how-to-upgrade-nvm-npm-node-and-npx-97f927dddd22) had instructions on how to update npx, being first you must update npm:
```
sudo npm install -g npm@latest
```
But this threw up errors:
```
npm WARN notsup Unsupported engine for npm@8.12.1: wanted: {"node":"^12.13.0 || ^14.15.0 || >=16"} (current: {"node":"10.19.0","npm":"6.14.4"})
npm WARN notsup Not compatible with your version of node/npm: npm@8.12.1
```
However, in that website's instructions to update node, npm had to first be at the latest version! Circular reference much!

How to fix this? In the website, the first step was to update nvm, so maybe I could try that.
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
And I got another error:
```
ERROR: npm is known not to run on Node.js v10.19.0
You'll need to upgrade to a newer Node.js version in order to use this
version of npm. You can find the latest version at https://nodejs.org/
```
So, off to https://nodejs.org I went, and found that the latest version is 18.3.0. Downloaded the tar.xz file and then looked up how to install it on Linux Mint. The instructions I [found](https://www.codegrepper.com/code-examples/shell/how+to+install+node.tar.xz+in+ubuntu) were:
```
tar xf [filename]

This will expand the contents of the file to a folder. Then the commands are, from the folder:

./configure

make

sudo make install
```
But of course when I try the second step I get:
```
./configure
bash: ./configure: No such file or directory
```
So frustrating. I do some more searching on how to install from a xz file. I find the following instructions [here](https://www.codegrepper.com/code-examples/shell/how+to+install+node.tar.xz+in+ubuntu)
```
sudo cp -r node-v18.3.0-linux-x64/{bin,include,lib,share} /usr/
```
I got no errors coming up, and I get success on checking the version:
```
node --version
v18.3.0
```
So now that node is the latest version, I try to install the latest npm version again:
```
sudo npm install -g npm@latest
```
And this time no errors. It also must have updated my npx, as now when I look at the version it is above 7.1.0!.
```
npx --version
8.11.0
```
### Back to installing Bootstrap
```
./bin/bundle add cssbundling-rails
```
I did this from my project folder, and got several pages of text returned in the console. I have no idea if it was successful or not. Hoping that it was, I proceed with the final step:
```
./bin/rails css:install:bootstrap
```
And of course I got an error:
```
./bin/rails css:install:bootstrap
rails aborted!
Don't know how to build task 'css:install:' (See the list of available tasks with `rails --tasks`)
```
So, going back to the pages of text, I noted right at the top it said:
```
#<NameError: uninitialized constant Gem::Source
```
Googling that error, I [found](https://stackoverflow.com/questions/15060011/nameerror-uninitialized-constant-gemsourceindex) the advice to:
```
gem update bundle && gem update --system
```
This returned the message that it was updated successfully, so I returned to run:
```
./bin/bundle add cssbundling-rails
```
This time I had success!
```
Fetching cssbundling-rails 1.1.0
Installing cssbundling-rails 1.1.0
```
So then the next step:
```
./bin/rails css:install:bootstrap
```
Lots of text, some of it red, and warnings:
```
./bin/rails css:install:bootstrap
Build into app/assets/builds
      create  app/assets/builds
      create  app/assets/builds/.keep
      append  app/assets/config/manifest.js
Stop linking stylesheets automatically
        gsub  app/assets/config/manifest.js
      append  .gitignore
      append  .gitignore
Remove app/assets/stylesheets/application.css so build output can take over
      remove  app/assets/stylesheets/application.css
Add stylesheet link tag in application layout
File unchanged! The supplied flag value not found!  app/views/layouts/application.html.erb
Add default Procfile.dev
      create  Procfile.dev
Ensure foreman is installed
         run  gem install foreman from "."
Fetching foreman-0.87.2.gem
Successfully installed foreman-0.87.2
1 gem installed
Add bin/dev to start foreman
      create  bin/dev
Install Bootstrap with Bootstrap Icons and Popperjs/core
      create  app/assets/stylesheets/application.bootstrap.scss
         run  yarn add sass bootstrap bootstrap-icons @popperjs/core from "."
yarn add v1.22.19
warning package.json: No license field
warning alpha-blog: No license field
[1/4] Resolving packages...
[2/4] Fetching packages...
[3/4] Linking dependencies...
[4/4] Building fresh packages...
success Saved lockfile.
warning alpha-blog: No license field
success Saved 20 new dependencies.
info Direct dependencies
├─ @popperjs/core@2.11.5
├─ bootstrap-icons@1.8.3
├─ bootstrap@5.1.3
└─ sass@1.52.3
info All dependencies
├─ @popperjs/core@2.11.5
├─ anymatch@3.1.2
├─ binary-extensions@2.2.0
├─ bootstrap-icons@1.8.3
├─ bootstrap@5.1.3
├─ braces@3.0.2
├─ chokidar@3.5.3
├─ fill-range@7.0.1
├─ glob-parent@5.1.2
├─ immutable@4.1.0
├─ is-binary-path@2.1.0
├─ is-extglob@2.1.1
├─ is-glob@4.0.3
├─ is-number@7.0.0
├─ normalize-path@3.0.0
├─ picomatch@2.3.1
├─ readdirp@3.6.0
├─ sass@1.52.3
├─ source-map-js@1.0.2
└─ to-regex-range@5.0.1
Done in 4.97s.
      insert  config/initializers/assets.rb
Appending Bootstrap JavaScript import to default entry point
      append  app/javascript/application.js
Add build:css script
         run  npm set-script build:css "sass ./app/assets/stylesheets/application.bootstrap.scss ./app/assets/builds/application.css --no-source-map --load-path=node_modules" from "."
npm WARN set-script set-script is deprecated, use `npm pkg set scripts.scriptname="cmd" instead.
         run  yarn build:css from "."
yarn run v1.22.19
warning package.json: No license field
$ sass ./app/assets/stylesheets/application.bootstrap.scss ./app/assets/builds/application.css --no-source-map --load-path=node_modules
Done in 2.46s.
```
So the red text was "File unchanged! The supplied flag value not found!  app/views/layouts/application.html.erb". The application file exists so I'm not sure what the "supplied flag" is meant to mean.

Not sure if the warnings broke it either?
```
warning package.json: No license field
warning alpha-blog: No license field
npm WARN set-script set-script is deprecated, use `npm pkg set scripts.scriptname="cmd" instead.
```












