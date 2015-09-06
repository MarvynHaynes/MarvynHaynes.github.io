---
layout:     page
title:      Travel Agency Database (Detailed)
date:       2014-04-10 10:23:45
summary:    Detailed steps of creating a Travel Agency Database for a school project.
categories: Project
author:     Marvyn
thumbnail:  briefcase
tags:
 - Oracle
 - SQL
 - Project
---

<img class="thumbnail" src="{{ site.baseurl }}/projects/travelAgency/images/kon-tiki-frontpage.JPG" alt="Travel Agency Database Frontpage">

# Overview
This was a project I worked on with a 2 other members which we designed, created and implemented an Oracle database.  For our project we decided to create a database based from a fictional travel agency where you can book flights, hotels and car rentals.  To meet the needs of our customers, they have the choice of booking individual services or book all three as a package.  The database keeps track of a range of information such as:

* customer name
* address
* contact information
* order type
* all relating information based on customers' order (ex. hotel info, car rental info, flight info, etc.)
 
### Main Entities and Attributes
Once we discussed what information is needed to gather in order to build the database, we created a schema to help us visualize the layout:

#### Customer<br>
`Customer_ID` `F_Name` `L_Name` `Address` `Birth_Date` `Phone_No` `Accompany_No`

#### Orders<br>
`Order_ID` `Customer_ID` `Order_Date` `Total_Price` `Pay_Method`

#### TripType (*SuperType*)<br>
`Trip_ID` `Details`

#### Cars<br>
`Car_ID` `Car_Class` `Car_Make` `Car_Model` `Car_Color` `Max_Passenger` `Rate` `Agency_Name`

#### Flights<br>
`Flight_ID` `Flight_No` `Dep_Airport` `Arv_Airport` `Dep_Date` `Dep_Time` `Arv_Date` `Arv_Time` `Airline`

#### Hotels<br>
`Hotel_ID` `Name` `Address` `City` `State` `Country`

#### TakeFlights<br>
`Order_ID` `Class_Type` `Specific_Need`

#### StayHotels<br>
`Order_ID` `Hotel_ID` `CheckIn_Date` `CheckOut_Date` `Room_Type` `Guest_No` 

#### RentalCars<br>
`RentalAgreement_No` `Car_ID` `Order_ID` `Pickup_Date` `Pickup_Place` `DropOff_Date` `DropOff_Place`

### Logical and Relational Diagrams

<div class="row">
	<div class="col-md-6">
		<a href="{{ site.baseurl }}/projects/travelAgency/images/TravelAgnecy(Logical).JPG">
			<img class="thumbnail" src="{{ site.baseurl }}/projects/travelAgency/images/TravelAgnecy(Logical).jpg" alt="Travel Agency Logical Database Diagram" width="250" height="156">
		</a>
	</div>
	<div class="col-md-6">
		<a href="{{ site.baseurl }}/projects/travelAgency/images/TravelAgnecy(Relational).JPG">
			<img class="thumbnail" src="{{ site.baseurl }}/projects/travelAgency/images/TravelAgnecy(Relational).jpg" alt="Travel Agency Logical Database Diagram" width="250" height="156">
		</a>
	</div>
</div>

