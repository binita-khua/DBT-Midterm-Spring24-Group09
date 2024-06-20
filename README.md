# DBT-Midterm-Spring24-Group09

## Duties Assigned to Team Members

**Aayushi Mehta**:
- Database schema design and identification of required tables.
- Identifying the data captured and the type for each attribute.
- Identifying 1 complete set of DDL and DML instructions for a chosen table.

**Bansi Kalariya**:
- Writing SQL queries to create the tables with the respective attributes.
- Writing SQL queries to insert data into all the tables.
- Identifying 1 complete set of DDL and DML instructions for a chosen table.

**Binita Khua**:
- Performing CRUD operations on the chosen table.
- Writing the 5 SQL queries to meet the specific requirements.
- Creating the TypeScript interface for any table to allow modification.

## Tables and Attributes

| Table      | Column                      | Type                                                           |
|------------|-----------------------------|----------------------------------------------------------------|
| *Authors*    | author_id                  | SERIAL PRIMARY KEY                                               |
|            | author_name                | VARCHAR(255) NOT NULL                                            |
|            | author_bio                 | TEXT                                                             |
| *Publishers* | publisher_id              | SERIAL PRIMARY KEY                                               |
|            | publisher_name            | VARCHAR(255) NOT NULL                                            |
|            | publisher_address         | VARCHAR(255)                                                     |
|            | publisher_phone           | VARCHAR(50)                                                      |
| *Books*      | book_id                    | SERIAL PRIMARY KEY                                               |
|            | book_title                 | VARCHAR(255) NOT NULL                                            |
|            | author_id                  | INT REFERENCES Authors(author_id)                                 |
|            | publisher_id               | INT REFERENCES Publishers(publisher_id)                          |
|            | book_genre                 | VARCHAR(255)                                                     |
|            | book_format                | VARCHAR(50) CHECK (book_format IN ('physical', 'ebook', 'audiobook')) |
|            | book_price                 | FLOAT                                                            |
|            | book_publish_date          | DATE                                                             |
|            | book_avg_rating            | FLOAT                                                            |
| *Customers*  | customer_id                | SERIAL PRIMARY KEY                                               |
|            | customer_name              | VARCHAR(255) NOT NULL                                            |
|            | customer_email             | VARCHAR(255) NOT NULL                                            |
|            | customer_phone             | VARCHAR(50)                                                      |
|            | customer_address           | VARCHAR(255)                                                     |
|            | customer_total_spent       | FLOAT                                                            |
|            | customer_last_purchase_date| DATE                                                             |
| *Reviews*    | review_id                  | SERIAL PRIMARY KEY                                               |
|            | book_id                    | INT REFERENCES Books(book_id)                                     |
|            | customer_id                | INT REFERENCES Customers(customer_id)                             |
|            | review_rating              | INT                                                              |
|            | review_text                | TEXT                                                             |
|            | review_date                | DATE                                                             |
| *Purchases*  | purchase_id                | SERIAL PRIMARY KEY                                               |
|            | customer_id                | INT REFERENCES Customers(customer_id)                             |
|            | book_id                    | INT REFERENCES Books(book_id)                                     |
|            | purchase_date              | DATE                                                             |
|            | purchase_quantity          | INT                                                              |
| *Sales*      | sale_id                    | SERIAL PRIMARY KEY                                               |
|            | book_id                    | INT REFERENCES Books(book_id)                                     |
|            | sale_quantity              | INT                                                              |
|            | sale_date                  | DATE                                                             |
