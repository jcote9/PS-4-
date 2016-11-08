# PS-4-

## Problem Set 4 

1. Create three tables: Customers, Orders, and OrderItems.

CREATE TABLE `Customers` (
  `customer_id` int(11) NOT NULL,
  `first_name` varchar(45) COLLATE utf8_unicode_ci NOT NULL,
  `last_name` varchar(45) COLLATE utf8_unicode_ci NOT NULL,
  `address` varchar(45) COLLATE utf8_unicode_ci NOT NULL,
  `zip_code` char(5) COLLATE utf8_unicode_ci NOT NULL,
  `email` varchar(45) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`customer_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `Orders` (
  `order_id` int(11) NOT NULL AUTO_INCREMENT,
  `customer_id` int(11) NOT NULL,
  `date` date NOT NULL,
  PRIMARY KEY (`order_id`),
  KEY `customer_id_idx` (`customer_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1029 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `OrderItems` (
  `orderitem_id` int(11) NOT NULL AUTO_INCREMENT,
  `order_id` int(11) DEFAULT NULL,
  `product_id` int(11) DEFAULT NULL,
  `quantity` varchar(45) COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`orderitem_id`),
  KEY `order_id_idx` (`order_id`),
  KEY `product_id_idx` (`product_id`),
  CONSTRAINT `order_id` FOREIGN KEY (`order_id`) REFERENCES `Orders` (`order_id`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `product_id` FOREIGN KEY (`product_id`) REFERENCES `Products` (`product_id`) ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;


2. Why do we need an OrderItems table?

We need an OrderItems table so each order can generate multiple rows in this table. Each item ordered is a product from the inventory, so each row has a product_id, which is linked to the products table. 

3. Create linked tables in MS Access.

4. Create forms to enter customer data.

5. Create a form with a subform to enter orders and order item.

6. Use forms created in 4 and 5 to insert Customers and Orders.  Add customers that have not made any orders. Make the number of entries relatively small.  Why?  

We keep it small so you can check your results by hand. The products table is so big you cant check them by hand. Keeping the number of entries small allows us to better understand sql, and search for possible problems and fixes.

7. Use SQL DML to INSERT records into Customers and Orders (and OrderItems).  

INSERT INTO `unemath_Cote`.`Customers` (`customer_id`, `first_name`, `last_name`, `address`, `zip_code`, `email`) VALUES ('910357861', 'Olivia', 'Finnerman', '74 Hillside Way', '01913', 'Ofinnerman99@gmail.com');

INSERT INTO `unemath_Cote`.`Customers` (`customer_id`, `first_name`, `last_name`, `address`, `zip_code`, `email`) VALUES ('910357863', 'Thomas', 'Tilton', '21 High Street', '04106', 'tttilton@yahoo.com');

Insert Into `unemath_Cote`.`Customers` Values ('910357888','James','Smith', '30 Oaks Drive', '03877','jsmith@une.edu');

Insert Into `unemath_Cote`.`Orders` Values ('1022','910357888','2016-11-11')

Insert Into `unemath_Cote`.`Orders` Values ('1023','910357863','2016-11-14')

INSERT INTO `unemath_Cote`.`OrderItems` (`order_id`, `product_id`, `quantity`) VALUES ('1027', '1001', '1');

INSERT INTO `unemath_Cote`.`OrderItems` (`order_id`, `product_id`, `quantity`) VALUES ('1027', '1007', '3');

INSERT INTO `unemath_Cote`.`OrderItems` (`order_id`, `product_id`, `quantity`) VALUES ('1027', '1004', '1');
8. Find all customer orders.

SELECT * FROM unemath_Cote.Orders;

Select Customers.customer_id, Customers.first_name, Customers.last_name, Orders.order_id from unemath_Cote.Customers inner join
unemath_Cote.Orders on Customers.customer_id = Orders.customer_id;

9. Select all customers that orders a certain product (This will depend on what data you entered into the table).  Find all customers that ordered product 3452.  

SELECT * from unemath_Cote.Products where product_id=3452;

Select Customers.customer_id, Customers.first_name, Customers.last_name, OrderItems.product_id from unemath_Cote.Customers inner join unemath_Cote.OrderItems where product_id=1001;

10. List 5 questions that you can answer from this data.

Which customer ordered two different orders?
Which product was ordered on November 14th, 2016?
How many total orders were made?
How many customers made orders on November 6th?
Which customer ordered a product whos product id is 1007? 


