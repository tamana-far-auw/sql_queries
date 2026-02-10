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
    

 -- queries : 
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

