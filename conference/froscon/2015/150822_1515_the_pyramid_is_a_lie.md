# The Pyramid is a Lie

by [Nikolas Martens](http://www.rtens.org/)

# what is it all about

* heavily inspired by ["modelling by example" by everzet](http://everzet.com/post/99045129766/introducing-modelling-by-example)
* it is about automated testing and architecture

# automated testing

* on what level do I test
* how do I write tests (ddd, bdd, tdd, etc.)
* two extreams are "integretation test" and "unit tests"
    * ui
    * end to end
    * acceptance
    * system
    * module
    * component

# integration testing vs unit testing

* ["integration test are a scam" (jbrains)](http://www.jbrains.ca/series/integrated-tests-are-a-scam)
* ["tdd is dead, long live testing" (dhh)](http://david.heinemeierhansson.com/2014/tdd-is-dead-long-live-testing.html)
* integration testing for rtens is
    * through a browser
    * running on a webserver
    * include database and other external services
* unit tests for rtens is
    * test a single class or method
    * fake all dependencies
    * should have "one reason to fail"

## integration tests communication session

### good

* closeness between test and value
* great for legacy testing

### bad

* far from code
* slow execution
* slow feedback
* instable because tidly coupled on a given user interface

## unit tests communication session

### good

* quick design and code feedback
* easy to setup (less data dependency, time etc.)
* confidence

### bad

* mocking can be messy
* harmful to design and architecture
* fixed to internals

# succeeding with agile (by mike cohn)

## content

* ui (only a few)
* service layer tests (some but no one thinks about it)
* unit test (you can't have to many)

## approach

* go from top down
    * create basic integration test
    * use mocks and the start
    * implement the features step by step
* go bottom up
    * create a beautiful architecture
    * use mocks for unit tests

## what are the problems

* you have coverd some areas in all three test areas
* if something big changes, you have to adapt all three tests
* if a feature b is using architecture of feature a, you are testing the same code again (and it will break if you change something in feature a that b needs)
* you start not believing in your tests, which is really bad 

# an other approach - start with the service layer testing (middle out)

* the user interface does not implement business logic
* business logic is expressed in this layer (ubiquitous language)
* the service is the domain
* ui, db, external is the infrastructure
* this is the hexagonal architecture

### ubiquitous language example

```
When I add "Red Car" to the basket"
```

```php
# service context
$basketService->add("Red Car");
```

```php
# ui context
$browser->click("button-add");
$browser->insert("Red Car");
$browser->click("button-send");
```

* you can decide how to do it and where

### howto

* cucumber: worlds
* behat: suits
* phpunit: dataproviders
    * write on test
    * inject a collection of "drivers"
        * service driver
        * ui driver (containing the click paths and so one)
    * define a interface for the driver

# hints

* its the job as the product owner to push you tp get things done quick
* its the job of the developer to push on the quality of the code
* both want to create a great product
* [watoki](https://github.com/watoki)
* use "\_" as place holder when you write methods in a unit tests (e.g. `whenISchedule_On_for_Hours($task, $when, $duration)`)
* use a memory or fixed data implementation in your design phase when dealing with the repository
