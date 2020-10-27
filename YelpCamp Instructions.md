#Things I need to do for YelpCamp:
Video 1
##Initialising the project
* Add Landing Page
* Add Campgrounds Page that lists all campgrounds
Each campground has:
* Name
* Image


1. Initialise the project
    npm init
2. Install express and ejs in to your project and saves the dependencies to the JSON file
    npm install express ejs --save
3. Create your app.js
4. Require express in to your app.js file:
    var express = require("express");
5. Setup the port listening:    
    app.listen(3000, function(){
       console.log("The YelpCamp server has started");
   });
This allows you to see your project from the Project menu after selecting Run/URL thing.
   6. Create the index route:
    app.get("/", function(req, res) {
       res.send("This will be the landing page");
   });
   7. Run the applications via the console to test the index route and server are all working:
    node app.js
   8. Create a views folder
    mkdir views
   9. Create a landing page file
    touch views/landing.ejs
   10. Add content to landing.ejs
    goorm views/landing.ejs
   11. Set the view engine for ejs files in the app.js file:
    app.set("view engine", "ejs");
   12. Restart the server to see changes made:
    node app.js
   13. Create a campsites route:
    app.get("/campgrounds", function(req, res) {
   });
   14. Add an array of campsites to this route
    app.get("/campgrounds", function(req, res) {
       var campgrounds = [
           {
               name: "Salmon Creek",
                  image: "img url"
           },
              {
                  name: "Banjo Spring",
                  image: "img url"
              },
              {
                  name: "The Upsidedown",
                  image: "img url"
              },
       ]
   });
   15. Add a line to render the page when the server is loaded after the array:
    app.get("/campgrounds", function(req, res) {
       var campgrounds = [];
       res.render("campgrounds");
   });
   16. Create the campgrounds page in the views folder:
    touch views/campgrounds.ejs
   17. Open the file and add content:
    goorm views/campgrounds.ejs
   18. Restart the server and see if the page exists by going to /campgrounds:
    url/campgrounds
   19. In landing.ejs add a anchor tag with a link to the campgrounds page:
    <a href="/campgrounds">View all campgrounds</a>
   20. Restart the server and see if the link exists at the index page:
    url/
   21. Under the /campgrounds route in app.js pass the data of the campsites through:
    res.render("campgrounds", {campgrounds: campgrounds});
   22. In campgrounds.ejs display the data that has been passed:
    <%= campgrounds %>
   23. Restart the server and check /campgrounds for objects appearing
   24. In campgrounds.ejs create a forEach that displays all campground names:
    <% campgrounds.forEach(function(campground){ %>
       <li>
           <%= campground.name %>
       </li>
   <% }); %>
   25. Restart the server and check the campgrounds page for campground names
   26. Change the loop to include images:
    <% campgrounds.forEach(function(campground){ %>
       <div>
           <h4>
               <%= campground.name %>
           </h4>
           <img src="<%= campground.image %>">
       </div>
   <% }); %>
   27. Restart server and refresh campgrounds page to see images


Video 2
##Layout and Basic Styling
      * Create our header and footer partials
    <%- include("partials/header") %>
    <%- include("partials/footer") %>
      * Add in Bootstrap


      1. In the views directory create a new directory called partials:
   Mkdir views/partials
      2. Add a header and footer file in to the partials directory:
   touch views/partials/header.ejs
   touch views/partials/footer.ejs
      3. Open header.ejs
   Goorm views/partials/header.ejs
      4. Add the HTML boilerplate to the header file:
   <!DOCTYPE html>
    <html>
        <head>
            <title>YelpCamp</title>
        </head>
        <body>
         5. Open the footer file and complete the boilerplate:
       <p>Trademark 2020</p>
       </body>
   </html>
         6. Add links to the header and footer files in to our landing page:
   <%- include(“partials/header”) %>

   <h1>
        Landing Page
    </h1>
    <p>
        Welcome to YelpCamp
    </p>


    <a href="/campgrounds">View all campgrounds</a>


    <%- include(“partials/footer”) %>
            7. Restart the server and have a look at the index page to see the footer
            8. Add the header and footers to the campgrounds.ejs file
   <%- include("partials/header") %>
    <h1>
        This is the campgrounds page
    </h1>


    <% campgrounds.forEach(function(campground){ %>
        <div>
            <h4>
                <%= campground.name %>        
            </h4>
            <img src="<%= campground.image %>">
        </div>
    <% }); %>
    <%- include("partials/footer") %>
               9. Restart the server and check header and footer added to campgrounds.
               10. Add Bootstrap CDN to project:
    <!DOCTYPE html>
    <html>
        <head>
        <title>YelpCamp</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        </head>
        <body>
        <p>
            This is a header
        </p>
               11. Restart server and refresh to see the changes bootstrap makes


Video 3
## Creating New Campgrounds
               * Setup new campground POST route
               * Add in body-parser
               * Setup route to show form
               * Add basic unstyled form


               1. Create a post route under the get route for campgrounds:
   app.post("/campgrounds", function(req, res){
        res.send("You have hit the POST route");
        // get data from form and add to campgrounds array
        // redirect back to campgrounds page
    });
                  2. Install body-parser into the project:
   npm install body-parser --save
                  3. Setup body parser in your app.js file:
   var bodyParser = require(“body-parser”);
                  4. Tell express to use body parser:
   app.use(bodyParser.urlencoded({extended: true}));
                  5. Restart the server to see if set up is correct, you will get no errors if correct.
                  6. Create a new route for the new campground form:
   app.get("/campgrounds/new", function(req, res){
        res.render("new.ejs");
    });
                     7. Create the new.ejs file:
   touch views/new.ejs
                     8. Open the new.ejs file:
   goorm views/new.ejs
                     9. Setup a basic form in new.ejs:
   <%- include("partials/header") %>
    <h1>
        Create a new Campground
    </h1>
    <form action="/campgrounds" method="POST">
        <input type="text" name="name" placeholder="name">
        <input type="text" name="image" placeholder="image url">
        <button>
            Submit
        </button>
    </form>
    <%- include("partials/footer") %>
                        10. Restart the server and go to url/campgrounds/new to see the form exists
                        11. Enter something random in to name and image url and hit submit, this should display the POST route message.
                        12. Move the array out from the route it is sat in, and place under the app.use and app.set lines:
   app.use(bodyParser.urlencoded({extended: true}));
    app.set("view engine", "ejs");


    var campgrounds = []

   app.get("/campgrounds", function(req, res) {
        res.render("campgrounds", {campgrounds: campgrounds});
    });
                           13. In the app.post route get the data from the form and add to the campgrounds array, and then redirect to campgrounds page:
   app.post("/campgrounds", function(req, res){
        // get data from form and add to campgrounds array
        var name = req.body.name;
        var image = req.body.image;
        var newCampground = {name: name, image: image};
        campgrounds.push(newCampground);
        // redirect back to campgrounds page
        res.redirect("/campgrounds");
    });
                              14. Restart the server, and refresh url/campgrounds/new.  Create a new campground and submit. This should create a new campground that appears at the bottom of url/campgrounds.  If you get an error message, make sure you only have res.redirect in the app.post and you have removed the re.render from the first line.  You can only have one res. command in each route.
                              15. Add a link to campgrounds.ejs to link to new.ejs:
   <a href="/campgrounds/new">Add new Campground</a>
                              16. Restart the server and navigate to url/campgrounds.  You should see a new link on the page, and clicking this will take you to the url/campgrounds/new form.
                              17. On the new.ejs file add a link to take you back to url/campgrounds:
   <a href="/campgrounds">Go back</a>


