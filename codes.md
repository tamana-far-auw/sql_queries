SCHEMA : 
	
	CREATE TABLE table_data(
	    	user_id INTEGER PRIMARY KEY AUTO_INCREMENT, 
	      	user_name VARCHAR(50),
	      	user_email TEXT,
	      	card VARCHAR(50), 
	      	price REAL
	    );
	    
	    
	-- NEXT TABLE TO CONNECT WITH FIRST ONE
	
	CREATE TABLE products(
		product_id INTEGER PRIMARY KEY AUTO_INCREMENT,
	  	user_id INTEGER UNIQUE,
	    product_name VARCHAR(100)
	 );
	 
	 INSERT INTO products(user_id,product_name) VALUE ((SELECT user_id FROM table_data  LIMIT 1), 
	   'Book'
	 ),((SELECT user_id FROM table_data  LIMIT 1),'Pen'),((SELECT user_id FROM table_data  LIMIT 1),'Pencil');

    
    INSERT INTO table_data( 
      	user_name ,
      	user_email ,
      	card , 
      	price 
    ) VALUES
    ( 'TAMANA', 'AUW242106@AUW.EDU.BD','FIRST,SECOND',23.5 
    );
    
    INSERT INTO table_data(
      user_name ,
      	user_email ,
      	card , 
      	price 
    ) VALUES
    ( 'SAMIRA', 'AUW242@AUW.EDU.BD','3.3 ,4',30
    );
    
    UPDATE table_data SET user_name = CONCAT(user_name, ' FARZAMI')
    

	queries : 
		 -- SELECT * FROM table_data  WHERE LENGTH(user_name) <= 5
		-- SELECT
		-- user_name AS name,
		-- card AS products
		-- FROM table_data
		-- -- WHERE to_tsvector(name) @@ to_tsquery('FARZAMI') THIS NOT WORK IT IS POSTSQL
		-- WHERE user_name LIKE '%FARZAMI%';
	
	SELECT user_name, 
	(SELECT product_name FROM products WHERE products.product_id = table_data.user_id) 
	AS my_data 
	FROM table_data;

	Assignmet 
	CREATE TABLE DeliveryInformation ( delivery_id INT PRIMARY KEY, destination VARCHAR(100) NOT NULL, delivery_time VARCHAR(20) NOT NULL ); 

	CREATE TABLE OrderInformation ( order_id INT PRIMARY KEY, food_item VARCHAR(100) NOT NULL, quantity INT NOT NULL, delivery_id INT, FOREIGN KEY (delivery_id) REFERENCES DeliveryInformation(delivery_id) );
	
	CREATE TABLE DeliveryStatus ( status_id INT PRIMARY KEY, delivery_id INT, delivered VARCHAR(3) CHECK (delivered IN ('Yes','No')), FOREIGN KEY (delivery_id) REFERENCES DeliveryInformation(delivery_id) ); 
	
	INSERT INTO DeliveryInformation VALUES (1, 'Campus Hall', '12:00 PM'), (2, 'Library', '12:30 PM'), (3, 'Admin Building', '01:00 PM'), (4, 'Dormitory A', '02:00 PM'), (5, 'Dormitory B', '02:30 PM'); 
	
	 INSERT INTO OrderInformation VALUES (1, 'Burger', 2, 1), (2, 'Pizza', 1, 2), (3, 'Sandwich', 3, 3), (4, 'Pasta', 2, 4), (5, 'Fried Rice', 1, 5);
	
	INSERT INTO DeliveryStatus VALUES (1, 1, 'Yes'), (2, 2, 'No'), (3, 3, 'Yes'), (4, 4, 'No'), (5, 5, 'Yes');
	
	

