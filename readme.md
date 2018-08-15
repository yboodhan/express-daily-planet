# Making Headlines - Daily Planet

![Daily Planet](http://blogs.smithsonianmag.com/design/files/2013/06/first-daily-planet1.jpg)

Welcome to the Daily Planet. We need your superhuman developer skills to help us share news with the world. We've seen that you have some Express knowledge and need you to make us a MVP website as soon as possible.

You'll need to hook your server up to a database to create, store and display articles.

## NOTE!

You may have done another version of this assignment for forming CRUD routes without a database. If so, feel free to use that as your starter code! In this case, our goal is to alter it to use a real SQL database instead of storing data in a JSON file. Delete the models folder and references to it, and we'll replace them with Sequelize.

If you did not do a previous version of this assignment, start from scratch following the directions from the class lesson.

## Getting Started


#### Setting up the Server (from existing code)

If you have a previous version of this assignment:

* Delete the models folder
* Set up Sequelize
  * The `sequelize init` command. This sets up a config.json file.
  * Set up your config file as appropriate - change the database name, credentials, and SQL flavor.
  * Create a database for this app to use on your local machine
  * Don't create your tables with raw SQL. Instead use the `sequelize model:create` command. Remember to make the names singular and lower case!
  * Remember that even though you've created the models, the tables don't actually get created until you run `sequelize db:migrate`!
* Replace the old references to the JSON file with actual Sequelize commands to read/write to the database

#### Setting up the Server (if starting from scratch)

To get going we need to set up a basic Express server (see today's notes for
full details).

* Fork/clone this repository
* Run `npm init` in the directory
* Install express, ejs, body-parser, express-ejs-layouts, pg, pg-hstore via npm
* Create an index.js file
* Setup a basic Express server with a root route

Use this for your basic root route just to make sure it is working.

```js
app.get('/', function(req, res) {
  res.send('HELLO TACO!!!');
});
```

At this point you should be able to run `nodemon` and then go to `http://localhost:3000` and see "HELLO TACO!!!".

## Requirements

#### Create a home page with a view

* Create a views folder
* Create a file for your home page: `index.ejs`
* Add HTML to the file created above
* Render the index page on your root route
  * Don't forget to set up your EJS view engine

Change your root route to render your home page (index.ejs)

```js
app.get('/', function(req, res) {
  res.render('index.ejs');
});
```

**STOP** At this point we should be able to go to `localhost:3000` and see an html page that is the result of the contents of what is in `index.ejs`. If you'd like, feel free to use partials for parts of this page.

#### Data setup

We'll store all the articles in Postgres. Use Sequelize to create a model
representing an article. Articles should have a `title` property and a `body`
property.

Reference course notes on [Sequelize](https://wdi_sea.gitbooks.io/notes/content/05-express/express-sequelize/readme.html)

#### Routes
You'll need to create the following `articles` routes. Notice: you won't need
to create routes to update or delete articles at this time.

Here's the class notes on implementing basic [CRUD in Express](https://wdi_sea.gitbooks.io/notes/content/05-express/express-intro/05crudexpress.html)

* `GET /`
  * view: `views/index.ejs`
  * purpose: Serve the homepage of your site.
* `GET /articles`
  * view: `views/articles/index.ejs`
  * purpose: displays a list of all articles
* `GET /articles/new`
  * view: `views/articles/new.ejs`
  * purpose: displays a form that users use to create a new article
* `POST /articles`
  * view: none (redirects to /articles after the article is created)
  * purpose: creates a new article (adds to articles array and saves the file)
* `GET /articles/:id`
  * view: `views/articles/show.ejs`
  * purpose: find an article by id in the array of `articles` and display it.

#### Static Pages
Create the following routes for static pages. You can use EJS with these pages, but you won't be passing any data.

* `GET /about` serve a static about daily planet page.
* `GET /contact` serve a static contact page.

#### Structure

Your EJS views should be organized using folders. Here is an example.
Use the `express-ejs-layouts` module so the main structure of your site
appears in only one file, the `layout.ejs` file.

```
- express-daily-planet
  - views
    - layout.ejs
    - articles
      - index.ejs
      - new.ejs
      - show.ejs
    - site
      - home.ejs
      - about.ejs
      - contact.ejs
```

#### Styling (Bootstrap, Materialize, etc.)

Style the page and include a navigation bar to help the user navigate the site.
Note that this is a news site, so style accordingly. Put the navbar in your
`layout.ejs` file to it appears everywhere easily!

##### What about static files, like CSS and front-end JS?

We'll need to set up a folder for serving up static files. Usually by convention, this will be a folder in your root directory called either `public` or `static`. Aside from that, you will need a small bit of code to let Express know where to look for those files. Don't worry - it's fairly straight-forward! Check out [Express documentation](http://expressjs.com/starter/static-files.html) for a useful resource.

## Bonus Ideas

* Create a DELETE route for removing articles
* Create a PUT route for editing articles
* Create a search form (can be on home page or articles index)
* Accept `q` query string on your articles route `/articles?q=search+term`
    * find how to access the query string from the request (Hint: the query isn't in `req.params`)
    * displays list of articles filtered by search term
    * ensure the route still works without a query string (displays all articles)
* There's no magic back-end solution to filtering! Use what you know about setting up routes, figure out how to access the query string and use regular JavaScript logic and array manipulation to build up an array of results.


---

## Licensing
1. All content is licensed under a CC-BY-NC-SA 4.0 license.
2. All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.
