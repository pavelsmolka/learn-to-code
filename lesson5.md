#Lesson 5

Decomposition, functions

##Theory
 - Principle of decomposition - each problem can be broken down into smaller problems. Not only it can, it must be in order for us to be able to solve it.
 - Example: Program testing the API response. How would you break it down? Try different levels of abstraction, so you end up with different numbers of "components".
 - Not only in programming, there are a lot of tasks which are well-defined and repeatable.
 - Function is a piece of code, which follows a certain (well-defined) piece of logic.
 - Each function has a strictly defined input and strictly defined output. These "boundaries" help us assemble large codebase. And of course the function has a body, which transforms the input into output.

 - Don't repeat yourself - duplication of code is easy (copy + paste), but it fails you in the long run. Trust me on this for now, you will confirm this yourself as you develop more complex (and permanent) code.
 - When you identify the common functionality, think of a "component" and create a function which you use from all necessary places.
 - Sometimes "common" functionality is non-trivial. 
   - Is adding up two different pairs of numbers a common functionality? (6+5 vs 3+2)
   - Is getting data from two different CSV files a common functionality?
   - Is extraction of two different fields from the data (assoc. array) a common functionality?
   - Is getting a list of products from the API and from the CSV a common functionality?
   - Is finding a maximum of an array of numbers a common functionality to finding the highest price in the CSV file? What is the relation between these two tasks?

##Hands on
 - Pen&Paper: Describe a function calculating a sum of two numbers would look like.
 - Pen&Paper: Design a function which computes a maximum of the list of numbers.

 - Use `function` keyword to declare a function, such as: `function($arg1, $arg2) { ... }`
 - Use `/**` to start a PHPDoc block. Describe what the function does.
 - Create a `fizzbuzz` function, which returns 'Fizz', 'Buzz' or 'FizzBuzz' based on the number.
 - Put this function into a separate file, for example `fizzbuzz.php`
 - Create a program which prints FizzBuzz for a random number (the same rules as in previous lesson). Use `fizzbuzz` function.
 - Create a program which prints FizzBuzz for all numbers from 1 to 30.

##Homework
 - Create a function which transforms the number into a currency code: 1 = GBP, 2 = USD, 3 = EUR (these values are hard-coded in the function body, use if/elseif/elseif, switch or associative array and key-value lookup).
 - Use the function from above in the program from our last lesson, which reads product data from the CSV.
 - Use the same function in the program which reads the product info from the API.
 - Finish your homework from last lessons (ideally doing (or at least trying) optional assignments as well).
 - Use functions where applicable. That includes cross-task functionality, such as "modify the previous program..."
 - Also, modify your already completed and submitted programs from the last lesson, so there is no unnecessary code duplication.

