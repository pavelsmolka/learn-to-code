Lesson 2
========

Theory
------
 - compiler, interpreter
 - PHP is interpreted language
 - source code divided into files
 - PHP can run in a command line (easiest) or it can be attached to a web server
 - Simple language constructs (see hands on)

Hands on
--------
 - Hello world! (opening tag, echo, string literal)
 - Using PHP as a simple calculator (nubers, arithmetic operators)
 - Printing current time using date("H:i:s") (calling a standard language function)
 - Saving current time to variable, sleep, print after 10 seconds (variable, sleep function)
 - Determining whether we should go home already (if statement, using else block, comparison operator)
 - Alarm which will tell us to go home at 5:30 (loop), use date("H:i")

Homework
--------
 - Write a short script which will print current time, wait for 1 minute and print the time again
 - Write an infinite script which will print the time every second (interrupt using Ctrl+C in command line)
 - Write a script which will print a random number from 0 to 50 (check http://php.net/manual/en/function.rand.php)
 - Write an infinite script which will print a different random number every second
 - Modify the previous program, so it also prints the verbal information whether the random number is greater or lower than 500
 - Write a similar program, which prints the number only if it is divisible by 3 (use operator modulo, N % M)
 - Write a similar program, which prints the number only if it is bigger then the digit representing the number of seconds of the current time.
 - Write a program which generates a random number from 0 to 50 every second. When the number is greater than 40, it prints it and finishes (use break; statement).
 - Write a similar program. It finishes if the number equals to the digit representing the number of seconds of the time when it was started.

Reading
-------
http://php.net/manual/en/control-structures.if.php
http://php.net/manual/en/control-structures.else.php
http://php.net/manual/en/control-structures.while.php
http://php.net/manual/en/control-structures.break.php
http://php.net/manual/en/language.variables.basics.php (Print variable within a double-quoted string)
http://php.net/manual/en/language.operators.assignment.php
http://php.net/manual/en/language.operators.comparison.php
http://php.net/manual/en/language.operators.string.php (Join two strings together to 1 variable, such as name + surname)


Next Lesson:
 - type system, primitive types, complex types
 - logical AND/OR, variables, lists, for loop
 - reading from file line by line, explode function
 - processing a CSV file, finding rows meeting certain criteria

Later:
 - classes, objects, functions
