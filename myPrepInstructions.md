# What I Need To Do

1. Make a list of screens you think you will need
2. Match these to Use Cases
3. Draw up a screen
4. Use draw.io to design a screen
5. Draw up a diagram of navigation
6. Use draw.io to draw up as many screens as you can
8. Start initialising the project
9. Install modules for the app <br>
  ````npm install express ejs body-parser mongoose passport passport-local passport-local-mongoose express-session method-override --save````
10. Create a views folder and create your landing page as an .ejs document.  Create register and login pages as .ejs documents if required.
11. Create a partials folder within views and include the header and footer.ejs files here.
12. In the views folder create folders for element of the project.  Assuming this is Questions only for now.
13. In the Questions folder create .ejs files for:
  * index - shows all questions, create an array full of stuff to set up displaying all of them.  change this to database entries later
  * new - form for creating a new question and its answers
  * edit - same form as new, but for updating/editting a question and its answers
  * show - Non-editable page that shows a specific question and its answers.  This page will have if statements that show answers if a user has a permission other than "minimum", and edit/delete buttons if the user has the "most" persmissions
14. Back at the top level create another folder called models and create what modelsas .js files, that are needed for creating documents in a database:
  * users
  * questions
  * others... you might need comments or something extra depending on the brief
15. Think about what the users are required to see when building the schema.  Users might just be username/email and password.  Questions might just be questions and answers.
16. Create the middleware folder and it's index.js file.
17. Write some functions for checking if a user is logged in, and one to check what permission level they have set?
18. Create a routes folder, containing index.js for registering (if required) and logging in.  And then a questions.js route page for restful routing.
19. Create a public folder, with a stylesheets folder in, and then add main.css for styling.  **Don't spend long on this, get everything working first!**
20. Test everything is working as you go along!  Create a seed.js file that populates some data so you can test things out.  Show this testing!
21. Once everything is working, write up some user instructions, plan next phases, make it look pretty. Hand it over.
