#Lesson 10

Final lesson, it's time to do some real stuff!

 - Relational databases, MySQL, PDO
 - Interfaces

##Theory
 - Interface: 
   - Similar to abstract class, but cannot provide any implementation.
   - Good for type hinting, making sure some class *implements* certain method(s).
   - For instance you want a `DataStorage`s, which do not share any functionality, you just need to ensure each of them implements `storeData()` method.
 - Database is just a software built on top of some files.
 - It allows us to see, edit, filter and manipulate the content in an easy way. Google Spreadsheet is a database, and so is Excel.
 - We will use relational database. Relational means there are certain Entities, more or less representing our business objects, connected together by relations. For instance, a Model is an entity, a Match is an entity, a Product is an entity. And we can connect a certain Product to a certain Model using a certain Match.
 - We use ER diagrams (ERD) to visualize the entities and relations.
 - We use SQL language to manipulate the data in the database. It's in fact a very specific programming language executed by the database software. (SQL ~ PHP, MySQL ~ php)
 - DDL (tables and data structure, like classes) and DML (individual entities, like objects)

##Hands on

###Interfaces
 - Let's reopen our Shapes project, find a good place to create an interface.
 - We can use it instead of an abstract class - see the difference.

###Databases
 - Let's draw ERD for FIE Product and Feed. Let's add Merchant, Model and Match.
 - Draw me ERD of people in the office, projects they work on and project managers. Can we allow a double-relation?
 - Use the provided DDL script to create the table structure.
 - Use the provided DML script to fill in some data.
 - Select everything from Product table.
 - Limit the query by a certain condition. Try LIKE query.
 - Use INNER JOIN to select all products for a certain feed.
 - SELECT COUNT.
 - Use GROUP BY with COUNT to aggregate.
 - Require `future/comp_data` in Composer.
 - Use `FuturePDO` class to access the database. Instantiate the class and use `$query = $pdo->query()` method to query the data. You need to `$query->fetchAll(PDO::FETCH_ASSOC)` in order to obtain the result in an associative array.

##Homework
 - Create an `ITestCheck` interface, specifying the mandatory behavior of each Check. Figure out how it should look like.
 - Make sure all check classes implement `ITestCheck`. 
 - Remember you can still use abstract classes (and inheritance (`extends`) hierarchy, alongside interfaces).
 - Realize our existing `TestStep` is in fact an `ApiTestStep`. It contains the input, which is the information about API request. Rename it accordingly.
 - Create new class `DatabaseTestStep`, which will check something in the database. The `DatabaseTestStep` should not contain a `TestInput` and `TestCheck`! It can follow a similar approach, or you can choose a different approach, suited to your needs. Consider keeping the functionality split between "how we get the data" and "how the data should look like when we have it", but especially the part of getting the data will be different - it will access the database. Use `FuturePDO` to get some data from the database, and then you can check whether you received what you expected.
 - Create an interface `ITestStep`. Our original `TestStep` encapsulates the Input and Check, so the interface should specify only method `run()` which will run the test step.

##What's next?
We will talk properly when I get back from holiday. But the idea is basically for you to use your new developer skill-set in real work! Also, if you have an idea of a tiny project, however silly it might be, set a little goal for yourself and try to achieve it. Most of the programmers (yes, most people here at Future as well) spend a lot of free time hacking their personal projects in order to learn new stuff and get better. But of course, that's entirely up to you!
 
##Snippets

Create table Feed and Product:
```
CREATE TABLE `feed` (
  `feed_id` mediumint(8) unsigned NOT NULL AUTO_INCREMENT,
  `feed_name` varchar(100) COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`feed_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `product` (
  `product_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `feed_id` mediumint(8) unsigned NOT NULL,
  `product_name` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  `affiliate_link_url` text COLLATE utf8_unicode_ci NOT NULL,
  `price` decimal(10,2) unsigned DEFAULT NULL,
  PRIMARY KEY (`product_id`),
  KEY `feed_id` (`feed_id`),
  CONSTRAINT `fk_product_feed_id` FOREIGN KEY (`feed_id`) REFERENCES `feed` (`feed_id`) ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

Add some data:
```
INSERT INTO feed(feed_name) VALUES ('Tesco');
INSERT INTO feed(feed_name) VALUES ('Amazon');

INSERT INTO product(product_name, affiliate_link_url, price) VALUES ('Tesco Hudl', 'http://www.tesco.com/direct/hudl', 120.50);

INSERT INTO product(feed_id, product_name, affiliate_link_url, price) VALUES (1, 'Tesco Hudl', 'http://www.tesco.com/direct/hudl', 120.50);
INSERT INTO product(feed_id, product_name, affiliate_link_url, price) VALUES (1, 'Another Tesco Product', 'http://www.tesco.com/direct/another', 15);
INSERT INTO product(feed_id, product_name, affiliate_link_url, price) VALUES (2, 'First Amazon Product', 'http://www.amazon.co.uk/something', 32.45);
INSERT INTO product(feed_id, product_name, affiliate_link_url, price) VALUES (2, 'Another Amazon Product', 'http://www.amazon.co.uk/another', 120);
INSERT INTO product(feed_id, product_name, affiliate_link_url, price) VALUES (2, 'Third Amazon Product', 'http://www.amazon.co.uk/third', 220);
```

Create MySQL connection via FuturePDO:
```
$pdo = new FuturePDO('mysql', '127.0.0.1', 'user', 'password', 'database_name');
if ($pdo->connect() === false) {
        throw new \Exception('Cannot connect to the database');
}

```

Fetch data grom the database:
```
$query = $pdo->query(
        "SELECT my_column
        FROM my_table
        WHERE some_value = ?",
        [$myValue]
);

$results = $query->fetchAll(PDO::FETCH_COLUMN);
$query->closeCursor();
```
