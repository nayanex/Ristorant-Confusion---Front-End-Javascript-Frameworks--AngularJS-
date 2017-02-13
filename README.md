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
![Installing Bower](app/images/bower-install.png?raw=true "Installing Bower using CMD")

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

![ng-repeat usage result](app/images/usage-of-ng-repeat.png?raw=true "Final result after the usage of ng-repeat")

####Note

 It is interesting to note that you have not written a single line of JavaScript code for this exercise, but still get a lot of dynamic functionality in the page.

## Angular Modules and Controllers

Now we are going to use Angular modules and controllers to organize our Angular application and separate the data from the layout of the page. 

#### Creating Angular Module

* First, update the ng-app with a name for the module that will define the application as follows:

```html
<html lang="en" ng-app="confusionApp">
```

This means that we now need to define an Angular module named confusionApp*. We will do this next.

* First, go to the bottom of the page and add the following code just before the body closing tag, to create the Angular module:

```html
<script>
        var app = angular.module('confusionApp',[]);
    </script>
```

* Next we will add a controller to this app as follows:

```html
 <script>
        var app = angular.module('confusionApp',[]);
        app.controller('menuController', function() {
        });
    </script>
```

* Then, we will shift the dishes JavaScript object array from the ng-init to the controller. Cut out the ng-init from the div completely, and add the following code to the Controller:

```javascript
 var dishes=[{
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
            }];

            this.dishes = dishes;
```
#### Attaching the Controller

* Modify the row class as follows to add the controller to the div:

```html
<div class="row row-content" ng-controller="menuController as menuCtrl">
```

This adds the menuController as the controller for this div, and also assigns an alias to the controller as menuCtrl.

* Next update, the list tag as follows:

```html
 <li class="media" ng-repeat="dish in menuCtrl.dishes">
```

* The web page itself will show no change, except that the code is now factored out into a controller.

## Angular Filters

Now we are going to create a menu that either presents the whole menu, or parts of the menu as selected by the user. The user will be able to:

* Use Angular filters to filter items based on user's selection
* Use Bootstrap navigation tabs in conjunction with AngularJS
* Make use of the ng-class and ng-click Angular directives

#### Setting up Tabbed Navigation for the Menu

* We will now take the help of Bootstrap tabs to set up a tabbed navigation for the menu. We will construct four tabs to display all the menu items, appetizers, mains, and Desserts based on user's selection. Add the following code to the column div, just before the `<ul>` containing the menu items:

```html
<ul class="nav nav-tabs" role="tablist">
    <li role="presentation">
        <a aria-controls="all menu" role="tab">The Menu</a>
    </li>
    <li role="presentation">
        <a aria-controls="appetizers" role="tab">Appetizers</a>
    </li>
    <li role="presentation">
        <a aria-controls="mains" role="tab">Mains</a>
    </li>
    <li role="presentation">
        <a aria-controls="desserts" role="tab">Desserts</a>
    </li>
</ul>
```
You will see the four tabs set up by the above navigation. However clicking on the tabs does not do anything, since we have not set up the logic to activate the tabs.

* Next, enclose the menu `<ul>` inside a `<div>` with class *tab-content*. Also appy the *tab-pane fade in active* class to the ul as shown below:

```html
    <div class="tab-content">
        <ul class="media-list tab-pane fade in active">
            . . .
        </ul>
    </div>
```

Keep the `<li>` item in the `<ul>` as is.

#### Activating the Navigation Tabs

* We will now activate the tabs so that the user can select any of the four tabs. We need to do this by adding some functions to the menucontroller and then use the functions to activate the tabs when selected. First we add a variable named tab to the menucontroller code as follows:

```javascript
    this.tab = 1;
```
Add this as the first statement in the menu controller. Note that the tabs are given indices 1 .. 4. The variable tab will keep track of the currently active tab. By default this will be assigned as the first tab. Obviously, the remaining tabs will be numbered 2 .. 4.

* Whenever the user clicks on a tab, we need to activate that tab. To do this, we take the help of the ng-click Angular directive. This directive will be fired when the user clicks on the tab. To do this, we will add an ng-click directive to every <a> tag within the tabs as follows:

```html
<ul class="nav nav-tabs" role="tablist">
    <li role="presentation">
        <a ng-click="menuCtrl.select(1)" aria-controls="all menu"              
           role="tab">The Menu</a>
    </li>
    <li role="presentation">
        <a ng-click="menuCtrl.select(2)" aria-controls="appetizers"
           role="tab">Appetizers</a>
    </li>
    <li role="presentation"> 
        <a ng-click="menuCtrl.select(3)" aria-controls="mains"
           role="tab">Mains</a>
    </li>
    <li role="presentation">
        <a  ng-click="menuCtrl.select(4)" aria-controls="desserts"
            role="tab">Desserts</a>
    </li>
</ul>
```