Video 4
##Style the campgrounds page
                                 * Add a better header/title
                                 * Make campgrounds display in a grid


                                 1. Open campgrounds.ejs
                                 2. Add a header to the page and move the h1 in to it:
   <header class="jumbotron">
        <h1>
            This is the campgrounds page
        </h1>
    </header>        
                                    3. Excluding the header and footer includes, move the page content in to a new div with the class container:
   <%- include("partials/header") %>
    <div class="container">
        <header class="jumbotron">
            <h1>
                Welcome to YelpCamp!
            </h1>
        <p>View our hand-picked campgrounds from all over the world
        </header>        


        <a href="/campgrounds/new">Add new Campground</a>


        <% campgrounds.forEach(function(campground){ %>
            <div>
                <h4>
                    <%= campground.name %>        
                </h4>
                <img src="<%= campground.image %>">
            </div>
        <% }); %>
    </div>
    <%- include("partials/footer") %>
                                       4. Restart the server and then refresh the url/campgrounds page to see the new layout of the header
                                       5. Move the anchor up into the jumbotron, but also make it a button:
   <header class="jumbotron">
        <h1>
            Welcome to YelpCamp!
        </h1>
        <p>
            View our hand-picked campgrounds from all over the world
        </p>
        <p>
            <a class="btn btn-primary btn-lg" href="/campgrounds/new">
                Add new Campground
            </a>
        </p>
    </header>
                                          6. Add a new container inside the jumbotron and place everything in it to retain spacing on resizing of window:
   <header class="jumbotron">
        <div class="container">
            <h1>
                Welcome to YelpCamp!
            </h1>
            <p>
                View our hand-picked campgrounds from all over the world
            </p>
            <p>
                <a class="btn btn-primary btn-lg" href="/campgrounds/new">
                    Add new Campground
               </a>
            </p>
        </div>
    </header>
                                             7.  Make the images appear in a grid using some Bootstrap classes:
    <div class="row">
        <% campgrounds.forEach(function(campground){ %>
            <div class="col-md-3 col-sm-6">
                <div class="thumbnail">
                    <img src="<%= campground.image %>">
                </div>                                        
            </div>
        <% }); %>
    </div>
                                             8. Under the thumbnail class add another div with the caption class:
   <div class="thumbnail">
        <img src="<%= campground.image %>">
        <div class="caption">
            <h4>
                <%= campground.name %>
            </h4>
        </div>
    </div>                                        
                                                9. Add some styling to the row class to make the grid work right when more data is added to campgrounds:
   <div class="row" style="display:flex; flex-wrap: wrap;">
                                                10. Make another change to row class to make text appear center:
   <div class="row text-center" style="display:flex; flex-wrap: wrap;">


Video 5
##Style the Navbar and Form
                                                   * Add a navbar to all templates
                                                   * Style the new campground form


                                                   1. Add a navbar to campgrounds.ejs.  This is placed under the partials/header link:
   <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <a class="navbar-brand" href="/">YelpCamp</a>
            </div>
        </div>
     </nav>
                                                      2. Expand on the navbar by adding some placeholder to links to the right of the navbar:
<nav class="navbar navbar-default">
    <div class="container-fluid">
        <div class="navbar-header">
            <a class="navbar-brand" href="/">YelpCamp</a>
        </div>
        <div class="collapse navbar-collapse">
            <ul class="nav navbar-nav navbar-right">
                <li><a href="/">Login</a></li>
                <li><a href="/">Sign Up</a></li>
                <li><a href="/">Logout</a></li>
            </ul>
        </div>
    </div>
</nav>
                                                         3. Move the nav bar to the header.ejs file
                                                         4. In new.ejs add some bootstrap to input and buttons:
   <input class="form-control" type="text" name="name" placeholder="name">
    <input class="form-control" type="text" name="image" placeholder="image url">
    <button class="btn btn-lg btn-default">
        Submit
    </button>
                                                            5. Place everything excluding the partials in to a container:
   <div class="container">
        <h1>
            Create a new Campground
        </h1>


        <form action="/campgrounds" method="POST">
            <input class="form-control" type="text" name="name" placeholder="name">
            <input class="form-control" type="text" name="image" placeholder="image url">
            <button class="btn btn-lg btn-default">
                Submit
            </button>
        </form>
        <a href="/campgrounds">Go back</a>
    </div>
                                                               6. Now place all the content in a row within the container:
   <div class="container">
        <div class=”row”>        
            <h1>
                Create a new Campground
            </h1>


            <form action="/campgrounds" method="POST">
                <input class="form-control" type="text" name="name" placeholder="name">
                <input class="form-control" type="text" name="image" placeholder="image url">
                <button class="btn btn-lg btn-default">
                    Submit
                </button>
            </form>
            <a href="/campgrounds">Go back</a>
        </div>
    </div>
                                                                  7. Place the form content into another stylised div:
   <div style="width: 30%; margin: 0 auto;">
        <form action="/campgrounds" method="POST">
            <input class="form-control" type="text" name="name" placeholder="name">
            <input class="form-control" type="text" name="image" placeholder="image url">
            <button class="btn btn-lg btn-default">
                Submit
            </button>
        </form>
    </div>
                                                                     8. Add another bootstrap class to the button to make it larger:
<button class=”btn btn-lg btn-default btn-block”>
                                                                     9. Wrap each input in to another div with the class form-group:
   <div class=”form-group”>
       <input class="form-control" type="text" name="name" placeholder="name">
   </div>
    <div class=”form-group”>
       <input class="form-control" type="text" name="image" placeholder="image url">
   </div>
    <div class=”form-group”>
       <button class="btn btn-lg btn-default">
            Submit
        </button>
    </div>
                                                                        10. Centre the Create a New Campground text:
   <h1 style="text-align: center;">
        Create a new Campground
    </h1>
                                                                           11. Change the button colour by changing it’s class slightly:
   <button class=”btn btn-lg btn-primary”>
                                                                           12. Move the Go Back link to the line just under the form closing tags:
       </form>
        <a href="/campgrounds">Go back</a>
    </div>
                                                                              13. Add some margin to the div that appears after the Create A New Campground heading:
   <h1 style="text-align: center;">
        Create a new Campground
    </h1>
    <div style="width: 30%; margin: 25px auto;">
                                                                                 14. Remove the Trademark from the footer






Notes on Installing Mongo
                                                                                 1. Mongod
                                                                                 2. Echo “mongod --nojournal” > mongod
                                                                                 3. ./mongod
                                                                                 4. You will get permission denied
                                                                                 5. Chmod a+x mongod
                                                                                 6. ./mongod
                                                                                 7. In a new terminal window: mongo
                                                                                 8. “Show dbs” to show databases
                                                                                 9. “Use dbname” to use a database name (dbname is placeholder, use the name of the database you want to use that was shown in “show dbs”)
                                                                                 10. To quit mongo type exit
                                                                                 11. Ctrl-C the mongod terminal when done

Notes on using mongoose
Use the following whenever requiring mongoose in your project:
    const mongoose = require('mongoose');
    mongoose.connect('mongodb://localhost:27017/db_name', {
        useNewUrlParser: true,
        useUnifiedTopology: true
    })
    .then(() => console.log('Connected to DB!'))
    .catch(error => console.log(error.message));


Notes about using Mongo
                                                                                 * Show dbs - shows all the databases in your mongo shell
                                                                                 * Use databaseName - will open up the named database for query
                                                                                 * Show collections - will show all data collections within specified database
                                                                                 * db.collectionName.find() - will display all entries within collection




Video 6
##Add Mongoose
                                                                                 * Install and configure mongoose
                                                                                 * Setup campground model
                                                                                 * Use campground model inside of our routes


                                                                                 1. Install mongoose in to your project:
   Npm install mongoose --save
                                                                                 2. Ensure mongod is running (new terminal window ./mongod, new terminal window mongo)
                                                                                 3. Require mongoose within your app.js:
    const mongoose = require('mongoose');
    mongoose.connect('mongodb://localhost:27017/db_name', {
        useNewUrlParser: true,
        useUnifiedTopology: true
    })
    .then(() => console.log('Connected to DB!'))
    .catch(error => console.log(error.message));
                                                                                    4. Restart the server to make sure it all works
                                                                                    5. Create a Schema and a model for the campgrounds:
   // Schema setup
   var campgroundSchema = new mongoose.Schema({
       name: String,
       image: String
   });
   var Campground = mongoose.model(“Campground, campgroundSchema);
                                                                                    6. Create a campground entry:
   Campground.create(
        {
           name: "Salmon Creek",
            image: "img_url"
       }, function (err, campground){
           if(err) {
               console.log(err);
           } else {
               console.log("Newly Created Campground");
                console.log(campground);
           }
       }
   );
                                                                                       7. Restart the server and check the terminal to see if you get an error or notification of a newly created campground.
                                                                                       8. Swap to the mongo terminal and check to see if the campground now exists:
   Use yelp_camp
   Show collections
   db.campgrounds.find()
Campgrounds should appear after running show collections
And the campground you created should appear after running db.campgrounds.find()
                                                                                       9. Try creating a second campground and check the database
                                                                                       10. Comment out the Campground.create and delete the campgrounds array
                                                                                       11. Update app.get(“/campgrounds”) to query the database instead:
   app.get("/campgrounds", function(req, res) {
        // Get all campgrounds from DB
        Campground.find({}, function(err, allCampgrounds){
            if(err){
                console.log(err);
            } else {
                res.render("campgrounds", {campgrounds: allCampgrounds});        
            }
        });
    });
                                                                                          12. Restart the server and check the url/campgrounds page.  Only one or two campgrounds should be listed.
                                                                                          13. app.post(“/campgrounds”) will no longer work as the array no longer exists, update app.post to use the database instead:
   app.post(“/campgrounds”, function(req, res) {
       // get data from form and add to campgrounds database
       Var name = req.body.name;
       Var image = req.body.image;
       Var newCampground = {name: name, image: image};
       // create a new campground and save to database
       Campground.create(newCampground, function(err, newlyCreated){
           if(err) {
               console.log(err);
           } else {
               res.redirect(“/campgrounds”);
           }
       });
   });
                                                                                          14. Restart the server and go to url/campgrounds/new and create a new campground.  If it works it should go back to url/campgrounds and you should see the newly created campground displayed.




