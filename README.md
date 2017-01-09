##Full Stack Web Development - Coursera Specialization
#### Module 3 - Front-End Web Javascript Frameworks: AngularJS
###### by **The Hong Kong University of Science and Technology**
###Getting Started with AngularJS

### The Power of Bower

* Install bower on your PC (you're going to need to have npm already installed):

```
npm install -g bower
```

* Open a terminal window and go to the conFusion folder. Then at the prompt type:

```
bower install
```
![Installing Bower](img/bower-install.png?raw=true "Installing Bower using CMD")

This will result in Bower fetching Bootstrap, JQuery, Font Awesome and Angular files for us and putting them into the bower_components folder.

* Once Bower completes the installation, your project folder is now all set

You will note that the file is already configured to include the Bootstrap CSS files and other CSS files from the folder. 

### Examining menu.html

* Open the project folder in your favorite text editor, and then open menu.html file to view its contents.

#### Adding Angular to the File

* We will now set up the page to use Angular by including the Angular JavaScript files into the menu.html page by adding the following code to the bottom of the page, just before the closing body tag:

```html
<script src="../bower_components/angular/angular.min.js"></script>
```

Note that we are using the Angular files that Bower has downloaded for us.

#### Configuring the Angular Application

Next we configure our web page to be an Angular application. Go to the `<html>`tag at the top of the page and then add the *ng-app* angular directive to it to configure the page to be an Angular application. This will bootstrap the Angular application on the page:

```html
<html lang="en" ng-app>
```

####

Adding Data using ng-init

* Next go to the content row in the body of the page, and add some data to be used within the application, by using the *ng-init* directive as follows:

```html
<div class="row row-content"
                      ng-init="
                         dish=
                         {
                           name:'Uthapizza',
                           image: 'images/uthapizza.png',
                           category: 'mains',
                           label:'Hot', 
                           price:'4.99',
                           description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
                           comment: ''
                        }">
```

This includes a JavaScript object named dish into the code. Browse the contents of this object.

#### Adding Menu Item using Media Object

* We will now make use of the Bootstrap media object to introduce a menu item into the inner column div as follows:

```html
<div class="col-xs-12">
    <div class="media">
        <div class="media-left media-middle">
            <a href="#">
                <img class="media-object img-thumbnail"
                ng-src={{dish.image}} alt="Uthappizza">
            </a>
        </div>
        <div class="media-body">
            <h2 class="media-heading">{{dish.name}}
            <span class="label label-danger">{{dish.label}}</span>
            <span class="badge">{{dish.price | currency}}</span></h2>
            <p>{{dish.description}}</p>
        </div>
    </div>
</div>
```
Note the use of Angular expressions with the curly braces {{ ... }} to include various properties of the JavaScript object to construct the menu item.

Also, in this code, note the use of the Angular `currency` filter to display the price within the badge.

#### Examining Two-way Binding

* Note the presence of a property called comment in the dish object. We will use two-way data binding feature of Angular to update this comment from an input box on the page, and see the updated comment immediately reflected to the web page.

* Update the media object in the column div as follows:

```html
<div class="col-xs-12">
    <div class="media">
        . . .
        <p>{{dish.description}}</p>
        <p>Comment: {{dish.comment}}</p>
        <p>Type your comment:
        <input type="text" ng-model="dish.comment"></p>
    </div>
</div>
```

We are adding three new lines with the `<p>`comment: ... `</p>` and the `<p>`Type your comment: ... `</p>` with the input box to the HTML code.

#### Object Array and ng-repeat

* We will now update the ng-init to contain an array of JavaScript objects as follows:

```html
<div class="row row-content" ng-init="
    dishes=[
               {
                    name:'Uthapizza',
                    image: 'images/uthapizza.png',
                    category: 'mains',
                    label:'Hot',
                    price:'4.99',
                    description:'A unique combination of Indian Uthappam (pancake) and Italian pizza, topped with Cerignola olives, ripe vine cherry tomatoes, Vidalia onion, Guntur chillies and Buffalo Paneer.',
                    comment: ''
                },
                {
                    name:'Zucchipakoda',
                    image: 'images/zucchipakoda.png',
                    category: 'appetizer',
                    label:'',
                    price:'1.99',
                    description:'Deep fried Zucchini coated with mildly spiced Chickpea flour batter accompanied with a sweet-tangy tamarind sauce',
                    comment: ''
                },
                {
                    name:'Vadonut',
                    image: 'images/vadonut.png',
                    category: 'appetizer',
                    label:'New',
                    price:'1.99',
                    description:'A quintessential ConFusion experience, is it a vada or is it a donut?',
                    comment: ''
                },
                {
                    name:'ElaiCheese Cake',
                    image: 'images/elaicheesecake.png',
                    category: 'dessert',
                    label:'',
                    price:'2.99',
                    description:'A delectable, semi-sweet New York Style Cheese Cake, with Graham cracker crust and spiced with Indian cardamoms',
                    comment: ''
                }
           ]">
```
Next we will update the code in the column div to create a list of media objects so that the menu can be displayed on the page constructed from the JavaScript object array. We take the help of the *ng-repeat* directive for this. Update the code as follows:

```html
<div class="col-xs-12">
    <ul class="media-list">
        <li class="media" ng-repeat="dish in dishes">
            <div class="media-left media-middle">
                <a href="#">
                    <img class="media-object img-thumbnail"
                    ng-src={{dish.image}} alt="Uthappizza">
                </a>
            </div>
            <div class="media-body">
                <h2 class="media-heading">{{dish.name}}
                <span class="label label-danger">{{dish.label}}</span>
                <span class="badge">{{dish.price | currency}}</span></h2>
                <p>{{dish.description}}</p>
                <p>Comment: {{dish.comment}}</p>
                <p>Type your comment:
                <input type="text" ng-model="dish.comment"></p>
            </div>
        </li>
    </ul>
</div>
```

####Note

 It is interesting to note that you have not written a single line of JavaScript code for this exercise, but still get a lot of dynamic functionality in the page.

#### Updated: January-9th-2017
