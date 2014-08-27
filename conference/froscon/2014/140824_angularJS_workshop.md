# [Sebastian Mancke](http://programm.froscon.de/2014/events/1331.html)

* [slides](http://smancke.github.io/angularjs-intro/)
* [source](https://github.com/smancke)

* core concept

* mvc framework
* focused on singe page apps
* browser based templating
* test driven based
* supports/restricts you to write understandable code
* declarative binding (variable gets synced in two ways, thats the main feature of knockout.js)

# delimitation

* to jquery: declarativ, less hacking in the dom
* to knockout: contains a lot more
* to emberjs: same but different

# basics

* data-ng-app = ng-app = ngApp 
* data-ng-app is html conform

    <html data-ng-app="presentation">
    // ...
    <!-- do not prefix your code with "$" -->
    <script src="./lib/jquery.min.js"></script>
    <script src="./lib/angular.min.js"></script>
    <script>
        var application = angular.module('presentation', []);
    </script>

# template

## bindings

* "data-ng-app" initialize the application
* angular.min.js around 97k
* initialization time with jquery around 250ms (so not for very fast pages)
* uses small version of jquery

    <!-- {{demo}} is binding to a variable in the current scope -->
    <h1 lang="en">Simple bindings {{demo}}</h1>
    <div lang="de" style="display: none;">
        AngularJS enables direct templating in the browser
    </div>
    <div lang="en">
        AngularJS utilizes templating in the browser.
    </div>
    <p>Demo: {{demo}}</p>
    <input type="text" data-ng-model="demo"> <!-- bind (data) model to variable demo in current scope -->

### other helpers for binding

* data-ng-model
* data-ng-if
* data-ng-init

    <input type="checkbox" data-ng-model="state" data-ng-true-value="enabled"
        data-ng-false-value="disabled" data-ng-init="state='enabled'">
    <p>State: {{state}}</p>
    <select data-ng-model="state"> <!-- model do not has to have a real object implementation behind, here it "just" represents the variabl -->
        <option value="enabled">enabled</option>
        <option value="disabled">disabled</option>
    </select>
    <h3 data-ng-if="state != 'disabled'">AngularJS is cool!</h3>

### and more binding examples

* data-ng-class
* data-ng-style

    <input type="checkbox" data-ng-model="everyThingOk" data-ng-init="everyThingOk=true">
    <span data-ng-class="{'alert-success':everyThingOk, 'alert-danger':!everyThingOk }">This is the message</span>

    <button data-ng-click="myStyle={color:'red', 'font-weight':'bold'}">red</button>
    <button data-ng-click="myStyle={'color':'blue'}">blue</button>
    <span data-ng-style="myStyle">Sample text, myStyle={{myStyle}}</span>

# controller

* defines the scope for variables
* initialization code will be executed directly
* functions are stored in the $scope variable
* dependency injection baby :-)

    //the "$" is important, thanks to dependency injection, angular is searching for "$scope" and injects this
    application.controller('BindingControllerOne', function($scope) {
        console.log('init controller ..');
        $scope.answer = 42;
        $scope.anyFunction = function () {
            $scope.question = ' is the answer!';
    }});

    <div data-ng-controller="BindingsCtrl1">
        <button type="button" data-ng-click="anyFunction()">Click me</button>
        <h3>{{answer}}{{question}}</h3>
    </div>

# formatter

* used for displaying numbers, for example currencies

    application.controller('FormatterCtrl', function($scope) {
        $scope.number = 42;
        $scope.time = new Date();                
    });

    application.filter('custom', function() {
        return function(value) {
        return '-' + value +'.00 formatted!';
    }
    });

    <!-- angular gets current local from browser? -->
    <div>Number: {{number | number:4}}</div>
    <div>Currency: {{number | currency}}</div>
    <div>Custom: {{number | custom}}</div>
    <div>Time: {{time | date:'medium'}}</div>

# tables

* data-ng-repeat

    application.controller('RepeatController', function($scope) {
        $scope.persons = [
        {first: 'Arthur', last: 'Dent'},
        {first: 'Zaphod', last: 'Beeblebrox'},
        {first: 'Marvin', last: 'robot'},
    ]});

    <table data-ng-controller="RepeatController">
        <tr data-ng-repeat="person in persons">
            <td>{​{person.first}}</td> <td>{​{person.last}}</td>
        </tr>
    </table>

# filtering and sorting

    <select data-ng-model="orderField">
        <option value="first">first</option>
        <option value="last">last</option>
    </select>
    <input type="text" data-ng-model="filterText">
    <tr data-ng-repeat="person in persons | orderBy:orderField | filter: filterText">

# scops

* are agularjs data objects holding the model
* every function call is done in the context of that scope
* child scops
    * can be nested along the dom hierarchy
    * nested scops inherit properties of parent scope
    * self defined properties are not visible outside (no scope messup)
* isolated scops
    * do not inherit parent properties
    * they can bind properties of parent scope through mapping

## observe scope changes

    $watch(watchExpression, [listener], [objectEquality]); 

### observing items of a collection

    $scope.$watch('backlogItems', function(newValue, oldValue) {
        console.log('user has modified "$scope.backlogItems" ..');
        //...
    }, true);

## manipulating data

* has to take in place of the angularJS context (to trigger view update)
* can be forces by '$scope.$apply()'

### most common

* window.setTimeout();
* native dom events
* integration of existing components
* use "data-ng-attr-" to initialize values correct (prevent errors happens when value is null/not initialized yet)

# services

    application.service('myService', function() {
        this.sayHello = function() {
            return 'hello, world';
        };
    });

# factories

    application.factory('myFactory', function() {
        return {
            sayHello: function () {
                return 'Hello, world';
            }
        }
    });

# dependency injecton in controller

    application.controller('DependencyInjection1', function($scope, helloService, helloFactory) {
        console.log(helloService.sayHello())
        console.log(helloFactory.sayHello());
    });
    //does the same and is robust against minifying
    application.controller('DependencyInjection2', ['$scope', 'helloService', 'helloFactory', 
        function($scope, helloService, helloFactory)
        {
            console.log(helloService.sayHello())
            console.log(helloFactory.sayHello());
    }]);

# extensions or directives

    application.directive('name', function () {
        return {
            restrict: //..
            template: //..
            replace: //..
            templateURL: //..
            transclude: //..
            link: //..
            scope: //..
        }
    });

## usable as

* element

    application.directive('myDirective', function () {
        return {
            restrict: 'E',
    }});
    <data-my-directive ...></data-my-directive>

* attribute

    application.directive('myDirective', function () {
        return {
            restrict: 'A',
    }});
    <div data-my-directive=".." ...></div> or <div data-my-directive></div>

* class

    application.directive('myDirective', function () {
        return {
            restrict: 'C',
    }});
    <div class="data-my-directive" ...></div>
* combinations are allowed also

### as templates

    application.directive('myButton', function () {
        return {
            restrict: 'E',
            template: '<button type="button">click me</button>',
    }});
    <my-button/>
    <!-- would become -->
    <my-button><button type="button">click me</button></my-button>
    <!-- with 'replace: true', the surrounding tag would be replaced also -->

* can be defined externally
* coverd by template cache 

    templateULR: '/myButton.html'
    <!-- or -->
    <script type="text/ng-template id="/myButton.html">
        <button type="button">click me</button>
    </script>

### enclosed templates

    application.directive('myButton2', function () {
        return {
            restrict: 'E',
            transclude: true, //thats the magic trigger
            template: '<button type="button">\  //template header
            <span data-ng-transclude></span></button>',  //template footer
    }});
    <my-button2>That's the <strong>label!</strong><my-button2/>

## execute all other code by using 'link'

* dom manipulation
* registration of event listener
* integration of other libraries

    //code is executed per "triggering" meaning multiple times
    application.directive('myLinkedButton', function () {
        return {
            restrict: 'E',
            template: '<button type="button">click me</button>',
            link: function (scope, elem, attrs) {
                elem.on('click', function() {
                alert(attrs.message);
        });
    }}});
    <my-button message="42, ist the answer!"/>

## isolated scope

    application.directive('myScopedButton', function () {
        return {
            restrict: 'E',
            scope: {
            myMessage: '@message', // read only mapping
            myModel: '=model', // two way binding 
            myAction: '&action', // function reference, from outer scope
        },
        template: '<input type="text" data-ng-model="myModel">\
        <button type="button" data-ng-click="myAction()">{{myMessage}}</button>',
    }});
    <my-scoped-button message="I'm a button!" model="anyVar" action="sayHello()"></my-scoped-button>

# routing

* pages can create modular
* views can be outsourced in templates

    application.config(function($routeProvider) {
        $routeProvider
            .when('/template1', {
                templateUrl: '/template1.html',
            }).when('/template2', {
                templateUrl: '/template2.html',
            }).otherwise({
                templateUrl: '/defaultTemplate.html',
        });       
    });

# rest

    application.controller('httpExample', function($scope, $http) {
        $http.get('/people')
            .success(function (result) {
            $scope.httpResult = result;
        });
    });

# resource

* special module
* promise objects
* object oriented access

    <!-- include module -->
    <script src="./lib/angular-resource.min.js"/>
    var app = angular.module('presentation', ['ngResource']);

    application.controller('resourceExample', function($scope, $resource) {
        var Person = $resource('/people/:id', {id:'@id'});
            $scope.person = Person.get({id:1}, function() {
            $scope.person.first = 'new Name';
            $scope.person.$save();
        });       
    });

# unit testing

* angularJS is designed with testing in mind
* use angular-mocks.js that includes some mock objects
* controllers are mockable through dependency injection

    application.run(function($httpBackend) {     
        var people = [{id: 0, first: 'Arthur', last: 'Dent'},
            {id: 1, first: 'Zaphod', last: 'Beeblebrox'}];
            $httpBackend.whenGET('/people').respond(people);
            $httpBackend.whenGET('/people/1').respond(people[1]);
            $httpBackend.expectPOST('/people/1').respond(function(data){return data});

            window.setTimeout(function() {
            $httpBackend.flush();
        }, 1000);
    });

# bdd

* karma as testrunner
* using jasmin
* testframework protractor (because selenium has to many problems with timeouts)

    describe("A suite", function() {
        beforeEach(function() {
            //...
        });
        it("contains spec with an expectation", function() {
            expect(true).toBe(true);
        });
    })

# others

    <!-- wrong -->
    <my-button/>
    <my-button2/>
    <!-- right -->
    <my-button></my-button>
    <my-button2></my-button2>

# links

* http://angularjs.org/
* http://blog.fusioncharts.com/2014/08/angularjs-vs-backbone-js-vs-ember-js―choosing-a-javascript-framework-part-2/
* http://blog.nebithi.com/angularjs-vs-emberjs/
* https://github.com/angular/angular.js
* http://gruntjs.com/
