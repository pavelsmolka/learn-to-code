Lesson 3
========

Revision
--------
 - What a source code is
 - PHP opening tag, running a PHP script from a command line
 - echo
 - language constructs: if, else, while; 
 - Have you checked elseif, switch + case, break?
 - String concatenation using dot (from reading part of HW)
 - variables
 - calling functions - date(), rand(), sleep()

Theory
------
 - Everything is binary in the computer
 - Every variable has a binary value and a "type" what it is (mention ASCII table)
 - Value comparison (==) vs. value + type comparison (===)
 - Numeric types: int, float; We already know numeric operations (+, -, *, /)
 - Boolean type (true/false). Boolean logic (AND, NOT, OR)
 - String (we take as a primitive type)
 - Complex data types: array, (there are also objects).
 - Array iteration
 - Using array index to retrieve an array item. Programmers count from zero!
 - Files: Binary or text, streaming or loading into memory.

Hands On
--------
 - Create a program, which generates random numbers. Print the information whether a random number is greater than 10 AND lower than 20.
 - Modify the previous program so it checks whether the number is greater than 20 OR even (use modulo operator, how would you do it without modulo?).
 - Find out what data type the result of date("s") is. How to make it a number? Comparisons with both to try == and ===.
 - Implement simple FizzBuzz for one random number: Fizz if divisible by 3, Buzz if divisible by 5, FizzBuzz if divisible by 15 (3 AND 5). Keep in mind, algorithmic thinking comes first!
 - Array (old and new syntax)
 - Using `while` and `array_pop()` to iterate over an array
 - Using `foreach` to iterate over an array
 - Using `for` to iterate N-times for ($ii = 0; $ii < N; $ii++). Use array index to access the item.
 - Create an array from a CSV file, using file() function, print each line
 - Use `explode()` to obtain individual CSV fields
   - nested arrays
   - what might be a problem when using explode, with real CSV data?

Homework
--------

###0. Playing with letters
 - *0.0* Use function ord() to retrieve a numeric (ASCII) representation of a character: http://php.net/manual/en/function.ord.php
 - *0.1* Generate random letters in an infinite loop, using `rand()` and `chr()`, but use the number only if the number stands for a valid lowercase OR uppercase letter.
 - *0.2* Create a program which contains two loops (iterations). In the first one, generate 100 random numbers and put them into an array. In the second part, iterate over this array and print the numbers bigger than 20.
 - *0.3* Modify the previous program so it does not print the numbers, but the indexes (positions in the array) where these numbers are.
 - *0.4* Modify the previous program so it prints only the index of first number greater than 20 (first occurence of such number).
 - *0.5* Create a program which prints numbers representing ASCII positions of letters of your name and surname. Hint: Create an array of the letters first, then iterate over that array and use `ord()` function.

###1. Processing a CSV file
 - *1.0* Create a program which reads a CSV file containing one product on each line. Find the cheapest product and print its name and price. Do not print data of any other product.
 - *1.1* Modify the previous program so it uses `fgetcsv()` function. What is the advantage of using it, instead of `file()` and explode()? Hint: you will need to open the file separately using `fopen()`, save the "handle" into a variable and only then call fgetcsv.
 - *1.2* Create a similar program, which reads products information from a CSV file. Each product has a currency. Print a list of all currencies which appear in the CSV file - but each currency only once! Hint: Build a list of currencies first, using `in_array` function to find out whether we already have the currency in the list or not. The printing part is easy then.

###2. FizzBuzz and Random Arrays
 - *2.0* (Refresh your memory checking the algorithmic homework from the first lesson).
 - *2.1* Generate an array of 50 random numbers (range from 0 to 99). Create a program which finds the biggest of these numbers and prints it, along with the index (position) of the number in the array.
 - *2.2* Create a similar program which calculates an average (mean) of the array.
 - *2.3* Try implementing the previous two tasks using built-in functions `max()` (for the former) and `array-sum()` (the latter) - or without these functions, if you already used them (basically the other way):
   - http://php.net/manual/en/function.array-sum.php
   - http://php.net/manual/en/function.max.php
 - *2.4*, *2.5* [Optional]: Create another two similar programs which find modal and median of the array of 50 random numbers.
 - *2.6* Create the standard FizzBuzz program: Print numbers from 1 to 500 with additional "Fizz" when the number is divisible by 3, Buzz when divisible by 5 and FizzBuzz when divisible by 3 AND 5. Remember algorithmic thinking!
 - *2.7* [Optional]: How would you approach FizzBuzz++, where you also need to find out whether the number is prime? How do you find out whether a number is prime at the first place? Hint: Use pen-n-paper to find an algorithmic way to get this information (prime or not) just for one number.
 - *2.8* Use rand() function to generate a number. Use this number as a size (length) of an array, and generate an array of random numbers of this size.
 - *2.9* Modify the previous program so it creates an array of arrays of random numbers. Hint: Generate the first number, which determines the length of the "main" array. Instead of filling this array directly with numbers, use similar approach to generate another number, which will determine the length of the "nested" array. Only then generate the members. The result (conceptually) should look similarly to the following:

```
// The main top-level array, it happens to have 2 members (random)
$main_array = [
   // First nested array, it happens to have 6 members (random)
   [10, 5, 2, 23, 14, 8], // <-- random numbersoption
   // Second nested array, it happens to have 3 members (random)
   [5, 13, 2],
];
```

Reference
---------
 - http://php.net/manual/en/language.operators.increment.php (Using in the for-loop)
 - http://en.wikipedia.org/wiki/ASCII
 - http://php.net/manual/en/function.chr.php
 - http://php.net/manual/en/function.ord.php
 - http://php.net/manual/en/control-structures.foreach.php
 - http://php.net/manual/en/control-structures.for.php
 - http://php.net/manual/en/function.file.php
 - http://php.net/manual/en/function.fopen.php
 - http://php.net/manual/en/function.fgetcsv.php
 - Anything else we talked about or you need in your homework, ideally on php.net

##Extra
 - http://christinacacioppo.com/blog/build-products (Some of those points are real pearls of wisdom: "Programming is the surest way I know to feel brilliant one second and idiotic the next")
 - http://vimeo.com/110554082 (This is rather crazy video, but full of interesting ideas about how important it is to be able to code, about team and project management, agile and also QA. I will be happy to hear your thoughts, but obviously this is not mandatory at all. Many things there are bollocks, but interesting and provocative bollocks to think about indeed.)