Once we agreed on the Database schema, the next step is to draft a Logical Diagram where we can specify each entity type and how it connects with the database.  We decided to use supertypes and subtypes to allow us to group certain entities that has attributes distinct from other types.  This also allows us to invoke inheritance since the subtypes will automatically contain attributes of supertypes.  You can find a good MSDN Lesson on SuperTypes and SubTypes [here](https://msdn.microsoft.com/en-us/library/cc505839.aspx). We used [Oracle SQL Datamodeler](http://www.oracle.com/technetwork/developer-tools/datamodeler/overview/index.html) (Free) to create the logical ER diagram using barker notation.  We then forward engineered the logical diagram to a relational ER diagram and made small adjustments to organize the diagram.

### Joins
After the Data Entry stage, we were required to produce results with advanced queries as they were requested by the professor. These included:

#### Natural Join

ex: *List customers that has picked up Economy Rental cars, sorted by customers' last name.*

{% highlight SQL %}
SELECT customers.l_name, customers.f_name, rentalcars.class_type
FROM customers
NATURAL JOIN orders
NATURAL JOIN service
NATURAL JOIN rentalcars
WHERE class_type = 'Economy'
ORDER BY customers.l_name;
{% endhighlight %}

#### Inner Join

ex: *List all economy flights arriving to Las Vegas, sorted by flight id.*

{% highlight SQL %}
SELECT takeflights.flight_id, takeflights.class_type, flights.arv_airport
FROM takeflights
INNER JOIN flights
ON takeflights.flight_id = flights.flight_id
WHERE takeflights.class_type = 'econom'
AND flights.arv_airport like '%Las Vegas%'
ORDER BY takeflights.flight_id;
{% endhighlight %}

#### Left Outer Join

ex: *List all flights arriving to San Francisco (SFO) Airport including non-booked flights.*

{% highlight SQL %}
SELECT flights.flight_id, flight_no, arv_airport, arv_Date_time, service_id, specific_need FROM flights
LEFT OUTER JOIN takeflights
ON takeflights.flight_id=flights.flight_id
WHERE arv_airport like '%SFO%';
{% endhighlight %}

### Top N Queries
Top-N queries provide a method for limiting the number of rows returned from ordered sets of data. They are extremely useful when you want to return the top or bottom "N" number of rows from a set or when you are paging through data.

ex: *A Top N query that displays the customers order information that paid the top-5 price.*

{% highlight SQL %}
SELECT * FROM
   (SELECT f_name, l_name, order_id, order_date, total_price FROM customers, orders 
   WHERE customers.customer_id=orders.customer_id  ORDER BY total_price desc)
WHERE rownum<=5;
{% endhighlight %}

### Cursors
Cursors in PL/SQL are used to retrieve more than one row at a time. The data that is stored in cursors is known as Active Data Set. These cursors are of two types:

* <u>Implicit Cursors</u> : predefined cursors
* <u>Explicit Cursors</u> : user defined cursors (which we provided)

ex: *Cursor that displays all rental companies in the 702 area code (Las Vegas).*

{% highlight SQL %}
SET SERVEROUTPUT ON
DECLARE
V_name rentalcaragencies.name%TYPE;
v_address rentalcaragencies.address%TYPE;
v_phone_no rentalcaragencies.Phone_no%TYPE;
CURSOR cur_rental_agencies IS 
SELECT name, address, Phone_no
FROM rentalcaragencies WHERE Phone_no LIKE '702%';
BEGIN
	OPEN cur_rental_agencies;
	LOOP
		FETCH cur_rental_agencies INTO V_name, v_address, v_phone_no;
		EXIT WHEN cur_rental_agencies%NOTFOUND;
		DBMS_OUTPUT.PUT_LINE('COMPANY NAME: '||v_name||', ADDRESS: '||v_address||', PHONE NO: '||v_phone_no);
	END LOOP;
CLOSE cur_rental_agencies;
END;
/
{% endhighlight %}

### Triggers 
A trigger is a named program unit that is stored in the database and fired (executed) in response to a specified event. The specified event is associated with either a table, a view, a schema, or the database, and it is one of the following:

* A database manipulation (**DML**) statement (DELETE, INSERT, or UPDATE)
* A database definition (**DDL**) statement (CREATE, ALTER, or DROP)
* A database operation (SERVERERROR, LOGON, LOGOFF, STARTUP, or SHUTDOWN)

For this project, we provided a working DML trigger that will display warning whenever the customers' prices have changed and keep track of changes.

**<u>Step1:</u>** Create a table to show changes in total_price*.

{% highlight SQL %}
CREATE TABLE orders_price_change (
	order_id INTEGER,
	new_price NUMBER(8,2),
	old_price NUMBER(8,2),
	CONSTRAINT order_id_FK FOREIGN KEY(order_id) 
	REFERENCES orders(order_id)
);
/
{% endhighlight %}

**<u>Step 2:</u>** Create a trigger that will display warning whenever prices are changed in Total_Price* then insert old and new price values into orders_price_change table.

{% highlight SQL %}
CREATE OR REPLACE TRIGGER price_changes_tr
BEFORE UPDATE OF Total_Price ON orders
FOR EACH ROW WHEN (new.total_price != old.total_price)
BEGIN
	dbms_output.put_line('WARNING! Price change detected under Orders.Total_Price!');
	dbms_output.put_line('Order ID = ' || :old.order_id);
	dbms_output.put_line('Old price = ' || :old.total_price);
	dbms_output.put_line('New price = ' || :new.total_price);
	INSERT INTO orders_price_change (order_id, old_price, new_price)
 	VALUES (:old.order_id, :old.total_price, :new.total_price);
END price_changes_tr;
/
{% endhighlight %}

**<u>Step 3:</u>** Any customers paid by cash, give them a 25% discount.

{% highlight SQL %}
UPDATE orders
SET total_price = total_price * 0.75
WHERE pay_method = 'Cash';
{% endhighlight %}

**<u>Step 4:</u>** Display changes made by trigger and stored into the orders_price_change table. This will display customers' **firstname, lastname, old price, new price** and **order id** by using an *Inner join* to combine the **ORDERS** and **CUSTOMER** tables in order to display the correct information.

{% highlight SQL %}
SELECT orders_price_change.order_id, orders_price_change.new_price, orders_price_change.old_price, customers.f_name, customers.l_name
FROM orders_price_change
INNER JOIN Orders
ON orders_price_change.order_id = orders.order_id
INNER JOIN customers
ON orders.customer_id = customers.customer_id
ORDER BY orders_price_change.order_id ASC;
{% endhighlight %}

# Conclusion
overall this was one of the best projects I have worked on throughout my program and building this database from scratch has provided me with an exceptional amount of knowledge.  Working with reliable team members that get along well is also important to tackle such big projects as this.  The feedback we recieved from our professor has been excellent and i feel the knowledge I gained here will come in handy in the future.