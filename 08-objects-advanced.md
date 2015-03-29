#Lesson 8

Objects - advanced

##Theory

###Visibility
 - Some actions cannot be performed directly, they are hidden for the sake of us being able to operate complex objects.
   - Example: You can start the car, but you cannot directly inject the fuel into the cylinder.
   - Example: You are able to find any file on the hard drive, but you cannot move the hard drive head.
 - Object oriented languages like PHP use *visibility* to hide the "internal" behavior. We touched this in the last class, and we have seen the difference between declaring methods or properties `public` and `protected`.

###Inheritance
 - We use classes to define how objects of one "type" look like.
 - However, the classes can also be more or less similar.
   - Example: A lorry and a car are two different types of objects (classes), but they are closer to each other than to a table. (However, a car and a lorry are still more distinct than two normal cars compared to each other).
   - They both have a certain number of wheels, a maximum speed. On top of that, a lorry has the volume of the loading platform, whereas a car has a number of seats.
   - In fact, "lorry" and "passenger car" are just two special types of cars. Possibly, there are others.
 - In the OO programming language, we use `inheritance` to make these "specialized" classes.
 - Some methods in the class might also be declared as *abstract*. We are basically requiring the specialized version to implement the functionality. An example might be a Person class: we know everyone can "say hello" in their language, but it depends on the specific type (English person, Czech person, ...) how exactly the greeting will sound.

###Composition
 - In real world, objects usually consist of other objects. For instance, a Laptop consists of a screen, hard drive, keyboard, memory, etc. Each of these components is in fact a (more or less) standalone object, which can be further decomposed into smaller objects, for instance the hard drive contains cylinders, the reading head, rotor, etc.
 - In OOP, we use *composition* to construct more complex objects. We literally compose them from the simpler ones.

##Hands on

We will do some geometry today!