Video 7
##Show page
                                                                                             * Review the RESTful routes
                                                                                             * Add description to our campground model
                                                                                             * Show db.collection.drop()
                                                                                             * Add a show route/template


RESTful Notes
Name                url                verb                description
=====================================================
INDEX                /dogs                GET                Display a list of all dogs
NEW                /dogs/new        GET                Displays form to make new dog
CREATE        /dogs                POST                Add new dog to database
SHOW                /dogs/:id        GET                Show a specific dog


                                                                                             1. Create a new SHOW route in the app.js file:
   app.get(“/campgrounds/:id”, function(req, res){
       res.send(“This will be the SHOW page one day”);
   });
                                                                                             2. Restart the server and navigate to url/campgrounds/something, the message should display.
                                                                                             3. Add a description to the campgroundSchema:
   Var campgroundSchema = new mongoose.Schema({
       name: String,
       image: String,
       description: String
   });
                                                                                             4. Swap to the mongo terminal window and clear the database:
   db.campgrounds.drop()
                                                                                             5. Go back to app.js and uncomment the Campground.create method, add a description property and create a new campground:
   Campground.create(
        {
            name: "Banjo Spring",
            image: "img_url",
            description: "Twang that banjo at a spring!"
        }, function (err, campground){
            if(err) {
                console.log(err);
            } else {
                console.log("Newly Created Campground");
                console.log(campground);
            }
        }
                );
                                                                                                6. Restart the server and see if the campground is created.
                                                                                                7. Swap to the mongo terminal and check there is an entry in the database.
   db.campgrounds.find()


Video 8
##Show page continued
                                                                                                   1. Rename campgrounds.ejs to index.ejs and change the index route to reflect the change:
   app.get("/campgrounds", function(req, res) {
        // Get all campgrounds from DB
        Campground.find({}, function(err, allCampgrounds){
            if(err){
                console.log(err);
            } else {
                res.render("index", {campgrounds: allCampgrounds});        
            }
        });
                });
                                                                                                      2. Open index.ejs and add a new paragraph under the campground.name div:
   <div class="caption">
        <h4>
           <%= campground.name %>
        </h4>
    </div>
    <p>
        <a href="" class="btn btn-primary">More Info</a>
    </p>
                                                                                                         3. Restart the server and see the change to url/campgrounds
                                                                                                         4. Go back to index.ejs and add a link to the campground page by updating the href:
   href=”/campgrounds/<%= campground._id %>”
                                                                                                         5. Restart the server and go to url/campgrounds and click the More Info button.  This should now take you to the SHOW page for that campsite (url/campgrounds/campgroundId) but display the This is the SHOW route message.
                                                                                                         6. Back in app.js update the SHOW route to display the campground name:
   // Show Route - shows more info about one campground
    app.get("/campgrounds/:id", function(req, res){
        // find the campground with the provided ID
        Campground.findById(req.params.id, function(err, foundCampground) {
            if(err) {
                console.log(err);
            } else {
                // render show template with that campground
                res.render("show", {campground: foundCampground});
            }
        });
    });
                                                                                                            7. Over in show.ejs update the page so that it displays the campground name:
   <p>
        <%= campground.name %>
    </p>
                                                                                                               8. Restart the server and click on More Info for a campground.  The SHOW page should display, showing the campground name.
                                                                                                               9. Change the show.ejs file to display an image and description, moving the title in to the header:
   <h1>
        <%= campground.name %>
    </h1>


    <img src="<%= campground.image %>">


    <p>
        <%= campground.description %>
    </p>
                                                                                                                  10. Restart the server and update the url/campground/campgroundId page and you should see the name, image and description.
                                                                                                                  11. Add the include partials lines to the show.ejs:
    <%- include("partials/header") %>
   Show.ejs page content
    <%- include("partials/footer") %>
                                                                                                                     12. Update new.ejs to include a description field:
   <div class="form-group">
        <input class="form-control" type="text" name="image" placeholder="image url">
    </div>
    <div class="form-group">
        <input class="form-control" type="text" name="description" placeholder="description">
    </div>
    <div class="form-group">
        <button class="btn btn-lg btn-primary btn-block">
            Submit
        </button>
    </div>
                                                                                                                        13. In app.js have the create route collect the description of the campground:
   // Create Route - Add new campground to database
    app.post("/campgrounds", function(req, res){
        // get data from form and add to campgrounds array
        var name = req.body.name;
        var image = req.body.image;
        var desc = req.body.description;
        var newCampground = {name: name, image: image, description: desc};
        // Create a new campground and save to DB
        Campground.create(newCampground, function(err, newlyCreated){
            if(err) {
                console.log(err)
            } else {
                res.redirect("/campgrounds");
            }
        });
    });
                                                                                                                           14. Restart the server and create a new campground at url/campgrounds/new.  Once created click on the More Info and you should see all the details.


Video 9
##Refactor Mongoose Code
                                                                                                                           * Create a models directory
                                                                                                                           * Use module.exports
                                                                                                                           * Require everything correctly


Code is now at version 3


                                                                                                                           1. Create a new directory called models and place a campground.js file within:
   mkdir models
   touch models/campground.js
   goorm models/campground.js
                                                                                                                           2. Cut the campgroundSchema content and paste in to the campground.js file, including the require of mongoose and an export:
   const mongoose         = require('mongoose');
            // looks like you don’t have to include all the extra mongoose guff in the model files


    // Schema setup
    var campgroundSchema = new mongoose.Schema({
        name: String,
        image: String,
        description: String
    });


    module.exports = mongoose.model("Campground", campgroundSchema);
                                                                                                                              3. Require the new campground.js file in to your app.js:
   Campground = require(“./models/campground”);
                                                                                                                              4. Test everything works by restarting the server and refreshing the url/campgrounds page.  If you see campgrounds it worked!


Video 10
##Add seeds file
                                                                                                                                 * Add a seeds.js file
                                                                                                                                 * Run the seeds file every time the server starts


                                                                                                                                 1. Create a seeds file in your v3 directory:
   touch seeds.js
                                                                                                                                 2. Open seeds.js:
   goorm seeds.js
                                                                                                                                 3. Require mongoose:
   var mongoose = require(“mongoose”);
                                                                                                                                 4. Require campground model:
   var Campground = require(“./models/campground”);
                                                                                                                                 5. Clear the database with a method:
   Campground.remove({}, function(err){
       if(err){
           console.log(err);
       } else {
           console.log(“Removed campgrounds”);
       }
   });
                                                                                                                                 6. In your app.js file require the seeds.js file:
   var seedDB = require(“./seeds”);
   seedDB();
                                                                                                                                 7. Add an exports to your seeds.js file:
