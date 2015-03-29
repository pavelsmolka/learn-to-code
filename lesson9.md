#Lesson 9

- Third party libraries, Composer
- Namespaces, Exceptions

##Theory
 - We don't want to write everything from scratch.
 - Do you remember problem decomposition? There are plenty of projects doing exactly what we might need - sending requests, logging, accessing various databases, etc. We sometimes call them libraries.
 - We can use the 3rd party projects and libraries, we just need to tell the program what we need and where it can find it.
 - Composer is a tool which allows us to easily load and manage dependencies - any 3rd party tools we need.
 - Composer also ensures all classes provided from the library are accessible. It can even help loading our own classes, so we don't need to require_once everything.
 - When we create class like `HawkDataAccessor`, it's unlikely that somebody else would create one as well. However, a naming collision might happen for plenty other cases, with more generic names. Each class should therefore also have a *namespace*, which ensures it is unique. For instance, we use namespace `Future\FIE` in our projects.
 - What happens when a method (or function) should return an object, but something unexpected happens? We can return null/false, but then there is no way to find out what exactly went wrong. The solution are `Exception`s.
 - An exception is a signal, which basically interrupts a program, similarly to return statement. It is possible to expect exceptions, catch them and react as necessary, based on the specific exception.
 - Exception is in fact just a class, which should inherit built-in `Exception`. We can for example have `NetworkFailureException` or `InvalidArgumentException`. When we throw an exception, we instantiate an object of this class, which carries the information about the error. We should have a different catch block (i.e. ways of handling the exception) for different exception classes.

##Hands on

###Composer
 - Make sure you have installed (`brew install composer`).
 - Create `composer.json` file on the top-level of the project.
 - Follow https://getcomposer.org/doc/00-intro.md
 - By running `composer install`, you actually download and install the dependencies.
 - Put all your source files into `src` directory - that's a convention.
 - Choose your autoloading option: https://getcomposer.org/doc/04-schema.md#autoload
 - You get autoloading of your AND 3rd party classes for free by using `require 'vendor/autoload.php';`

###Namespaces
 - The namespace should follow structure of {vendor}\{project}\{anything\you\need}
 - Use `namespace` keyword, on the very top of the script
 - Whenever you use a namespaced class, you must refered to it by its full name, or use `use` keyword, right below the namespace declaration.

###Exceptions
 - Let's modify our programs from lesson 7
 - Find a place where we checked for some condition, and wanted to report an error.
 - Determine how you would name the error and create an Exception class which will represent it.
 - Instantiate the exception and use `throw` statement to throw it.
 - Run the program and find out what happens if you throw an exception.
 - Wrap the call in `try { ... }` block and then `catch (YourException $e) { ... }`
 - What happens now?
 - What is the three biggest advantages of using exceptions, compared to returning null/false? 
   - You can handle situations where result value is difficult to handle (constructors, methods which do not return anything).
   - You can communicate specific error types.
   - The exception does not have to be handled at the very next layer above.
 - From now on, always consider using `YourSpecificException` rather than returning `null`. From now on, never return false where you would normally return object (it's a type mismatch and we should avoid it!).

##Homework
This time, there is again much less information given from me, and much more for you to figure out, similarly to last time. Most of the tasks do not have one solution, you can approach them from a different perspectives, and I will just give you some feedback.

This week, we will continue developing our API-testing project. Ideally, continue working on the same code-base, and extract it to a dedicated project (from the original homework one), if you already haven't done so.

Generally, please make sure (now and also for the homework from last week) that:
 - All your classes are in a namespace.
 - You use Composer to auto-load all classes (require vendor/autoload only at the very beginning of the top-level program).
 - [Optional]: You can of course use any third party libraries you find, as long as you install them via Composer. At least Monolog, the logging library, is handy to print any kind of messages, and very easy to use.

###Enhancing TestChecks
First part, as a warm-up, create several more `TestCheck`s, following the same concept as last week. You can create a class to check anything from the API response. It does not have to be a check which will pass for all requests. For instance a class which will test whether a CarPhone product is present in the contracts part of the response seems quite topical. If you cannot come up with anything, just think about what you usually test: Is there an URL rewrite included in the link? Are there enough deals? Are they ordered by price? You can even create a "parametrized" class, for instance a `CurrencyGroupCheck`, which will be instantiated with an array of currencies, and it will check whether the deals with these currencies have been present, in the right order.

We need to ensure every `TestCheck` will be able to say whether it succeeded or failed. Create a custom `TestStepFailExceptin` class, and throw an exception of that class if the test check fails. If the exception is not thrown, the check is assumed to pass.

###TestStep
Recall how `TestInput` and `TestCheck`s are supposed to work. All `TestCheck`s are probably extending your `AbstractCheck` class. Create a new class `TestStep`, which wraps these two together (it should be quite a small class, just a container to easily handle these two together). Essentially, `TestStep` is one testing unit we can mark as pass/fail. In Behat, it is represented by one line in the scenario (which combines what to do and what to check together, if you think about it).

###TestGenerator
Last time, we loaded the tests from a CSV. It is good, but we need to specify every combination of testing parameters, which would lead to repetition. In this part, you will create a class which will essentially generate `TestStep`s. We will generate various `TestInput`s from the "atomic" parameters, and attach any relevant `TestCheck`s to them.

The first part is generating the inputs. Let's say we have 10 article IDs, 3 territories, 2 site codes and 3 widgets. If we want to test all combinations, it combines up to 90! If you use nested loops, it is quite easy to generate all these combinations beforehand.

More importantly, we want to combine specific `TestInput`s with relevant `TestCheck`s. We can probably add the "generic" checks to every input (at least `WidgetTitleCheck` and `TwoListsOfProductsCheck`, as we designed them last week). In addition, we might want to say, that for instance for two specific article IDs representing phone articles, we want to also add for example `ContractsIncludedCheck`, `CarPhonePresentCheck`. Or, a different example, we might add a parametrized `ProductNumberCheck`, which tests whether there is a certain number of products in the response. We want to specify this number differently for the review widget (it's 4 deals only), and differently for CC (there are up to 100, so we can test whether there are at least 20, let's say).

We have already calculated that various combinations of "atomic" input parameters give us let's say 90 inputs. The `TestGenerator` should be able to produce these and combine them with the checks, producing even bigger number of complete `TestStep`s. In other words, you add 1 or more checks for every input. If you added 5 checks for one input (in average), that gives us 450 `TestSteps`. It's important to keep in mind each `TestStep` is self-contained, it consists of only one individual input and one check. If we check for more than one thing, we should create more steps, because one might pass and another one fail.

###TestPlan
The last thing for you to build this week is `TestPlan` class. Basically, it should replace any top-level script you would use otherwise. It's generally a good practice to put as much code as possible into classes. Our `TestPlan` object can use `TestInputSource` from last week or/and `TestGenerator` to create list of `TestStep`s. You can try both approaches, and you can create two slightly different `TestPlan`s if you need - don't forget about the inheritance! 

The `TestPlan` should be responsible for obtaining the list of `TestStep`s from the source/generator, running them in a loop, plus printing the results (as a simple messages)). Make sure you use the catch block to check whether `TestStepFailExceptin` from any check was thrown. You can choose whether the test plan will continue after a fail, or whether it will immediately interrupt the execution (I believe Behat has such option you use, am I right?).

##References
 - https://packagist.org
 - https://getcomposer.org