###Visibility
 - We already used both `public` and `protected properties in last lesson. In this exercise, we will build on that.
 - Create a class `Square`, which will represent the geometric shape of square.
 - Make sure you can set (and capture in the property) the length of the square side in the constructor. Why do we set in the constructor? We need to make sure the object is valid from the very first point of creation. Also, why don't we allow the side length to change?
 - Create a protected property and a public setter representing the color. Why don't we insist on receiving the color in the constructor as well?
 - Create a method calculateArea(), which will print the area (2D volume) of the square.
 - Create a method describe(), which will print the information about the square, such as "A {blue} square with area of {25}", where the parts in {curly brackets} will be replaced by the respective values.
 - Are we able to determine the side length of the square, once the square is created? Do we want/need to?
 - What is the main message here? Visibility is just a tool to make the code less error-prone. It does not provide any additional functionality. In fact, it only *hides* certain parts of the objects, so we don't misuse them in the way they weren't designed (checking the values in getters etc.)

###Inheritance
 - In the next phase, we will create another shapes: Rectangle, Circle and Triangle.
 - First, create the class `Circle`. What do we need to set in the constructor?
 - Let's make sure Circle supports similar functionality to Rectangle: 
    - We will be able to calculate the area.
    - We will be able to receive an information about the Circle, which includes the color and the area.
 - Now, we have a lot of duplicated code. That's always a smell...
 - What should we do? Create a more generic `Shape` class. Then, `Square` and `Circle` will be more specific types of `Shapes`, similarly to our lorry & passenger car example from the theory.
 - Make sure you "push" all common properties and methods to `Shape`. We still need to keep some of them in the specific shapes. Why is that? Is it correct?
 - Create an `abstract` method. Abstract method is basically a contract which the specific class *must* implement. In fact, we *override* the abstract declaration with the actual method.
 - We can also override an actual method, if we need. You will see that in the homework.

###Composition
 - In the final part of our hands-on, we will deal with 3D shapes.
 - Let's create a `RectangularCuboid` with a rectangular base. In fact, we should compose it of a rectangle (the base) and the vertical height (a line).
 - Make sure we implement similar methods as in the previous examples - color, volume (3D this time!) and description.
 - Create `Cylinder` class. How is it different from the `RectangularCuboid`?
 - Can we merge these two classes into one, or at least "promote" the common functionality to a parent class?
 - Create similar two classes for `RectangularPyramid` and `Cone`. Can we simplify these using a parent class?

##Homework

As you might have noticed, your tasks are less and less specific as we advance in the programming topics. That's not because I am lazy (well, I am, but that's another story), but predominantly because a substantial part of software engineer's work is thinking about the problem, the problem decomposition, design of the algorithm and sketching the appropriate program structure - classes, functions etc. You have to rely more and more on your judgement. Feel free to ask any questions, but implementation-wise, it's a lot up to you. Note, there are no more numbers for the homework - we should implement everything with classes.

Make sure you use PHPDoc comments. For one, it is a good practice and it's one of the things I want you to learn. But more importantly, it's very useful for you. When you have a lot of different classes and objects to juggle with, it will really help you to stay sane.

##Test Plan
This week, we will design a `TestPlan` class. Its purpose is to provide the individual steps of the testing process. Each step consists of two logical parts - what we test (test input), and what result we expect (test assertion). 

As an example, we might have the following:
 - Test input: Live API response (JSON) for top widget on TechRadar, where the product ID is 1191350.
 - Test assertion: The response contains list of "deals", in which there are valid products (without contracts).

###Test Input
The test input should be represented by `TestInput` class. It is very simple, it basically consists (i.e. is has properties) of the widget name (string) and (an associative array of) query parameters, which together define an API endpoint (assuming we already know the host name). The parameters are basically the same as the parameters of the last method of `HawkDataAccessor` you have worked on last week.

Refactor your `HawkDataAccessor` (or create a new similar class, if you want), so that it will take a `TestInput` object as a parameter. Then, inside the method of `HawkDataAccessor`, the actual values are "pulled" from the specific `TestInput` (use getters) and the respective request is sent to the API. 

Test that your code works so far by creating a simple top level program, which creates several different `TestInput`s, one `HawkDataAccessor` and prints the JSON response for each request. You should get this working before you continue with the next part. Ideally, `json_decode` the response inside the `HawkDataAccessor` class, so the result will be an associative array (use the second parameter `true` to enforce it to be an array) representing the result, NOT just a long string with bunch of curly brackets.

##Test Input Source
Create a class `CsvTestInputSource`. An object of this class will be given a path to a CSV file, from which it will read the test inputs. As an example, the columns of the CSV might be "widget id", "site", "territory", "article_id". Each row in the file then represents a specific request. `CsvTestInputSource` will create a new `TestInput` object from each row. Create a method of the reader, which will return one `TestInput` at a time. Return `null` when there are no more inputs (i.e. the we reached the end of the file).

Now, you can amend your top level program (or create a new one, that's up to you). Instead of manually creating each `TestInput` object, you will just create one `CsvTestInputSource`, which will start creating these inputs for you, as you specify them in the CSV. The big advantage of such approach is that we can have an overview of the test steps in a spreadsheet, and just make the software crunch through them.

##Test Checks
In reality, each test check should be specific per each API endpoint. We might for example check (assert), that response for "DE" territory will return a product in EUR, whereas "GB" request returns a pound product. We will get there eventually, but in this homework, we will work with assertions separately from the requests. Right now, we basically only want to test things which should work "across the board", for all requests (at least these in our input). That includes the widget title, checking whether there are any products, and whether each product is valid (has a numeric price, affiliate link which is a valid URL etc).

Right now, we will create two different checks (assertions), represented by two classes. One for the widget title and another one checking there is an array of "deals" and another array of "contracts" in the response. Each of these classes should have a method `checkApiResponse` which takes the (already decoded) API response as a parameter. If you remember, we should have this response available as an associative array from our `HawkDataAccessor` class.

So, the first assertion is represented by `WidgetTitleCheck`. In the `checkApiResponse`, you will just traverse through the associative array and test whether the 'title' field is present and it's a non-empty string. Return `true` if the test passes, or `false` if any of the described conditions is not met.

The second check is `TwoListsOfProductsCheck`. In this case, we will find 'deals' and 'contracts' fields, and make sure they are both arrays. Again, return `true` or `false`, based on the result of the test. The array of 'deals' or 'contracts' might be empty. We should test whether at least one of these arrays is non-empty. If this was the case, Hawk should have fallen back to TopDeals!

Once you have these two classes done, think whether you can "promote" the common functionality to the parent object (something like `AbstractCheck`), from which both your Check classes inherit (remember to use `extends` keyword). 

If you got this far and you are still up to some [optional] work, feel free to come up with any other Check-class, maybe looking into the product records themselves, or testing the "meta" fields, such as deals_count, merchants_count or territory. Have a look at the actual API response and decide, what would make sense.
