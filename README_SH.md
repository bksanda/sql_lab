#SQL Lab


##Getting Started

To get started we'll need to import the booktown.sql file.

1. open terminal
2. use the command `psql -f booktown.sql`
3. type `sql` to open your psql console
4. type \list to ensure the booktown database was successfully completed

##Instructions
Provide the follow sql statements below each question.

##Order
1. Find all subjects sorted by subject

	* SELECT * FROM subjects ORDER BY subject ASC;
	
2. Find all subjects sorted by location
	* SELECT * FROM subjects ORDER BY location ASC; 

##Where
1. Find the book "Little Women"
	* SELECT * FROM books WHERE title = 'Little Women';
2. Find all books containing the word "Python"
	* SELECT * FROM books WHERE title LIKE '%Python%';
3. Find all subjects with the location "Main St" sort them by subject
	* SELECT * FROM subjects WHERE location = 'Main St' ORDER by subject ASC;

##Joins

1. Find all books about Computers list ONLY book title
	* //SELECT * FROM subjects JOIN books on subjects.subject = 'Computers' ORDER BY title ASC; (NOT SURE)
	* ANS = SELECT books.title FROM books JOIN subjects ON books.subject_id = subjects.id WHERE subject ILIKE '%computers%';

* Find all books and display ONLY
	* Book title
	* Author's first name
	* Author's last name
	* Book subject

	* // SELECT book.title, authors.first_name, authors_lastname, subject.subject FROM books JOIN authors ON books.author_id = authors.last_name AND books.author_id = authors.first_name JOIN subjects ON books.subject_id = subjects.subject; (NOT SURE)
	* ANS =SELECT books.title, authors.first_name, authors.last_name, subjects.subject FROM books JOIN authors ON books.author_id = authors.id JOIN subjects ON books.subject_id = subjects.id; 
	* ANS with concat = SELECT books.title, concat(authors.first_name, authors.last_name) AS authors_fullname, subjects.subject FROM books JOIN authors ON books.author_id = authors.id JOIN subjects ON books.subject_id = subjects.id;
	
* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and price
	* ANS = SELECT books.title, stock.cost FROM books JOIN editions ON books.id = editions.book_id JOIN stock ON editions.isbn = stock.isbn; 
	* ANS = SELECT books.title, stock.retail FROM books JOIN editions ON books.id = editions.book_id JOIN stock ON editions.isbn = stock.isbn ORDER BY stock.cost DESC;

* Find the book "Dune" and display ONLY
	* Book title
	* ISBN number
	* Publisher name
	* Retail price
	
	* //SELECT books.title, stock.isbn, publishers.name, stock.retail FROM books JOIN editions ON books.id = editions.book_id JOIN stock ON editions.isbn = stock.isbn JOIN shipments ON stock.isbn = shipments.isbn JOIN publishers ON shipments.id = publishers.id WHERE title ILIKE '%Dune%';
	
	*ANS= SELECT books.title, stock.isbn, publishers.name, stock.cost FROM books JOIN editions ON books.id = editions.book_id JOIN stock ON editions.isbn = stock.isbn JOIN publishers ON editions.publisher_id = publishers.id WHERE title ILIKE '%Dune%';  

* Find all shipments sorted by ship date display ONLY:
	* Customer first name
	* Customer last name
	* ship date
	* book title
	
	* ANSWER = SELECT customers.first_name, customers.last_name, shipments.ship_date, books.title FROM books JOIN editions ON books.id = editions.book_id JOIN shipments ON editions.isbn = shipments.isbn JOIN customers ON shipments.customer_id = customers.id; 

* Find all books that have either a 2nd or 3rd edition associated to it display ONLY:
	* Book title
	* Book Author
	* Edition Number
	
	* ANSWER = SELECT books.title, authors.first_name, authors.last_name, editions.edition FROM books JOIN authors ON books.author_id = authors.id JOIN editions ON books.id = editions.book_id WHERE edition IN (2,3);
	
	OR 
	
	CONCATENATE NAME
	
	* SELECT books.title, authors.first_name || ' ' || authors.last_name, editions.edition FROM books JOIN authors ON books.author_id = authors.id JOIN editions ON books.id = editions.book_id WHERE edition IN (2,3);