Module.exports = seedDB;
                                                                                                                                 8. Restart the server, you should see Removed campgrounds in your terminal window.  You are also likely to see a DeprecationWarning.  This can be ignored or you could replace Campground.remove({}... with Campground.deleteMany({}...  Refreshing the url/campgrounds page will show the campgrounds have been removed.
                                                                                                                                 9. Create some sample data for the seeds.js file to use:
   Var data = [
       {
           Name: “Cloud’s Rest”,
           Image: “img_url”,
           Description: “Some text here”
       } x3
   ]
                                                                                                                                 10. In the seedDB function create a loop:
   // Add a few campgrounds
   data.forEach(function(seed){
       Campground.create(seed, function(err, data) {
           if(err) {
                console.log(err);
           } else {
               console.log(“Removed campgrounds”);
           }
       });
   });
                                                                                                                                    11. Ensure this new loop sits within the else statement of Campground.deleteMany or .remove, but after the console.log(“Removed campgrounds”):
   function seedDB(){
       // Remove all campgrounds
        // Campground.remove({}, function(err){
        Campground.deleteMany({}, function(err){
            if(err) {
                console.log(err);
            } else {
                console.log("Removed campgrounds");
                // Add a few campgrounds
                data.forEach(function(seed){
                    Campground.create(seed, function(err, data){
                        if(err) {
                            console.log(err);
                        } else {
                            console.log("added a campground");
                        }
                    });
                });
            }
        });
        // add a few comments
    }
                                                                                                                                       12. Restart the server, the terminal should display:
   Removed campgrounds
   Added a campground
   Added a campground
   Added a campground
                                                                                                                                       13. Refresh the url/campgrounds page and you should see 3 campgrounds.
                                                                                                                                       14. Create a comment within the Campground.create method:
   Campground.create(seed, function(err, campground){
        if(err) {
            console.log(err);
        } else {
            console.log("added a campground");
            // create a comment
            Comment.create({
                text: "This place is great but I wish there was Wifi",
                author: "Homer"
            }, function(err, comment) {
                if(err){
                    console.log(err);
                } else {
                    campground.comments.push(comment);
                    campground.save();
                    console.log("created new comment");
                }
            });
        }
    });
                                                                                                                                          15. Set up a require for Comment, even though we don’t have a Comment file set up yet:
Comment = require(“./models/comment”);




Video 11
##Add the comment model
                                                                                                                                             * Make our errors go away
                                                                                                                                             * Display comments on campground show page


                                                                                                                                             1. Create the comment.js file:
   Touch models/comment.js
                                                                                                                                             2. Open the comment file:
   Goorm models/comment.js
                                                                                                                                             3. Prepare the module.exports:
   Module.exports = ;
                                                                                                                                             4. Import mongoose:
   Var mongoose = require(“mongoose”);
                                                                                                                                             5. Now create the comment model:
   Var commentSchema = mongoose.Schema({
       Text: String,
       Author: String
   });
                                                                                                                                             6. And update the exports:
   Module.exports = mongoose.model(“Comment”, commentSchema);
                                                                                                                                             7. Restart the server and check for errors.
                                                                                                                                             8. You will get errors.  Stick with the videos
                                                                                                                                             9. In campground.js make a reference to the comments:
   var campgroundSchema = new mongoose.Schema({
        name: String,
        image: String,
        description: String,
        comments: [
            {
                type: mongoose.Schema.Types.ObjectID,
                ref: "Comment"
            }
        ]
    });
                                                                                                                                                10. Restart the server again and you should get no errors.  Check the url/campgrounds and the database for entries.
                                                                                                                                                11. Go to app.js and delete all the comment out section that was creating a new campground.
                                                                                                                                                12. Update the SHOW route so that comments are retrieved too:
   // Show Route - shows more info about one campground
    app.get("/campgrounds/:id", function(req, res){
        // find the campground with the provided ID
        Campground.findById(req.params.id).populate("comments").exec(function(err, foundCampground) {
           if(err) {
               console.log(err);
            } else {
                console.log(foundCampground);
                // render show template with that campground
                res.render("show", {campground: foundCampground});
            }
        });
   });
                                                                                                                                                   13. Restart the server.  When checking the webpage make sure you start at url/ first, as stated before all campground IDs will have changed and you will need to start from the index page to view without errors.  When you click on More Info your terminal should display the campground including comments.  If you get an error navigate to url/ first and then url/campground/:id
                                                                                                                                                   14. Open the show.ejs:
   Goorm views/show.ejs
                                                                                                                                                   15. Add a loop to display comments and authors above the footer:
   <% campground.comments.forEach(function(comment){ %>
        <p><strong><%= comment.author %></strong> - <%= comment.text %></p>
    <% }) %>
    <%- include("partials/footer") %>
                                                                                                                                                      16. Restart the server and visit a campground page.
                                                                                                                                                      17. You should now see a comment by Homer.




Video 12
##Comment New/Create
                                                                                                                                                      * Discuss nested routes
                                                                                                                                                      * Add the comment new and create routes
                                                                                                                                                      * Add the new comment form


                                                                                                                                                      1. Create a new route in the app.js file just above the app.listen:
   //==========================
    //Comments Routes
    //==========================


    app.get("/campgrounds/:id/comments/new", function(req, res){
        res.render("comments/new");
    });
                                                                                                                                                         2. Create a couple of new folders in your views directory to handle comments and campgrounds:
   Mkdir views/campgrounds
   Mkdir views/comments
                                                                                                                                                         3. Move the new.ejs, show.ejs and index.ejs into the new views/campgrounds folder
                                                                                                                                                         4. Create a new.ejs file in the views/comments folder
                                                                                                                                                         5. Restart the server, you will get an error message when you try to go to view campgrounds, this is because the header and footer partial links in new.ejs, show.ejs and index.ejs are all now incorrect.
                                                                                                                                                         6. Fix the header and footer partial links in new.ejs, show.ejs and index.ejs:
   <%- include("../partials/header") %>
   <%- include("../partials/footer") %>
                                                                                                                                                         7. Open up the new.ejs in views/comments and add a header stating this is the new comment form.
                                                                                                                                                         8. Restart the server and everything should be fine
                                                                                                                                                         9. Navigate to a campground page and then go to the new comment url:
   url/campgrounds/:id/comments/new
                                                                                                                                                         10. You should see the header you added.
                                                                                                                                                         11. Copy the contents of new.ejs from views/campgrounds and paste it in to your new.ejs in views/comments.  Change up some of the details so that it relates to a comment rather than a campground:
   <%- include("../partials/header") %>
    <div class="container">
        <div class="row">
            <h1 style="text-align: center;">
                Add New Comment to <%= campground.name %>
            </h1>
            <div style="width: 30%; margin: 25px auto;">
                <form action="/campgrounds/<%= campground._id %>/comments" method="POST">
                    <div class="form-group">
                        <input class="form-control" type="text" name="comment[text]" placeholder="text">        
                    </div>
                    <div class="form-group">
                        <input class="form-control" type="text" name="comment[author]" placeholder="author">
                    </div>
                    <div class="form-group">
                        <button class="btn btn-lg btn-primary btn-block">
                            Submit
                        </button>
                    </div>
                 </form>
                 <a href="/campgrounds">Go back</a>
            </div>
        </div>
    </div>
    <%- include("../partials/footer") %>
                                                                                                                                                            12. Update the new comment route in app.js to send the data required for the new.ejs for comments:
   app.get("/campgrounds/:id/comments/new", function(req, res){
        // find campground by id
        Campground.findById(req.params.id, function(err, campground){
            if(err) {
                console.log(err);
            } else {
                res.render("comments/new", {campground: campground});        
            }
        });
    });
                                                                                                                                                               13. Now create a POST route for the new comments:
   app.post("/campgrounds/:id/comments", function(req, res){
        // lookup campground using id
        Campground.findById(req.params.id, function(err, campground){
            if(err){
                console.log(err);
                res.redirect(".campgrounds");
            } else {
                Comment.create(req.body.comment, function(err, comment){
                    if(err){
                        console.log(err);
                    } else {
                        campground.comments.push(comment);
                        campground.save();
                        res.redirect("/campgrounds/" + campground._id);
                    }
                });
            }
        });
        // create new comments
        // connect new comment to campground
        // redirect to campground show page
    });
                                                                                                                                                                  14. Add a button to the show page to create a new comment:
   <p>
        <a class="btn btn-success" href="/campgrounds/<%= campground._id %>/comments/new">Add New Comment</a>
    </p>




Video 13
##Style Show Page
                                                                                                                                                                     * Add sidebar to show page
                                                                                                                                                                     * Display comments nicely


                                                                                                                                                                     1. In the show.ejs in views/campgrounds, add a side bar under the partial header:
   <div class="container">
        <div class="row">
            <div class="col-md-3">
                <p class="lead">
                    YelpCamp
                </p>
                <div class="list-group">
                    <li class="list-group-item active">Info 1</li>
                    <li class="list-group-item">Info 2</li>
                    <li class="list-group-item">Info 3</li>
                </div>
            //MAP
            </div>
         </div>
     </div>
                                                                                                                                                                        2. Expand on the side bar to include the main page elements so that show.ejs looks like this:
   <%- include("../partials/header") %>
        <div class="container">
                        <div class="row">
                <div class="col-md-3">
                    <p class="lead">
                        YelpCamp
                    </p>
                    <div class="list-group">
                        <li class="list-group-item active">Info 1</li>
                        <li class="list-group-item">Info 2</li>
                        <li class="list-group-item">Info 3</li>
                    </div>
                    <!-- Map will go here -->
                </div>
                <div class="col-md-9">
                    <div class="thumbnail">
                        <img class="image-responsive" src="<%= campground.image %>">
                            <div class="caption-full">
                                <h4 class="pull-right">
                                    £9.00/night
                                </h4>
                                <h4>
                                    <a><%= campground.name %></a>
                                </h4>
                                <p>
                                    <%= campground.description %>
                                </p>
                            </div>
                        </div>
                    </div>
               </div>
            </div>
           <p>
               <a class="btn btn-success" href="/campgrounds/<%= campground._id %>/comments/new">Add New Comment</a>
            </p>


    <% campground.comments.forEach(function(comment){ %>
        <p><strong><%= comment.author %></strong> - <%= comment.text %></p>
    <% }) %>
    <%- include("../partials/footer") %>
                                                                                                                                                                           3. Now add the comments in to the bootstrap elements:
   <div class="well">
        <div class="text-right">
            <a class="btn btn-success" href="/campgrounds/<%= campground._id %>/comments/new">Add New Comment</a>
        </div>
        <hr>
        <% campground.comments.forEach(function(comment){ %>
            <div class="row">
                <div class="col-md-12">
                    <strong><%= comment.author %></strong>
                    <span class="pull-right">10 days ago</span>
                    <p>
                        <%= comment.text %>
                    </p>
                </div>
            </div>
        <% }) %>
    </div>
                                                                                                                                                                              4. Make a public directory, and then make a stylesheets directory and create a file called main.css in there:
   Mkdir public
   Mkdir public/stylesheets
   Touch public/stylesheets/main.css
                                                                                                                                                                              5. Open main.css:
   Goorm public/stylesheets/main.css
                                                                                                                                                                              6. Change the body style to see the css changes on the site:
   Body {
       Background-color: purple;
   }
                                                                                                                                                                              7. Add the css file to the app.js file:
   app.use(express.static(__dirname + “/public”);
                                                                                                                                                                              8. Go to the header.ejs file and add another link to the head tag:
   <link rel="stylesheet" href="/stylesheets/main.css">
                                                                                                                                                                              9. Restart the server and you should see a purple background on every page.
                                                                                                                                                                              10. Swap back to main.css and remove the purple background, and then add a width value to all thumbnail images:
   .thumbnail img {
       Width: 100%;
   }
                                                                                                                                                                              11. Remove the padding from the thumbnail:
   .thumbnail {
       Padding: 0;
   }
                                                                                                                                                                              12. Add some padding to the caption:
   .thumbnail .caption-full {
       Padding: 9px;
   }


Video 14
##Add User Model
                                                                                                                                                                                 * Install all packages needed for auth
                                                                                                                                                                                 * Define User model


                                                                                                                                                                                 1. Install all the required packages:
   Npm install passport passport-local passport-local-mongoose express-session --save
                                                                                                                                                                                 2. Check the package json file:
   Goorm package.json
                                                                                                                                                                                 3. Create a user.js file:
    Touch models/user.js
                                                                                                                                                                                    4. Create a user schema for mongoose:
   var mongoose = require("mongoose");
    var passportLocalMongoose = require("passport-local-mongoose");
    var UserSchema = new mongoose.Schema({
        username: String,
        password: String
    });
    UserSchema.plugin(passportLocalMongoose);
    module.exports = mongoose.model("User", UserSchema);
                                                                                                                                                                                       5. Add the packages to your app.js file:
   passport         = require("passport"),
    LocalStrategy = require("passport-local"),
    User = require("./models/user"),
                                                                                                                                                                                          6. Restart the server to see if there are any errors


Video 15
##Register
                                                                                                                                                                                          * Configure Passport
                                                                                                                                                                                          * Add register routes
                                                                                                                                                                                          * Add register template


                                                                                                                                                                                          1. Open app.js and configure passport:
   // Passport Config
    app.use(require("express-session")({
        secret: "This is my secret",
        resave: false,
        saveUninitialized: false
    }));
    app.use(passport.initialize());
    app.use(passport.session());
    passport.use(new LocalStrategy(User.authenticate()));
    passport.serializeUser(User.serializeUser());
    passport.deserializeUser(User.deserializeUser());
                                                                                                                                                                                             2. Create a register route in your app.js:
   // show register form
    app.get("/register", function(req, res){
        res.render("register");
    });
                                                                                                                                                                                                3. Create register.ejs in the views directory:
   Touch views/register.ejs
                                                                                                                                                                                                4. Open up register.ejs and create some content to see if the route works:
   Goorm views/register.ejs
    <h1>
       Sign Up!
   </h1>
                                                                                                                                                                                                   5. Restart the server and check the register page:
   url/register
                                                                                                                                                                                                   6. This should display Sign Up!
                                                                                                                                                                                                   7. Create a form in the register.ejs:
   <form action="/register" method="post">
        <input type="text" name="username" placeholder="username">
        <input type="password" name="password" placeholder="password">
        <button>
            Sign Up
        </button>
    </form>
                                                                                                                                                                                                      8. Create a post route for register in app.js:
   //handle sign up logic
    app.post("/register", function(req, res){
        var newUser = new User({username: req.body.username});
        User.register(newUser, req.body.password, function(err, user){
            if(err){
                console.log(err);
                return res.render("register");
            }
            passport.authenticate("local")(req, res, function(){
            res.redirect("/campgrounds");
            });
        });
    });
                                                                                                                                                                                                         9. Restart the server and navigate to url/register
                                                                                                                                                                                                         10. Create a new account.  If it works you will be redirected back to the campgrounds page, other wise the sign up page will be displayed again.
                                                                                                                                                                                                         11. You can see if it works by opening up a new terminal window and looking in the mongo database for the account you created:
   Mongo
   Use yelp_camp
                db.users.find()
                                                                                                                                                                                                            12. A user should be displayed with an incredibly large object that is the password.


Video 16
##Login
                                                                                                                                                                                                            * Add login routes
                                                                                                                                                                                                            * Add login template


                                                                                                                                                                                                            1. Create the login route in app.js:
// Login routes
// show login form
    app.get("/login", function(req, res){
        res.render("login");
    });
                                                                                                                                                                                                               2. Create a login.ejs file and open it:
   Touch views/login.ejs
   Goorm views/login.ejs
                                                                                                                                                                                                               3. Put some content in and then restart the server and check it renders:
   <h1>
       Login!
   </h1>
   url/login
                                                                                                                                                                                                               4. Create a login form:
    <form action="/login" method="POST">
        <input type="text" name="username" placeholder="username">
        <input type="password" name="password" placeholder="password">
        <input type="submit" value="Login!">
    </form>
                                                                                                                                                                                                                  5. Restart the server and refresh the login page to see the form.  Try logging in, it will error as we don’t have a route set up.
                                                                                                                                                                                                                  6. Update the route in app.js:
    // handle login logic
    app.post("/login", function(req, res){
        res.send("Login Logic");
    });
                                                                                                                                                                                                                  7. Restart the server and try logging in with any credentials to see the Login Logic message
                                                                                                                                                                                                                  8. Insert middleware in to the login route:
    app.post("/login", passport.authenticate("local", {
        successRedirect: "/campgrounds",
        failureRedirect: "/login"
    }), function(req, res){
    });
                                                                                                                                                                                                                  9. Restart the server and login using correct details, this should take you to campgrounds.  And if you login with incorrect details, it should refresh the login page.


Video 17
##Logout / Navbar
                                                                                                                                                                                                                  * Add logout route
                                                                                                                                                                                                                  * Prevent user from adding a comment if not signed in
                                                                                                                                                                                                                  * Add links to navbar
                                                                                                                                                                                                                  * Show/hide auth links correctly


                                                                                                                                                                                                                  1. Add a logout route:
   // Logout routes
    app.get("/logout", function(req, res){
        req.logout();
        res.redirect("/campgrounds");
    });
                                                                                                                                                                                                                     2. Open the header.ejs file and fix the navbar links:
   <li><a href="/login">Login</a></li>
    <li><a href="/register">Sign Up</a></li>
    <li><a href="/logout">Logout</a></li>
                                                                                                                                                                                                                        3. Add the header and footer partials to the login.ejs and register.ejs:
    <%- include("./partials/header") %>
   <%- include("./partials/footer") %>
                                                                                                                                                                                                                        4. In app.js write a logged in checker function:
   function isLoggedIn(req, res, next){
        if(req.isAuthenticated()){
            return next();
        }
        res.redirect("/login");
    };
                                                                                                                                                                                                                           5. Add this function in to the create new comment route as a middleware:
   app.get("/campgrounds/:id/comments/new", isLoggedIn, function(req, res){
        // find campground by id
        Campground.findById(req.params.id, function(err, campground){
            if(err) {
                console.log(err);
            } else {
                res.render("comments/new", {campground: campground});
            }
        });
    });
                                                                                                                                                                                                                              6. Add middleware to the show comments route too:
   app.post("/campgrounds/:id/comments", isLoggedIn, function(req, res){
        // lookup campground using id
        Campground.findById(req.params.id, function(err, campground){
            if(err){
                console.log(err);
                res.redirect(".campgrounds");
            } else {
                Comment.create(req.body.comment, function(err, comment){
                    if(err){
                        console.log(err);
                    } else {
                        campground.comments.push(comment);
                        campground.save();
                        res.redirect("/campgrounds/" + campground._id);
                    }
                });
            }
        });
    });


Video 18
## Show/Hide Links
                                                                                                                                                                                                                                 * Show/Hide auth links in navbar correctly


                                                                                                                                                                                                                                 1. In app.js add the following app.use before the routes:
   app.use(function(req, res, next){
        res.locals.currentUser = req.user;
        next();
    });
                                                                                                                                                                                                                                    2. In header.ejs add a conditional statement to check if a user is logged in:
   <ul class="nav navbar-nav navbar-right">
        <!-- if no user -->
        <% if(!currentUser){ %>
            <li><a href="/login">Login</a></li>
            <li><a href="/register">Sign Up</a></li>
        <!-- else -->        
        <% } else { %>
            <li><a href="/logout">Logout</a></li>
        <% } %>
    </ul>
                                                                                                                                                                                                                                       3. Restart the server, pages should only show Logout if a user is logged in, and Login/SignUp if a user is not logged in.
                                                                                                                                                                                                                                       4. Above the Logout link add a line to display the user:
<li><a href='#'>Signed in as <%= currentUser.username %></a></li>
	Video 19
## Refactor the Routes
                                                                                                                                                                                                                                       * Use Express router to reorganise all routes


                                                                                                                                                                                                                                       1. Create a new folder called routes:
    Mkdir routes
                                                                                                                                                                                                                                       2. Create a comments.js, campgrounds.js and index.js files in routes:
   Goorm routes/comments.js routes/campgrounds.js routes/index.js
                                                                                                                                                                                                                                       3. Open these files
                                                                                                                                                                                                                                       4. Copy and paste the following from app.js in to each file below:
    Campgrounds.js:
// Index Route - shows all campgrounds
app.get("/campgrounds", function(req, res){
    // Get all campgrounds from DB
   Campground.find({}, function(err, allCampgrounds){
       if(err){
      console.log(err);
  } else {
            res.render("campgrounds/index",{campgrounds:
allCampgrounds, currentUser: req.user});
  }
    });
});


// Create Route - Add new campground to database
app.post("/campgrounds", function(req, res){
    // get data from form and add to campgrounds array
    var name = req.body.name;
    var image = req.body.image;
    var desc = req.body.description;
    var newCampground = {name: name, image: image, description: desc};
    // Create a new campground and save to DB
    Campground.create(newCampground, function(err, newlyCreated){
        if(err) {
            console.log(err)
        } else {
            res.redirect("/campgrounds");
        }
    });
});


// New Route - show form to create new campground
app.get("/campgrounds/new", function(req, res){
    res.render("campgrounds/new");
});


// Show Route - shows more info about one campground
app.get("/campgrounds/:id", function(req, res){
    // find the campground with the provided ID
    Campground.findById(req.params.id).populate("comments")
.exec(function(err, foundCampground) {
        if(err) {
            console.log(err);
        } else {
            console.log(foundCampground);
            // render show template with that campground
            res.render("campgrounds/show", {campground: foundCampground});
        }
    });
});
	

    // Index Route - shows all campgrounds
    app.get("/campgrounds", function(req, res) {
        // Get all campgrounds from DB
       Campground.find({}, function(err, allCampgrounds){
           if(err){
                console.log(err);
            } else {
                res.render("campgrounds/index", {campgrounds: allCampgrounds, currentUser: req.user});        
            }
        });
    });


    // Create Route - Add new campground to database
    app.post("/campgrounds", function(req, res){
        // get data from form and add to campgrounds array
        var name = req.body.name;
        var image = req.body.image;
        var desc = req.body.description;
        var newCampground = {name: name, image: image, description: desc};
        // Create a new campground and save to DB
        Campground.create(newCampground, function(err, newlyCreated){
            if(err) {
                console.log(err)
            } else {
                res.redirect("/campgrounds");
            }
        });
    });


    // New Route - show form to create new campground
    app.get("/campgrounds/new", function(req, res){
        res.render("campgrounds/new");
    });


    // Show Route - shows more info about one campground
    app.get("/campgrounds/:id", function(req, res){
        // find the campground with the provided ID
        Campground.findById(req.params.id).populate("comments").exec(function(err, foundCampground) {
            if(err) {
                console.log(err);
            } else {
                console.log(foundCampground);
                // render show template with that campground
                res.render("campgrounds/show", {campground: foundCampground});
            }
        });
    });


Comments.js:
    //==========================
    //Comments Routes
    //==========================
    app.get("/campgrounds/:id/comments/new", isLoggedIn, function(req, res){
        // find campground by id
        Campground.findById(req.params.id, function(err, campground){
            if(err) {
                console.log(err);
            } else {
                res.render("comments/new", {campground: campground});
            }
        });
    });


    app.post("/campgrounds/:id/comments", isLoggedIn, function(req, res){
        // lookup campground using id
        Campground.findById(req.params.id, function(err, campground){
            if(err){
                console.log(err);
                res.redirect(".campgrounds");
        } else {
                Comment.create(req.body.comment, function(err, comment){
                    if(err){
                        console.log(err);
                    } else {
                        campground.comments.push(comment);
                        campground.save();
                        res.redirect("/campgrounds/" + campground._id);
                    }
                });
            }
        });
    // create new comments
    // connect new comment to campground
    // redirect to campground show page
    });


Index.js:
    app.get("/", function(req, res) {
        res.render("landing");
    });


    // ===========
    // Auth routes
    // ===========


    // show register form
    app.get("/register", function(req, res){
        res.render("register");
    });


    //handle sign up logic
    app.post("/register", function(req, res){
        var newUser = new User({username: req.body.username});
        User.register(newUser, req.body.password, function(err, user){
            if(err){
                console.log(err);
                return res.render("register");
            }
            passport.authenticate("local")(req, res, function(){
            res.redirect("/campgrounds");
            });
        });
    });


    // Login routes
    // show login form
    app.get("/login", function(req, res){
        res.render("login");
    });


    // handle login logic
    app.post("/login", passport.authenticate("local", {
        successRedirect: "/campgrounds",
        failureRedirect: "/login"
    }), function(req, res){
    });


    // Logout routes
    app.get("/logout", function(req, res){
        req.logout();
        res.redirect("/campgrounds");
    });


    function isLoggedIn(req, res, next){
        if(req.isAuthenticated()){
            return next();
        }
        res.redirect("/login");
    };
                                                                                                                                                                                                                                          5. Add requires to each file created:
campground.js:
const Campground         = require("../models/campground"),
      express         = require("express"),
      router         = express.Router();
Comments.js:
const Campground         = require("../models/campground"),
        Comment        = require("../models/comment"),
        express         = require("express"),
        router         = express.Router({mergeParams: true});
Index.js:
const Campground         = require("../models/campground"),
        passport        = require("passport"),
        Comment        = require("../models/comment"),
        express         = require("express"),
        router         = express.Router(),
        User                = require("../models/user");
                                                                                                                                                                                                                                             6. Replace all app.get/app.post with router.get/router.post in each file
                                                                                                                                                                                                                                             7. Add module.exports = router; to the end of each file
                                                                                                                                                                                                                                             8. In app.js add the following lines under the existing const:
const campgroundRoutes         = require("./routes/campgrounds"),
        commentRoutes         = require("./routes/comments"),          
        authRoutes                 = require("./routes/index");


                                                                                                                                                                                                                                             9. And then add the following just above the app.listen method:
    app.use("/", authRoutes);
    app.use("/campgrounds/:id/comments", commentRoutes);
    app.use("/campgrounds", campgroundRoutes);
                                                                                                                                                                                                                                                10. In comments.js you can now remove “/campgrounds/:id/comments” from each of the routes:
    router.get("/new", isLoggedIn, function(req, res){...
   router.post("/", isLoggedIn, function(req, res){...
                                                                                                                                                                                                                                                11. And in campgrounds.js you can remove “/campgrounds” from all routes:
    router.get("/", function(req, res) {...
   router.post("/", function(req, res){...
   router.get("/new", function(req, res){...
   router.get("/:id", function(req, res){...
                                                                                                                                                                                                                                                12. The website should still function once the server has been restarted.


Video 20
##Comments
                                                                                                                                                                                                                                                   * Associate users and comments
                                                                                                                                                                                                                                                   * Save author’s name to a comment automatically


                                                                                                                                                                                                                                                   1. Open up comment.js and remove String from author and replace with an object:
var commentSchema = mongoose.Schema({
    text: String,
    author: {
        Id: {
            Type: mongoose.Schema.Types.ObjectId,
                    Ref: “User”
                   },
        Username: String
    }
});
                                                                                                                                                                                                                                                      2. Open up the seeds.js and comment out every line within the function. Restart the server.  This will have cleared all campgrounds.
                                                                                                                                                                                                                                                      3. Uncomment all the lines and save.
                                                                                                                                                                                                                                                      4. Open up app.js and comment out the line that calls the seedDB function.
                                                                                                                                                                                                                                                      5. Open up comment.js in the routes directory and add the user id and username to the comment creation:
Comment.create(req.body.comment, function(err, comment){
    if(err){
        console.log(err);
    } else {
        // add username and id to comment
        comment.author.id = req.user._id;
        comment.author.username = req.user.username;
        // save comment
        comment.save();
        campground.comments.push(comment);
        campground.save();
        console.log(comment);
        res.redirect("/campgrounds/" + campground._id);
    }
});
                                                                                                                                                                                                                                                         6. Open up new.ejs in views/comments and delete the author input field.
                                                                                                                                                                                                                                                         7. Open up show.ejs in views/campgrounds and update the author field to include the username:
<div class="col-md-12">
    <strong><%= comment.author.username %></strong>
    <span class="pull-right">10 days ago</span>
    <p>
        <%= comment.text %>
    </p>
</div>
                                                                                                                                                                                                                                                            8. Now when you restart the server and make a comment on a campground it will display the user name you logged in with in the comment.


Video 21
## Users and campgrounds
                                                                                                                                                                                                                                                            * Prevent unauthenticated user from creating a campground
                                                                                                                                                                                                                                                            * Save username+id to the newly created campground


                                                                                                                                                                                                                                                            1. Open campgrounds.js from the routes folder and add the isLoggedIn middleware:
function isLoggedIn(req, res, next){
    if(req.isAuthenticated()){
        return next();
    }
    res.redirect("/login");
};
                                                                                                                                                                                                                                                               2. Add the call to the middleware to the new route and the create route:
   router.get("/new", isLoggedIn, function(req, res){...
   router.post("/", isLoggedIn, function(req, res){
                                                                                                                                                                                                                                                               3. Open up campground.js in models and add the author details:
   var campgroundSchema = new mongoose.Schema({
        name: String,
        image: String,
        description: String,
        author: {
            id: {
                type: mongoose.Schema.Types.ObjectId,
                ref: "User"
            },
            username: String
        },
        comments: [
            {
                type: mongoose.Schema.Types.ObjectId,
                ref: "Comment"
            }
        ]
    });
                                                                                                                                                                                                                                                                  4. Open campgrounds.js in routes and create an author object:
   var author = {
        id: req.user._id,
        username: req.user.username
    };
                                                                                                                                                                                                                                                                     5. Pass author into the newCampground object:
   var newCampground = {name: name, image: image, description: desc, author: author};
                                                                                                                                                                                                                                                                     6. Open show.ejs within views/campgrounds and update to display the author details under the description:
   <p>
        <em>Submitted by <%= campground.author.username %></em>
    </p>
                                                                                                                                                                                                                                                                        7. Restart the server


Video 22
##Editing Campground
                                                                                                                                                                                                                                                                        * Add Method-Override
                                                                                                                                                                                                                                                                        * Add Edit Route for Campgrounds
                                                                                                                                                                                                                                                                        * Add Link to Edit Page
                                                                                                                                                                                                                                                                        * Add Update Route
                                                                                                                                                                                                                                                                        * Fix $set problem


                                                                                                                                                                                                                                                                        1. Install method-override:
   Npm install method-override --save
                                                                                                                                                                                                                                                                        2. Require method-override in app.js:
   methodoverride         = require("method-override"),
            app.use(methodoverride("_method"));
                                                                                                                                                                                                                                                                           3. In campgrounds.js within routes/ create an Edit route:
   router.get(“/:id/edit”, function(req, res){
       res.render(“campgrounds/edit”);
   });
                                                                                                                                                                                                                                                                           4. Create edit.ejs:
   Touch views/campgrounds/edit.ejs
                                                                                                                                                                                                                                                                           5. Add some content, restart the server and go to url/campgrounds/:id/edit and see if your content is displayed.
                                                                                                                                                                                                                                                                           6. In campground.ejs in the routes folder update the Edit route to pass the campground id:
router.get("/:id/edit", function(req, res){
    Campground.findById(req.params.id, function(err, foundCampground){
        if(err){
            res.redirect("/campgrounds");
        } else {
            res.render("campgrounds/edit", {campground: foundCampground});
        }
    });        
});
                                                                                                                                                                                                                                                                              7. Then, in edit.js within views/campgrounds copy the form from views/campgrounds/new.ejs and paste it in, and then change the <form action=””> field:
   <form action="/campgrounds/<%= campground._id %>?_method=PUT" method="POST">
                                                                                                                                                                                                                                                                              8. Change the title to Edit Campground:
<h1 style="text-align: center;">
    Edit <%= campground.name %>
</h1>
                                                                                                                                                                                                                                                                                 9. Restart the server and go to the edit page for a campground:
   url/campgrounds/:id/edit
                                                                                                                                                                                                                                                                                 10. This should display the edit form.
                                                                                                                                                                                                                                                                                 11. Update the edit.ejs and change placeholder to value and its value:
<div class="form-group">
    <input class="form-control" type="text" name="campground[name]" value="<%= campground.name %>">        
 </div>
<div class="form-group">
    <input class="form-control" type="text" name="campground[image]" value="<%= campground.image %>">
</div>
<div class="form-group">
    <input class="form-control" type="text" name="campground[description]" value="<%= campground.description %>">
</div>
                                                                                                                                                                                                                                                                                    12. Update the Update Route in campgrounds.ejs in the routes folder:
// Update Route
router.put("/:id", function(req, res){
    // find and update the correct campground
    Campground.findByIdAndUpdate(req.params.id, req.body.campground, function(err, updatedCampground){
        if(err) {
            res.redirect("/campgrounds");
        } else {
            // redirect to show page
            res.redirect("/campgrounds/" + req.params.id);
        }
    });
});
                                                                                                                                                                                                                                                                                       13. And in the show.ejs found in views/campgrounds add a button to take you to the edit page and place it under the Submitted by field:
<a class="btn btn-warning" href="/campgrounds/<%= campground._id %>/edit">Edit</a>


Video 23
##Deleting Campgrounds
                                                                                                                                                                                                                                                                                          * Add Destroy Route
                                                                                                                                                                                                                                                                                          * Add Delete Button


                                                                                                                                                                                                                                                                                          1. Open campgrounds.js in the routes directory and add a Destroy route:
//Destroy route
router.delete(“/:id”, function(req, res){
   res.send(“You are trying to delete a campground”);
});
                                                                                                                                                                                                                                                                                          2. In views/campgrounds directory open the show.ejs file and add a delete button under the edit button:
<a class="btn btn-warning" href="/campgrounds/<%= campground._id %>/edit">Edit</a>
<form action="/campgrounds/<%= campground._id %>?_method=DELETE" method="POST">
    <button class="btn btn-danger">
        Delete
    </button>
</form>
                                                                                                                                                                                                                                                                                             3. Back in campgrounds.js in the routes directory rework the delete route:
router.delete("/:id", function(req, res){
    Campground.findByIdAndRemove(req.params.id, function(err){
        if(err){
            res.redirect("/campgrounds");
        } else {
            res.redirect("/campgrounds");
        }
    });
});
                                                                                                                                                                                                                                                                                                4. Restart the server and delete a campground, it should actually be deleted now.
                                                                                                                                                                                                                                                                                                5. Back in the show.ejs file add an id to the form for the delete button:
<form id="delete-form" action="/campgrounds/<%= campground._id %>?_method=DELETE" method="POST">
                                                                                                                                                                                                                                                                                                6. Open up the main.css file in url/public/stylesheets/main.css
                                                                                                                                                                                                                                                                                                7. Change the style of the delete button using the id you provided:
#delete-form {
    display: inline;
}
                                                                                                                                                                                                                                                                                                   8. Restart the server, the delete button should now sit beside the edit button.


Video 24
## Authorisation
                                                                                                                                                                                                                                                                                                   * User can only edit his/her campgrounds
                                                                                                                                                                                                                                                                                                   * User can only delete his/her campgrounds
                                                                                                                                                                                                                                                                                                   * Hide/show edit and delete buttons


                                                                                                                                                                                                                                                                                                   1. Open campgrounds.js found in the routes directory
   Goorm routes/campgrounds.js
                                                                                                                                                                                                                                                                                                   2. Write a new function that checks if a user is logged in and if a user matches the owner of a site:
function checkCampgroundOwnership(req, res, next){
    if(req.isAuthenticated()){
        Campground.findById(req.params.id, function(err, foundCampground){
            if(err){
                res.redirect("back");
            } else {
                // does the owner own the campground?
                if(foundCampground.author.id.equals(req.user._id)) {
                    next();
                } else {
                    res.redirect("back");
                }
            }
        });        
    } else {
        res.redirect("back");        
    }
}
                                                                                                                                                                                                                                                                                                      3. Add this middleware to the edit route and delete all unrequired code:
router.get("/:id/edit", checkCampgroundOwnership, function(req, res){
    Campground.findById(req.params.id, function(err, foundCampground){
        res.render("campgrounds/edit", {campground: foundCampground});        
    });
});
                                                                                                                                                                                                                                                                                                         4. Add the middleware to Update and Destroy routes too:
router.put("/:id", checkCampgroundOwnership, function(req, res){...
router.delete("/:id", checkCampgroundOwnership, function(req, res){...
                                                                                                                                                                                                                                                                                                         5. Go to views/campgrounds/show.ejs and add an if statement around the edit and delete buttons:
<% if(currentUser && campground.author.id.equals(currentUser._id)){ %>
    <a class="btn btn-warning" href="/campgrounds/<%= campground._id %>/edit">Edit</a>
    <form id="delete-form" action="/campgrounds/<%= campground._id %>?_method=DELETE" method="POST">
        <button class="btn btn-danger">
            Delete
        </button>
    </form>
<% } %>
                                                                                                                                                                                                                                                                                                            6. Restart the server and check to see if a user can edit any campgrounds they dont own.
At this point I had to clear my mongo database as an error was occurring when trying to edit a campground that had no owner.


Video 25
##Editing Comments
                                                                                                                                                                                                                                                                                                               * Add Edit route for comments
                                                                                                                                                                                                                                                                                                               * Add Edit button
                                                                                                                                                                                                                                                                                                               * Add Update route


                                                                                                                                                                                                                                                                                                               1. In comments.js found in the routes/comments directory add an edit route:
router.get("/:comment_id/edit", function(req, res){
    res.send("Edit route for comment");
});
                                                                                                                                                                                                                                                                                                                  2. Restart the server and navigate to an campground comment edit route:
/url/campgrounds/:id/comments/jibberish
                                                                                                                                                                                                                                                                                                                  3. The Edit route for comment message should be displayed.
                                                                                                                                                                                                                                                                                                                  4. Open show.ejs in the views/campgrounds directory
                                                                                                                                                                                                                                                                                                                  5. Add a button under the comment.text paragraph:
<a class="btn btn-xs btn-warning" href="/campgrounds/<%= campground._id %>/comments/<%= comment._id %>/edit">
    Edit
</a>
                                                                                                                                                                                                                                                                                                                     6. Now create an edit.ejs file in the views/comments directory and open it:
Touch views/comments/edit.ejs
Goorm views/comments/edit.ejs
                                                                                                                                                                                                                                                                                                                     7. Copy the contents from views/comments/new.ejs and paste in to views/comments/edit.ejs
                                                                                                                                                                                                                                                                                                                     8. Change the form for editing purposes:
<h1 style="text-align: center;">
    Edit Comment</h1>
<div style="width: 30%; margin: 25px auto;">
    <form action="/campgrounds/<%= campground_id %>/comments/<%= comment._id %>?_method=PUT" method="POST">
        <div class="form-group">
            <input class="form-control" type="text" name="comment[text]" value="<%= comment.text %>">        
        </div>
        <div class="form-group">
            <button class="btn btn-lg btn-primary btn-block">
                Submit
            </button>
        </div>
    </form>
    <a href="/campgrounds">Go back</a>
</div>
                                                                                                                                                                                                                                                                                                                        9. In comments.js update the update route:
router.put("/:comment_id", function(req, res){
Comment.findByIdAndUpdate(req.params.comment_id, req.body.comment, function(err, updatedComment){
        if(err){
            res.redirect("back");
        } else {
            res.redirect("/campgrounds/" + req.params.id);
        }
    });
});
                                                                                                                                                                                                                                                                                                                           10. Restart the server, you should be able to edit comments


Video 26
##Deleting Comments
                                                                                                                                                                                                                                                                                                                           * Add Destroy route
                                                                                                                                                                                                                                                                                                                           * Add Delete button


                                                                                                                                                                                                                                                                                                                           1. In /routes/comments/js write the following route:
router.delete("/:comment_id", function(req, res){
    //findByIdAndRemove
    Comment.findByIdAndRemove(req.params.comment_id, function(err){
        if(err){
            res.redirect("back");
        } else {
            res.redirect("/campgrounds/" + req.params.id);
        }
    });
});
                                                                                                                                                                                                                                                                                                                              2. In /views/campgrounds/show.ejs add a button under the edit button:
<form action="/campgrounds/<%= campground._id %>/comments/<%= comment._id %>?_method=DELETE" method="POST" class="delete-form" >
    <input type="submit" class="btn btn-xs btn-danger" value="Delete">
</form>
                                                                                                                                                                                                                                                                                                                                 3. Change the delete-form id in /public/stylesheets/main/css from an id to a class:
.delete-form {
    display: inline;
}


Video 27
##Authorisation
                                                                                                                                                                                                                                                                                                                                    * User can only edit his/her comments
                                                                                                                                                                                                                                                                                                                                    * User can only delete his/her comments
                                                                                                                                                                                                                                                                                                                                    * Hide/Show buttons
                                                                                                                                                                                                                                                                                                                                    * Refactor middleware


                                                                                                                                                                                                                                                                                                                                    1. Copy the middleware from /routes/campgrounds.js for checking ownership and paste in to /routes/comments.js and edit to reflect its use for comments:
function checkCommentsOwnership(req, res, next){
    if(req.isAuthenticated()){
        Comment.findById(req.params.comment_id, function(err, foundComment){
            if(err){
                res.redirect("back");
            } else {
                // does owner own the comment?
                if(foundComment.author.id.equals(req.user._id)) {
                    next();
                } else {
                    res.redirect("back");
                }
            }
        });        
    } else {
        res.redirect("back");        
    }
}
                                                                                                                                                                                                                                                                                                                                       2. Add the middleware to routes:
router.get("/:comment_id/edit", checkCommentsOwnership, function(req, res){...
router.put("/:comment_id", checkCommentsOwnership, function(req, res){...
router.delete("/:comment_id", checkCommentsOwnership, function(req, res){...
                                                                                                                                                                                                                                                                                                                                       3. In /views/campgrounds/show.ejs add another if statement around the comment buttons:
<% if(currentUser && comment.author.id.equals(currentUser._id)){ %>
    <a class="btn btn-xs btn-warning" href="/campgrounds/<%= campground._id %>/comments/<%= comment._id %>/edit">
        Edit
    </a>
    <form action="/campgrounds/<%= campground._id %>/comments/<%= comment._id %>?_method=DELETE" method="POST" class="delete-form" >
        <input type="submit" class="btn btn-xs btn-danger" value="Delete">
    </form>
<% } %>
                                                                                                                                                                                                                                                                                                                                          4. Create a new directory called middleware:
mkdir/middleware
                                                                                                                                                                                                                                                                                                                                          5. Create a new file called index.js in middleware:
Touch middleware/index.js
                                                                                                                                                                                                                                                                                                                                          6. Open up middleware/index.js and require all objects, create an object for middleware, create an export, and copy and paste all the middleware from the files in routes and paste them here:
var Campground = require("../models/campground");
var Comment = require("../models/comment");


// all the middleware goes here
var middlewareObj = {};


middlewareObj.checkCampgroundOwnership = function(req, res, next) {
    if(req.isAuthenticated()){
        Campground.findById(req.params.id, function(err, foundCampground){
            if(err){
                res.redirect("back");
            } else {
                // does owner own the campground?
                if(foundCampground.author.id.equals(req.user._id)) {
                    next();
                } else {
                    res.redirect("back");
                }
            }
        });        
    } else {
        res.redirect("back");        
    }
};


middlewareObj.checkCommentOwnership = function(req, res, next){
    if(req.isAuthenticated()){
        Comment.findById(req.params.comment_id, function(err, foundComment){
            if(err){
                res.redirect("back");
            } else {
                // does owner own the comment?
                if(foundComment.author.id.equals(req.user._id)) {
                    next();
                } else {
                    res.redirect("back");
                }
            }
        });        
                } else {
        res.redirect("back");        
    }
};


middlewareObj.isLoggedIn = function(req, res, next){
    if(req.isAuthenticated()){
        return next();
    }
    res.redirect("/login");
};


module.exports = middlewareObj
                                                                                                                                                                                                                                                                                                                                             7. Update all the route files with a require for middleware:
middleware         = require("../middleware")
                                                                                                                                                                                                                                                                                                                                             8. Restart the server and check everything works correctly


Video 28
##Adding in Flash!
                                                                                                                                                                                                                                                                                                                                                * Install and configure connect-flash
                                                                                                                                                                                                                                                                                                                                                * Add bootstrap alerts to header


                                                                                                                                                                                                                                                                                                                                                1. Install connect-flash to your project:
Npm install --save connect-flash
                                                                                                                                                                                                                                                                                                                                                2. Require connect flash and use it:
Var flash = (“connect-flash”);
app.use(flash());
                                                                                                                                                                                                                                                                                                                                                3.