Note that the complete code is given above, just in case you wish to cut and paste the code. Note how the *ng-click* directives are introduced using 
*ng-click="menuCtrl.select(i)"*.

* Upon clicking of the tab, the ng-click directive will cause the execution of the select() function in the menucontroller. Next, we need to implement the select() function. Add the following code to the menucontroller to implement the select() function:

```javascript
this.select = function(setTab) {
    this.tab = setTab;
}
```

This function will set the tab variable to the selected tab index.

Next we take the help of the *ng-class* directive in order to add the Bootstrap *active* class to the selected tab. To do this modify the `<ul>` for the tabs as follows, where you can clearly see the ng-class directive being used:

```html
<ul class="nav nav-tabs" role="tablist">
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(1)}">
        <a ng-click="menuCtrl.select(1)" aria-controls="all menu"
           role="tab">The Menu</a>
    </li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(2)}">
        <a ng-click="menuCtrl.select(2)" aria-controls="appetizers"
           role="tab">Appetizers</a>
    </li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(3)}">
        <a ng-click="menuCtrl.select(3)" aria-controls="mains"
           role="tab">Mains</a>
    </li>
    <li role="presentation" ng-class="{active:menuCtrl.isSelected(4)}">
        <a  ng-click="menuCtrl.select(4)" aria-controls="desserts"
            role="tab">Desserts</a>
    </li>
</ul>
```
Note that for each of the `<li>` elements, we introduced the *ng-class="{active:menuCtrl.isSelected(i)}"* directive. This directive will apply the active class to that element, if the function on the right (that specifies a condition) evaluates to true.

* Next, we need to implement the isSelected() function in the menucontroller. Add the following code to implement this function in the menucontroller:

```javascript
this.isSelected = function (checkTab) {
    return (this.tab === checkTab);
}
```

This function will return true if the current tab is the same as the tab specified in the function parameter.

* Now the selection of the tabs, and activating the selected tab should work correctly. However no matter which tab is selected, you will still see the list of all menu items.

#### Using Angular Filter

Next we take the help of the Angular filter to select only those items from the menu corresponding to each tab. Note that each dish object already has a property named *category*. We can use this to filter our items.

We will now set up the filters on the list items in the menu as follows:

```html
    <li class="media" ng-repeat="dish in menuCtrl.dishes | filter:menuCtrl.filtText">
```

The above modification implies that the filter will use the variable filtText from the menucontroller to filter the items from the dishes array.

* Next we need to introduce the filtText variable in the menucontroller and have a way of setting it to the appropriate value when the various tabs are selected. To do this, add the following code to the menucontroller:

```javascript
    this.filtText = '';
```

We are specifying that initially since the first tab is selected as default, the filtText should not filter out any item from the menu. Hence filtText is set to the empty string.

* Then, whenever a tab is selected, the filtText value should be updated to reflect the selected tab and the corresponding filter value to be applied. To do this, modify the select() function as follows:

```
    this.select = function(setTab) {
        this.tab = setTab;
        if (setTab === 2)
            this.filtText = "appetizer";
        else if (setTab === 3)
            this.filtText = "mains";
        else if (setTab === 4)
            this.filtText = "dessert";
        else
            this.filtText = "";
    }
```
Note that using the if statements, we are able to set the filtText to the appropriate value.

* Now the application should show the correctly filtered results from the menu items when the tabs are selected.

## Dish Details

#### Task 1

In this task you will display the information about the dish in the page. To do this, you need to complete the following:

* Set up the row to use the dishDetailController
* Use the Bootstrap Media Object to display the information about the dish.

### Task 2

In this task you will display all the comments from the dish JavaScript object as a list of comments underneath the dish description on the page. To do this, you need to complete the following:

* Use the Bootstrap blockquote class to format the comments. The author and the date information should be in the footer of the blockquote.
* The date field should be formatted using the Angular date filter.
* The comments are constructed by iterating over the comments array using the appropriate ng- directive.

### Task 3

In this task you will add the filter to the comments section so that the comments can be ordered according to user's selected criteria. You will use the orderBy filter in Angular to achieve this. To do this, you need to complete the following:

* Set up an input field that enables the user to type in their ordering criteria: *author*, *date* and *rating*. These could be prefixed with a '-' sign to indicate reverse ordering.
* Set up the orderBy filter on the comments so that the comments will be ordered as per the user's specification.

#### Updated: February-8th-2017
