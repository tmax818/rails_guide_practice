# Getting Started with Rails

## 1 Guide Assumptions
This guide is designed for beginners who want to get started with a Rails application from scratch. It does not assume that you have any prior experience with Rails.

Rails is a web application framework running on the Ruby programming language. If you have no prior experience with Ruby, you will find a very steep learning curve diving straight into Rails. There are several curated lists of online resources for learning Ruby:

- [Official Ruby Programming Language website](https://www.ruby-lang.org/en/documentation/)  
- [List of Free Programming Books](https://github.com/vhf/free-programming-books/blob/master/free-programming-books.md#ruby)

Be aware that some resources, while still excellent, cover versions of Ruby as old as 1.6, and commonly 1.8, and will not include some syntax that you will see in day-to-day development with Rails.

## 2 What is Rails?
Rails is a web application development framework written in the Ruby programming language. It is designed to make programming web applications easier by making assumptions about what every developer needs to get started. It allows you to write less code while accomplishing more than many other languages and frameworks. Experienced Rails developers also report that it makes web application development more fun.

Rails is opinionated software. It makes the assumption that there is a "best" way to do things, and it's designed to encourage that way - and in some cases to discourage alternatives. If you learn "The Rails Way" you'll probably discover a tremendous increase in productivity. If you persist in bringing old habits from other languages to your Rails development, and trying to use patterns you learned elsewhere, you may have a less happy experience.

The Rails philosophy includes two major guiding principles:

- Don't Repeat Yourself: DRY is a principle of software development which states that "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system." By not writing the same information over and over again, our code is more maintainable, more extensible, and less buggy.  
- Convention Over Configuration: Rails has opinions about the best way to do many things in a web application, and defaults to this set of conventions, rather than require that you specify minutiae through endless configuration files.

### 3 Creating a New Rails Project
The best way to read this guide is to follow it step by step. All steps are essential to run this example application and no additional code or steps are needed.

By following along with this guide, you'll create a Rails project called blog, a (very) simple weblog. Before you can start building the application, you need to make sure that you have Rails itself installed.

>The examples below use $ to represent your terminal prompt in a UNIX-like >OS, though it may have been customized to appear differently. If you are >using Windows, your prompt will look something like `c:\source_code>`

#### 3.2 Creating the Blog Application
Rails comes with a number of scripts called generators that are designed to make your development life easier by creating everything that's necessary to start working on a particular task. One of these is the new application generator, which will provide you with the foundation of a fresh Rails application so that you don't have to write it yourself.

To use this generator, open a terminal, navigate to a directory where you have rights to create files, and type:

```
$ rails new blog
```

This will create a Rails application called Blog in a `blog` directory and install the gem dependencies that are already mentioned in `Gemfile` using `bundle install`.

```
$ cd blog
```

The blog directory has a number of auto-generated files and folders that make up the structure of a Rails application. Most of the work in this tutorial will happen in the app folder, but here's a basic rundown on the function of each of the files and folders that Rails created by default:



| File/Folder | Purpose     |
|-----------|---------------|
| app/   | Contains the controllers, models, views, helpers, mailers, channels, jobs and assets for your application. You'll focus on this folder for the remainder of this guide.  |
| bin/   | Contains the rails script that starts your app and can contain other scripts you use to setup, update, deploy or run your application.    |
| config/ | Configure your application's routes, database, and more. This is covered in more detail in [Configuring Rails Applications.](http://guides.rubyonrails.org/configuring.html)    |
| config.ru | Rack configuration for Rack based servers used to start the application. For more information about Rack, see the [Rack website](https://rack.github.io/).                |
| db/     | Contains your current database schema, as well as the database migrations.     |
| Gemfile Gemfile.lock | These files allow you to specify what gem dependencies are needed for your Rails application. These files are used by the Bundler gem. For more information about Bundler, see the [Bundler website].   |
| lib/   | Extended modules for your application.       |
| log/  | Application log files.     |
| package.json | This file allows you to specify what npm dependencies are needed for your Rails application. This file is used by Yarn. For more information about Yarn, see the [Yarn website.]  |
| public/    | public/	The only folder seen by the world as-is. Contains static files and compiled assets.     |
| Rakefile    | This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing Rakefile, you should add your own tasks by adding files to the lib/tasks directory of your application. |
| README.md    | This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on. |
| test/      | Unit tests, fixtures, and other test apparatus. These are covered in [Testing Rails Applications.](http://guides.rubyonrails.org/testing.html)   |
| tmp/       | Temporary files (like cache and pid files).   |
| vendor/      | A place for all third-party code. In a typical Rails application this includes vendored gems.  |
| .gitignore    | This file tells git which files (or patterns) it should ignore. [See GitHub - Ignoring files](https://help.github.com/articles/ignoring-files) for more info about ignoring files.  |
| .ruby-version   | This file contains the default Ruby version.  |

### 4 Hello, Rails!
To begin with, let's get some text up on screen quickly. To do this, you need to get your Rails application server running.

#### 4.1 Starting up the Web Server
You actually have a functional Rails application already. To see it, you need to start a web server on your development machine. You can do this by running the following in the blog directory:

```
$ bin/rails server
```

This will fire up Puma, a web server distributed with Rails by default. To see your application in action, open a browser window and navigate to http://localhost:3000. You should see the Rails default information page:

![image](http://guides.rubyonrails.org/images/getting_started/rails_welcome.png)

The "Welcome aboard" page is the smoke test for a new Rails application: it makes sure that you have your software configured correctly enough to serve a page.

#### 4.2 Say "Hello", Rails
To get Rails saying "Hello", you need to create at minimum a controller and a view.

A controller's purpose is to receive specific requests for the application. Routing decides which controller receives which requests. Often, there is more than one route to each controller, and different routes can be served by different actions. Each action's purpose is to collect information to provide it to a view.

A view's purpose is to display this information in a human readable format. An important distinction to make is that it is the controller, not the view, where information is collected. The view should just display that information. By default, view templates are written in a language called eRuby (Embedded Ruby) which is processed by the request cycle in Rails before being sent to the user.

To create a new controller, you will need to run the "controller" generator and tell it you want a controller called "Welcome" with an action called "index", just like this:
```
$ bin/rails generate controller Welcome index
```
Rails will create several files and a route for you.
```
create  app/controllers/welcome_controller.rb
 route  get 'welcome/index'
invoke  erb
create  app/views/welcome
create  app/views/welcome/index.html.erb
invoke  test_unit
create  test/controllers/welcome_controller_test.rb
invoke  helper
create  app/helpers/welcome_helper.rb
invoke  test_unit
invoke  assets
invoke  coffee
create  app/assets/javascripts/welcome.coffee
invoke  scss
create  app/assets/stylesheets/welcome.scss
```
Most important of these are of course the controller, located at app/controllers/welcome_controller.rb and the view, located at app/views/welcome/index.html.erb.

Open the app/views/welcome/index.html.erb file in your text editor. Delete all of the existing code in the file, and replace it with the following single line of code:

```
<h1>Hello, Rails!</h1>
```

#### 4.3 Setting the Application Home Page
Now that we have made the controller and view, we need to tell Rails when we want "Hello, Rails!" to show up. In our case, we want it to show up when we navigate to the root URL of our site, http://localhost:3000. At the moment, "Welcome aboard" is occupying that spot.

Next, you have to tell Rails where your actual home page is located.

Open the file `config/routes.rb` in your editor.
```
Rails.application.routes.draw do
  get 'welcome/index'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```
This is your application's routing file which holds entries in a special DSL (domain-specific language) that tells Rails how to connect incoming requests to controllers and actions. Edit this file by adding the line of code root 'welcome#index'. It should look something like the following:

```
Rails.application.routes.draw do
  get 'welcome/index'

  root 'welcome#index'
end
```

`root 'welcome#index'` tells Rails to map requests to the root of the application to the welcome controller's index action and `get 'welcome/index'` tells Rails to map requests to http://localhost:3000/welcome/index to the welcome controller's index action. This was created earlier when you ran the controller generator (`bin/rails generate controller Welcome index`).

Launch the web server again if you stopped it to generate the controller (`bin/rails server`) and navigate to http://localhost:3000 in your browser. You'll see the "Hello, Rails!" message you put into `app/views/welcome/index.html.erb`, indicating that this new route is indeed going to `WelcomeController`'s index action and is rendering the view correctly.

>For more information about routing, refer to [Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html).

### 5 Getting Up and Running
Now that you've seen how to create a controller, an action and a view, let's create something with a bit more substance.

In the Blog application, you will now create a new resource. A resource is the term used for a collection of similar objects, such as articles, people or animals. You can create, read, update and destroy items for a resource and these operations are referred to as CRUD operations.

Rails provides a resources method which can be used to declare a standard REST resource. You need to add the article resource to the `config/routes.rb` so the file will look as follows:
```
Rails.application.routes.draw do
  get 'welcome/index'

  resources :articles

  root 'welcome#index'
end
```
If you run bin/rails routes, you'll see that it has defined routes for all the standard RESTful actions. The meaning of the prefix column (and other columns) will be seen later, but for now notice that Rails has inferred the singular form article and makes meaningful use of the distinction.

```
$ bin/rails routes
       Prefix Verb   URI Pattern                  Controller#Action
welcome_index GET    /welcome/index(.:format)     welcome#index
     articles GET    /articles(.:format)          articles#index
              POST   /articles(.:format)          articles#create
  new_article GET    /articles/new(.:format)      articles#new
 edit_article GET    /articles/:id/edit(.:format) articles#edit
      article GET    /articles/:id(.:format)      articles#show
              PATCH  /articles/:id(.:format)      articles#update
              PUT    /articles/:id(.:format)      articles#update
              DELETE /articles/:id(.:format)      articles#destroy
         root GET    /                            welcome#index
```

In the next section, you will add the ability to create new articles in your application and be able to view them. This is the "C" and the "R" from CRUD: create and read. The form for doing this will look like this:

![image](http://guides.rubyonrails.org/images/getting_started/new_article.png)

It will look a little basic for now, but that's ok. We'll look at improving the styling for it afterwards.

### 5.1 Laying down the groundwork
Firstly, you need a place within the application to create a new article. A great place for that would be at /articles/new. With the route already defined, requests can now be made to /articles/new in the application. Navigate to http://localhost:3000/articles/new and you'll see a routing error:

![image](http://guides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

This error occurs because the route needs to have a controller defined in order to serve the request. The solution to this particular problem is simple: create a controller called `ArticlesController`. You can do this by running this command:
```
$ bin/rails generate controller Articles
```

If you open up the newly generated app/controllers/articles_controller.rb you'll see a fairly empty controller:
```
class ArticlesController < ApplicationController
end
```

A controller is simply a class that is defined to inherit from `ApplicationController`. It's inside this class that you'll define methods that will become the actions for this controller. These actions will perform CRUD operations on the articles within our system.

There are public, private and protected methods in Ruby, but only public methods can be actions for controllers. For more details check out [Programming Ruby](http://www.ruby-doc.org/docs/ProgrammingRuby/).

If you refresh http://localhost:3000/articles/new now, you'll get a new error:

![image](http://guides.rubyonrails.org/images/getting_started/unknown_action_new_for_articles.png)

This error indicates that Rails cannot find the new action inside the `ArticlesController` that you just generated. This is because when controllers are generated in Rails they are empty by default, unless you tell it your desired actions during the generation process.

To manually define an action inside a controller, all you need to do is to define a new method inside the controller. Open app/controllers/articles_controller.rb and inside the `ArticlesController` class, define the new method so that your controller now looks like this:

```
class ArticlesController < ApplicationController
  def new
  end
end
```
With the new method defined in ArticlesController, if you refresh http://localhost:3000/articles/new you'll see another error:

![image](http://guides.rubyonrails.org/images/getting_started/template_is_missing_articles_new.png)

You're getting this error now because Rails expects plain actions like this one to have views associated with them to display their information. With no view available, Rails will raise an exception.

Let's look at the full error message again:

> ArticlesController#new is missing a template for this request format and variant. request.formats: ["text/html"] request.variant: [] NOTE! For XHR/Ajax or API requests, this action would normally respond with 204 No Content: an empty white screen. Since you're loading it in a web browser, we assume that you expected to actually render a template, not… nothing, so we're showing an error to be extra-clear. If you expect 204 No Content, carry on. That's what you'll get from an XHR or API request. Give it a shot.

That's quite a lot of text! Let's quickly go through and understand what each part of it means.

The first part identifies which template is missing. In this case, it's the articles/new template. Rails will first look for this template. If not found, then it will attempt to load a template called application/new. It looks for one here because the ArticlesController inherits from ApplicationController.

The next part of the message contains request.formats which specifies the format of template to be served in response. It is set to text/html as we requested this page via browser, so Rails is looking for an HTML template. request.variant specifies what kind of physical devices would be served by the response and helps Rails determine which template to use in the response. It is empty because no information has been provided.

The simplest template that would work in this case would be one located at app/views/articles/new.html.erb. The extension of this file name is important: the first extension is the format of the template, and the second extension is the handler that will be used to render the template. Rails is attempting to find a template called articles/new within app/views for the application. The format for this template can only be html and the default handler for HTML is erb. Rails uses other handlers for other formats. builder handler is used to build XML templates and coffee handler uses CoffeeScript to build JavaScript templates. Since you want to create a new HTML form, you will be using the ERB language which is designed to embed Ruby in HTML.

Therefore the file should be called articles/new.html.erb and needs to be located inside the app/views directory of the application.

Go ahead now and create a new file at app/views/articles/new.html.erb and write this content in it:
```
<h1>New Article</h1>
```

When you refresh http://localhost:3000/articles/new you'll now see that the page has a title. The route, controller, action and view are now working harmoniously! It's time to create the form for a new article.
