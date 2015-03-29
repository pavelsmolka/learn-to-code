Lesson 4
========
Associative arrays and JSON.

##Revision
 - Type system: primitive types (boolean, integer, float/double, string)
 - Type-casting string"20" to an actual number 20 using `(int)$stringVariable`
 - Array type - a list of values, arbitrarily long
 - Accessing arrays using index (no iteration necessary)
 - Iterating over an array -> `foreach` and `for` loop
 - Mapping a file to an array, each line as one string in an array, using `file()` function
 - Opening a file using `fopen()`, obtaining a file handle, which we can use later, for example for `fgetcsv()`

##Theory
 - Array index = key.
 - Finding a mode (most frequently occuring number) in a list -> we need to store the number of occurrences for every number.
 - Associative arrays (map, hash) are arrays, where the key is arbitrary (primitive) type.
 - JSON data format - very popular due to its simplicity
 - JSON is basically an associative array (written for JavaScript)
 - XML format - more options, not so popular lately, but still very useful (and powerful)

##Hands on
 - Create an associative array of people in our team, where the key is the name and value is the age.
 - Without any iteration, print Petr's age.
 - Use `var_dump()` or `var_export()` to inspect the associative array variable.
 - Iterate over the associative array and print everyone's name and age. Use `foreach ($people as $name => $age)`.
 - Create a program which reads data from FIE API (use `file_get_contents`). Print the data first to check you are getting something: http://search-api.fie.futurenet.com/widget.php?site=TRD&territory=GB&trd_product_id=1191350&id=top
 - Modify the previous program so it uses `json_decode` (with 2nd parameter `true`) to get the data into a (nested) associative array structure. Use `var_dump()` or `var_export()` to find out how exactly the data looks like. Iterate over the products in the result and print the name and affiliate link for each of them. You might need to get into the array of products first! 
 - Open the program with Hawk team members, and instead of printing people names, generate a JSON using `json_encode()` and print the result. How difficult is that? Do we need to iterate?
 - Add another team member, after the array has been initialized. Use something like `$people['Jonathan'] = 32;`. 
 - You can access any field in both normal and associative array referring to its index, and rewrite its value. Change Ross's age to whatever+1, he had his birthday on Wednesday!

##Homework 3

### 3.1 More numbers!
 - 3.1.1 Generate an array of 100 random numbers (range from 0 to 9). Find the mode (most frequently occurring number), print it and print the number of its occurrences.
 - 3.1.2 Modify the previous program so it prints number of occurrences of all items in the list (should be 10 records, unless we are extremely unlucky).
 - 3.1.3 [Optional]: Generate an array of 100 random numbers (range from 0 to 99). Divide them into "categories" identified by multiples of 10 (0, 10, 20, ..., 90), so that each category is represented by an item in the associative array, where the item key is the category identifier number (0, 10, 20, ..., 90), and the value is a *list* (normal array) of all numbers from the original array, which are greater than or equal to this number, but lower than the next one. Hint: Initialize the $result array first, so you have an empty result list, to which you add numbers as you iterate the randomly-generated input array. Example result:
```php
$result = array( 
    0 => array(1, 0, 7, 4, 0, 5, 1),
    10 => array(12, 17, 19, 10),
    20 => array(21, 20, 24, 25, 27),
    ...
    90 => array(99, 92, 90, 91, 98, 90, 92),
);
```

### 3.2 Generating JSON from CSV file
 - 3.2.1 Open a CSV file and parse it using `fgetcsv`. Store the first line in a separate variable - it's the array header. Use `array_combine` to create an associative array from each line. If your original CSV file had N rows (including the header), you should have N-1 associative arrays, ideally stored within one big array (with numeric index). Use `var_dump()` to make sure you have the right result.
 - 3.2.2 Modify the previous program so it prints the names and prices of the products, using the CSV header name. What is different to our last homework? What happens if somebody changes the order of the columns in the CSV?
 - 3.2.3 Modify the previous program so it does not print the names and prices. Instead, create a new associative array, where the keys will be product IDs, and the values the product names. Use `json_encode()` to generate a JSON from this new array. Hint: Initialize your `$result` (associative) array before you start iterating over the CSV lines. Then, for each line, do the data processing and add the product to the result, such as `$result[$productId] = $productName`.
 - 3.2.4 Modify the previous program so each record (the assoc. array value) will consist of a (nested) associative array, containing the product `price`, `name` and `link`, identified with these words as keys. The result should look similarly to the following:
```json
{ 
    1234597 : { "name" : "iPad Air 16GB", "price" : 204.50, "link" : "http://..." },
    2032594 : { "name" : "Motorola Moto G", "price" : 120.00, "link" : "http://..." },
    5434587 : { "name" : "Lego Emma's Bricks", "price" : 17.25, "link" : "http://..." },
    ...
}
```

### 3.3 Testing the data sets
 - 3.3.1 
   - Create a simple associative array, such as Hawk team members we did in the lesson. 
   - Use `isset($assocArray[$key])` to check whether a certain key exists in that array. What happens if there is an item in the array with `null` value?
   - Use `unset($assocArray[$key])` to remove a key from the array. Check that the item is actually removed using `isset`. What happens if you try to unset it again? Can you an item with the same key, if you already unset it?
 - 3.3.2 Remember how we can download data from FIE API and parse the JSON into an (nested) associative array structure. Create a program which iterates over the products from the result (var_dump can help you find the right "path" inside the data) and checks, whether the score, price and affiliate link is set for each product: http://search-api.fie.futurenet.com/widget.php?site=TRD&territory=GB&trd_product_id=1191350&id=top
 - 3.3.3 
   - Modify the previous program so it checks that the score is a floating-point number; price is a string but can be converted to non-zero floating-point number as well, and affiliate link is URL (use `filter_var($url, FILTER_VALIDATE_URL)`).
   - Test whether the products are ordered by price, from the cheapest to the most expensive.
   - Test whether the `score` attribute is descending (the first product should have the highest score, the last one the lowest).
 - 3.3.4 Use the Comparison Chart API to get slightly different data: http://search-api.fie.futurenet.com/widget.php?site=TRD&territory=GB&trd_product_id=1191350&id=comparison&rows=20 With this dataset, check the previous two conditions as well (price order, score order). What results do you see? Is it correct?
 - 3.3.5 Put the Top Widget test and Comparison Chart test into one test file, copy-paste code when necessary. Realize how much code you need to duplicate and think about the disadvantages of copy-pasted (very similar) code snippets. Think about what the best solutions might be.
