#Lesson 7

Objects - basics:
 - Class vs. Object
 - Object instantiation + constructor
 - Properties
 - Methods


![Brace yourself](http://i.imgur.com/nc8puKI.jpg)

##Revision
 - Primitive types (int, bool, string), complex ones (array, associative array)
 - Loops
 - Functions: input -> output

##Theory
 - Algorithms (software generally) solve real life problems. The closer to real life the programming model is, the better.
 - A real world consists of "objects" - things you can see, use, consume, buy, destroy...
   - Example: A car, a table, a pen, paper.
 - Real world objects have certain properties, specific per each type of an object:
   - A table has a certain number of legs, a car has a certain color, maximum speed and trunk volume, maybe a number of wheels, but definitely not legs.
 - You can manipulate objects in a certain way:
   - Example: A car - you can honk the horn, you can switch the lights on and off. You can use the pen to write something on a piece of paper.
 - Also, in real life, things have certain state, dependent on the actions you performed:
   - Example: Once you turn the lights on, the car has the lights on - oh really? O.o
   - Example: If you take a screwdriver and remove a leg from the table, it has a different number of legs.

 - We can model the software in a very similar way:
   - Real life objects are software Objects
   - Real life properties (color, number of wheels) are Object Properties.
   - Manipulation is represented by calling methods (functions in objects).
   - The object state is represented by the specific values of Object Properties.

 - Similarly to the concept of an English word, describing a class of the same objects ("a car"), there is the same concept represented by "class" in the programming. 
 - Class describes what the objects have to have in common:
   - Example: A car must have 4 or more wheels.
   - Example: Given a car, you can honk its horn.
 - Although class defines some boundaries, it also lets you define some individual properties:
   - Example: Each car can have a different color.
   - Example: Each car can have different number of wheels, on the condition it is at least 4 (see the example above).

 - So, a recap before we start with hands on:
   - A class is a description of how objects of a certain type will look like (the car as a concept).
   - A class defines the properties (state) and methods (actions). 
   - An object is one specific instance of the class (one specific car).
   - You can modify the state of an object by calling the methods, and results of methods depend on the state:  P <-> M

##Hands on
 - Let's design a simple object representing a Car:
   - You will be able to honk a horn (print "Honk, honk!"). (method)
   - The Car will have a color of users choice. The color of one specific car cannot be changed, once the car exists. (property)
   - You will be able to tell what color the car has. (method)
   - The Car will have lights switched on or off. (property)
   - You will be able to toggle the lights on and off. (method)

Create and use a car:
 - We need to create the Car *class* first. Each class should be in a separate file, similar to what we did with functions.
 - Use `class` keyword to define the class - PHPStorm can help you with it.
   - Heads up: do we have a car yet? No, we have just defined the concept. So:
 - Create a simple script which *instantiates* a new Car *object*. That's the program which will actually create and use one specific car object, based on the class description.

Honk:
 - Within the class, create a method, such as if you want to declare a `function`.
   - What the input is?
   - What the output is?
 - Call the method from our program, using the arrow operator: `$car->honk()`. Arrow is used for accessing both methods and properties, it's the brackets which make the difference between these two.
 - Use the keyword `public` to declare a property representing the lights (on/off) (within the class, but outside methods).
 - Make sure the lights are switched off when the car is created.
 - Create a method which will toggle the lights, call it and test whether it works.

##Homework

In the homework, you will create three classes. Each section of the homework is one class. Even though the homework is split into very granular level, there are only 3 files, each of which contains one class - `Person`, `HawkDataAccessor` and `NumberAggregator`.

Besides these three "main" files, you should create a simple program for each class - in order to test the functionality you write. In this program (top-level program), instantiate the object of the tested class and call the methods as you need, in order to test whether it does what it should, similarly as we did with our `Car` class from the lesson. Please, submit these testing programs as well. You can create as many testing (top-level) programs as you want.

###7.1 Person
 - 7.1.1 Create an empty class called `Person`.
 - 7.1.2 Create a method `sayHello()` which prints "Hello!" whenever called.
 - 7.1.3 Create another method `getGreeting()`, which returns "Hello!", instead of printing it. We provide the top-level program with the result, and the top-level program should print it.
 - 7.1.4 Create a constructor (`__construct()` method), which takes a string variable `$name` as a parameter (argument) and saves it in the object property `public $name`.
 - 7.1.5 Create a method `getName()`, which returns a string like "I am <name>", where <name> will be the actual name previously provided in the contructor.
 - 7.1.6 Read about `time()` function in PHP and find out, what "Unix timestamp" is. Make sure you understand the concept.
 - 7.1.7 When the object is created, save current time to a property (use `time()` function). That will be the "birth second" of our object.
 - 7.1.8 Create a method `getAgeInSeconds()`, which determines what the "age" of the object is (in seconds), and returns the result (as a number). Use `sleep()` in the top-level program to test whether it actually works.

###7.2 Number Aggregator
 - 7.2.1 Create `NumberAggregator` class.
 - 7.2.2 Make sure the connstructor takes array of numbers as an argument (parameter) and keeps them in the object property (so the property will be an array). Use PHPDoc to annotate the type of the property with `/** @var array */`.
 - 7.2.3 Create a method `addNumber()` which will add another number (provided as a method parameter) to the array of numbers stored within the object.
 - 7.2.4 Create `getNumbers()` method, which returns the array of numbers currently stored in the given `NumberAggregator` object. Use PHPDoc to annotate the result type of the method.
 - 7.2.5 Create `getMaximum()` method, which returns the highest number from the numbers currently stored in the given object. Feel free to use max() within the method.
 - 7.2.6 Create similar `getMinimum()` which returns the lowest number.
 - 7.2.7 Create `getMean()`, `getMedian()` and `getMode()` methods returning the respective "average" number. Reuse the code from your previews homeworks. Ideally, you should already have each of these ready as a plain `function` from the previous homeworks, so make sure you `require_once` the file with the function (include it to the top of the class file, above the name) and call the appropriate function from within each method.

###7.3 Hawk Data Accessor
 - 7.3.1 Create `HawkDataAccessor` class.
 - 7.3.2 Make sure the constructor accepts `$hostName` parameter, and saves it in the object property of the same name. The host name should represent the API host name, such as "stage.search-api.fie.future.net.uk" or "search-api.fie.future.net.uk".
 - 7.3.3 Create a method fetchData($url), which uses the host to retrieve the data from the API. The $url parameter is the part of the request URL on the right side of slash (called "path" and "query") - for example "widget.php?site=TRD&trd_product_id=1191350&id=top". You can `json_decode()` the result before the method returns it, if you think it's sensible.
 - 7.3.4 Create a method `fetchWidgetQuery($widgetName, $query)`. The first argument stands for the widget name, such as "top", which is the "path" part of the URL (basically everything between the first slash and the question mark). The second one contains the "query" part of the URL, such as "site=TRD&trd_product_id=1191350&id=top". The method should connect these two and use `fetchData` (which you have created before) to get the same result. So, the only difference in these two methods is in how they accept the request parameters.
 - 7.3.5 Create another method `fetchWidgetAssoc($widgetName, $parameters)`, which is very similar to the previous one. The main difference is that `$parameters` are an associative array of the parameters specified in "query" part of the URL. An example would be `$parameters = array('site' => 'TRD', 'trd_product_id' => 1191350, 'id' => 'top');` Use `http_build_query` function to generate the query string, and then use `fetchWidgetQuery` to retrieve the data.
 - 7.3.6 Add a validation to the `fetchWidgetAssoc` method. Check, whether the `$parameters` array contains the keys `'id'` and `'site'`. If it does not, print an error message and return null.
