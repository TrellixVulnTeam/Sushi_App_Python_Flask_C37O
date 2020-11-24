# MySushiRecipes

This is a full stack CRUD application which allows a user to register, login and logout to create, read, edit, update and delete recipes.
This web application has been created using Python 3.7 for the back-end with Flask which is a Python-based microframework. MongoDB Atlas has been used for the database. Bootstrap has been implemented for the front-end.

The purpose of this project is for educational purposes and serves as the Milestone 4 Project in the Data Centric Development module of the Full Stack Software Development Program at the Code Institute.

The live project can be viewed on heroku at [link](https://sushi-sandwich.herokuapp.com) here.

## UX
I wanted to develop a breathable app for anyone to store and retrieve sushi recipes. There is a login feature which is explained more in *CRUD Functionality*. **Layout design**: the site theme is based on the [colour palette](https://github.com/fion21/new-flask-1/blob/master/planning/wireframes/color_scheme.PNG) which includes an orange and some blues and greys. This was brought in from my main background image of red caviar on a blue-grey background, which I subsequently left out as I wanted to concerntrate on readability over photography. The new screen is black background with orange text, which is much clearer. **Typography**: As to design I was following Swiss design principles from the 1960s, which sans-serif fonts were derived from, and necessary to use on the app to avoid pixelization from a serif font. The user has to see the words to navigate well. The image is not present on the create, edit, delete and single recipe (full page view) as it reads better on smaller screens that way. The font is is *orangered* which is the pre-determined html standard font colour.

## Wireframes
The app works 100% on all phones and screens.
[Desktop](https://github.com/fion21/new-flask-1/blob/master/planning/desktopviewindex.PNG) [Ipad](https://github.com/fion21/new-flask-1/blob/master/planning/tabletverticalviewindex.PNG) [Iphone6](https://github.com/fion21/new-flask-1/blob/master/planning/iphone6.PNG)


## CRUD Functionality

### CREATE
Users whether regisistered or not can view a list of recipes already on the database. These recipe lists are displayed on the index page and some are also on the recipes page and can be searched and retrieved by keywords via the search bar located on *recipes.html*. A user can chose to register, then as a logged in user can add a recipe, update and delete their own recipies added to the database.

### READ 
Thus users to the site can read a selection of recipes from the database collection via those displayed mentioned above. Furthermore, if a user presses the "more info" button they can view a recipe as a single page with all the details. The idea was provided by the Task Manager project at CI.

The search bar feature within the `recipes.html` allows viewers to search for a term as a filter via a keyword such as a tag to read from the collection and the results of which will be displayed after the search button is depressed.

### UPDATE 

This is only available to registered/logged-in users a hashed password security feature using the *bycrypt* feature from Flask. A user has to fill in all the fields to be able to add a new recipe.

I used the code of *update one* in the `app.py` as part of the edit_recipe route as *recipe_db = mongo.db.recipes.find_one_or_404({'_id': ObjectId(recipe_id)})* which is also translated via code in `{{ form.submit() }}`,  on the `edit_recipe.html` originating from `forms.py`. There is no update link on the menu bar, the page appears as an option to view from the `Add Recipe` page. Checking was done by simply logging into MongoDB itself to check the recipe list had been updated, then a browser refresh on the front-end. On successful editing the user is returned to the homepage.

### DELETE 

This is accessed from viewing a recipe that the author has created, (found by searching it in the search bar or finding it listed on the whole list of recipes it appears in order of insertion, usually this would be at the end of the list) and pressed more info on similar functionality to the `update` button. If a user presses the delete button there is a flash message warning beforehand. The code is handled with `forms.py` Similar logic to that described for *update one*, here it is `recipes_db.delete_one({...etc` in`app.py`. On successful deletion the user is returned to the homepage.

#### Other Features
A `logout` feature is available on the navbar and allows the logged in user to logout of their current session, which will create a redirect to the homepage. `Views`: Shows in incremental value the number of times a full recipe page is called.

#### Features Left to Implement
Have a `likes` button on each recipe. Charting data vizualization of `views` popularity via D3.JS. Follwers and to 'follow other users' functionality, plus a user avatar to add to the welcome username once they have logged in.

## Technologies Used
* [Python 3.7](https://www.python.org/download/releases/3.0/) Language
* [Flask 1.0.2](http://flask.pocoo.org/) Web framework
* [HTML5](https://en.wikipedia.org/wiki/HTML5) Webpage markup language
* [CCS3](https://www.w3.org/Style/CSS/) Styling and layout
* [Bootstrap](https://www.getbootstrap.com) Front-end component library
* [JavaScript](https://www.javascript.com/) with jQuery and HTML scripts 
* [jQuery](https://jquery.com/) Navbar dropdown
* [Flaticon](https://www.flaticon.com/authors/smashicons) URL Sushi tab icon
* [Jinja2](https://palljtsprojects.com/p/jinja/) templating engine for Python 
* [MongoDB](https://www.mongodb.com/) Database source file

## Testing
#### Responsiveness
The UX fonts and card feature, plus the navbar and hamburger are all scalable, responsive and easy to navigate throughout the site.
The site follows responsive design and works for desktop viewing on browsers: google chrome, firefox and explorer as well as mobiles having checked the rending on the iPhone: from 5 to X, Samsung Galaxy: all versions, iPad: all versions, Google: Pixel 2 and 3.

#### Coding Tests
The HTML, CSS code for this application has been checked via W3C Markup and reported no significant errors. The Python code has been tested via working on the code in stages and running the app on the front-end. Some pep8 coding from VS code helped by providing the correct indentation, but on other times the jinja templating would stay on the same line, which was a hinderence. Back-end terminal testing and running were standard procedures throughout the app development. New tests have been added to test the back-end functionality.

#### Testing Template Views
Routes have been created in flask which bring in a template view on the front-end. Elements of which have been run in the browser and refactored to the final stage for deployment.

#### Database Testing
The database is set up in Mongodb and is comprised of a list of recipe elements including the user's added recipes which have page view increments. The most difficult aspect was getting familiar with the interface and finding the connection string. This took me a lot of time to understand and I eventually worked out how to set the os.environ to Mongodb so that the actual string is not displayed in the github repository. The connection string was added to the config vars on Heroku which is accessible only to the owner of the site.

## Deployment
Installing the project can be done via the following stages:
````
Download this repository via the green download button on the head of this page
Login to Heroku.com presumming you have pre-registered
On the Heroku dashboard click on Create New App
Enter a unique name and your region (nearest), click Create
Go back to your command line terminal where your app is, enter heroku
then heroku login, enter your credentials for Heroku
In your terminal (using powershell on windows 10, may differ slightly for Mac etc.)
pip freeze --local > requirements.txt
echo web: python run.py > Procfile
git add .
git commit -m "initial commit"
git push -u heroku master
heroku ps:scale web=1
Set debug to False in production/live within the main file (eg app.py)
In your heroku app set the config vars to IP : 0.0.0.0, 
PORT : 5000 and MONGO_URI :mongodb://[yourusername]:[youpassword]
@the string that your got from mongodb.com:something/<whatever the collection name is>.
Find the More tab> Restart all Dynos
This should see the app live at https://<whatever you called it>.herokuapp.com/
 ````
 
## Credits and Acknowledgements
**Stack Overflow**, **CI** for coding issues

**Miguel Grinberg** Flask Mega Tutorial

**Spencer Bariball** tutor at Code Institute

**Shalabh Aggarwal** Flask Framework Cookbook

## Images
All images used in this application are copyright of their respective website owners, the links will take viewers to their respective sites, those being [Journey of Japan](https://journey-of-japan.com), [Tenkaichi](https://tenkaichi.com.sg), [Villagevoice](http://www.villagevoice.com/wp-content/uploads/2017/01/nyv_food_20161216_sugarfish_bhawks_008-1366x911.jpg) and [Seth Lui](https://sethlui.com).

## License
This project is released under the [MIT licence](https://github.com/fion21/new-flask-1/blob/master/LICENSE).

## Disclaimer
The purpose of the project is for educational purposes only.

If you found this code useful, there is a way to support me, this is a cool way to say thank you:

<a href="https://www.buymeacoffee.com/fion34" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

