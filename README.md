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
|            | purchase_amount            | DECIMAL(10, 2)                                                   |
| *Sales*      | sale_id                    | SERIAL PRIMARY KEY                                               |
|            | book_id                    | INT REFERENCES Books(book_id)                                     |
|            | sale_quantity              | INT                                                              |
|            | sale_date                  | DATE                                                             |

## SQL Queries to Create Tables with required Attributes

```sql
CREATE TABLE Authors (
    author_id SERIAL PRIMARY KEY,
    author_name VARCHAR(255) NOT NULL,
    author_bio TEXT
);

CREATE TABLE Publishers (
    publisher_id SERIAL PRIMARY KEY,
    publisher_name VARCHAR(255) NOT NULL,
    publisher_address VARCHAR(255),
    publisher_phone VARCHAR(50)
);

CREATE TABLE Books (
    book_id SERIAL PRIMARY KEY,
    book_title VARCHAR(255) NOT NULL,
    author_id INT REFERENCES Authors(author_id),
    publisher_id INT REFERENCES Publishers(publisher_id),
    book_genre VARCHAR(255),
    book_format VARCHAR(50) CHECK (book_format IN ('physical', 'ebook', 'audiobook')),
    book_price FLOAT,
    book_publish_date DATE,
    book_avg_rating FLOAT
);

CREATE TABLE Customers (
    customer_id SERIAL PRIMARY KEY,
    customer_name VARCHAR(255) NOT NULL,
    customer_email VARCHAR(255) NOT NULL,
    customer_phone VARCHAR(50),
    customer_address VARCHAR(255),
    customer_total_spent FLOAT,
    customer_last_purchase_date DATE
);

CREATE TABLE Reviews (
    review_id SERIAL PRIMARY KEY,
    book_id INT REFERENCES Books(book_id),
    customer_id INT REFERENCES Customers(customer_id),
    review_rating INT,
    review_text TEXT,
    review_date DATE
);

CREATE TABLE Purchases (
    purchase_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES Customers(customer_id),
    book_id INT REFERENCES Books(book_id),
    purchase_date DATE,
    purchase_quantity INT,
    purchase_amount DECIMAL(10, 2)
);

CREATE TABLE Sales (
    sale_id SERIAL PRIMARY KEY,
    book_id INT REFERENCES Books(book_id),
    sale_quantity INT,
    sale_date DATE
);
```

## Insert Queries for all the Tables

```sql
INSERT INTO public.authors(
    author_name, author_bio)
    VALUES ('William Shakespeare', 'William Shakespeare was an English playwright, poet and actor. He is widely regarded as the greatest writer in the English language and the world''s pre-eminent dramatist'),
    ('Charles Dickens','Charles John Huffam Dickens was an English novelist, journalist, short story writer and social critic.'),
    ('J. K. Rowling','Joanne Rowling CH OBE FRSL, known by her pen name J. K. Rowling, is a British author and philanthropist. She wrote Harry Potter, a seven-volume fantasy series published from 1997 to 2007.'),
    ('Agatha Christie','Dame Agatha Mary Clarissa Christie, Lady Mallowan, DBE was an English writer known for her 66 detective novels and 14 short story collections, particularly those revolving around fictional detectives Hercule Poirot and Miss Marple.');

INSERT INTO public.publishers(
    publisher_id, publisher_name, publisher_address, publisher_phone)
    VALUES (1, 'Penguin Random House', '1745 Broadway, New York, NY 10019', '212-555-1234'),
           (2, 'HarperCollins', '195 Broadway, New York, NY 10007', '212-555-5678'),
           (3, 'Hachette Book Group', 'New York, NY 10104', '212-555-9101'),
           (4, 'Simon & Schuster', '1230 Avenue of the Americas, New York, NY 10020', '212-555-3145'),
           (5, 'Macmillan Publishers', 'New York, NY 10271', '212-555-2789'),
           (6, 'Scholastic', '604 King Street West, Toronto,  Ontario M5V 1E1', '416-849-7912'),
           (7, 'Oxford University Press', 'Oxford England, United Kingdom', '212-555-6789'),
           (8, 'Cengage Learning', '10650 Toebben Drive, Independence, KY 41051', '800-354-9706');

INSERT INTO public.books(
    book_title, author_id, publisher_id, book_genre, book_format, book_price, book_publish_date, book_avg_rating)
    VALUES ('Hamlet', 1, 1, 'Fiction', 'physical', 15.99, '1603-01-01', 4.8),
    ('Great Expectations', 2, 2, 'Fiction', 'ebook', 12.99, '1861-01-01', 4.6),
    ('Harry Potter and the Sorcerer''s Stone', 3, 3, 'Fantasy', 'audiobook', 19.99, '1997-06-26', 4.9),
    ('Murder on the Orient Express', 4, 1, 'Mystery', 'physical', 14.99, '1934-01-01', 4.7),
    ('Macbeth', 1, 1, 'Fiction', 'physical', 14.99, '1606-01-01', 4.7),
    ('A Tale of Two Cities', 2, 2, 'Fiction', 'ebook', 13.99, '1859-01-01', 4.5),
    ('Harry Potter and the Chamber of Secrets', 3, 3, 'Fantasy', 'audiobook', 18.99, '1998-07-02', 4.8),
    ('The ABC Murders', 4, 1, 'Mystery', 'physical', 13.99, '1936-01-01', 4.6);

INSERT INTO public.customers(
    customer_name, customer_email, customer_phone, customer_address, customer_total_spent, customer_last_purchase_date)
    VALUES ('Binita Khua', 'binitakhua@gmail.com', '548-555-2586', 'Waterloo', 47.97, '2024-06-24'),
           ('Aayushi Mehta', 'Amehta5253@gmail.com', '548-555-7542', 'Kitchener', 48.97, '2024-06-23'),
           ('Bansi Kalariya', 'Bkalariya5738@gmail.com', '548-555-7851', 'Kitchener', 57.96, '2024-06-22');

INSERT INTO public.purchases(
    customer_id, book_id, purchase_date, purchase_quantity, purchase_amount)
    VALUES 
    (1, 1, '2024-06-24', 1, 15.99),
    (1, 2, '2024-06-24', 1, 12.99),
    (2, 3, '2024-06-23', 1, 19.99),
    (2, 4, '2024-06-23', 1, 14.99),
    (3, 5, '2024-06-22', 1, 14.99),
    (3, 6, '2024-06-22', 1, 13.99),
    (1, 7, '2024-06-24', 1, 18.99),
    (2, 8, '2024-06-23', 1, 13.99),
    (3, 1, '2024-06-22', 1, 15.99),
    (3, 2, '2024-06-22', 1, 12.99);

INSERT INTO public.sales(
    book_id, sale_quantity, sale_date)
    VALUES 
    (1, 50, '2024-06-24'),
    (2, 45, '2024-06-24'),
    (3, 60, '2024-06-23'),
    (4, 40, '2024-06-23'),
    (5, 35, '2024-06-22'),
    (6, 30, '2024-06-22'),
    (7, 20, '2024-06-24'),
    (8, 25, '2024-06-23');

INSERT INTO public.reviews(
    book_id, customer_id, review_rating, review_text, review_date)
    VALUES 
    (1, 1, 5, 'A timeless classic.', '2024-06-25'),
    (2, 1, 4, 'An engaging read.', '2024-06-25'),
    (3, 2, 5, 'Magical and captivating.', '2024-06-24'),
    (4, 2, 4, 'A thrilling mystery.', '2024-06-24'),
    (5, 3, 4, 'A powerful tragedy.', '2024-06-23'),
    (6, 3, 4, 'A moving story.', '2024-06-23'),
    (7, 1, 5, 'Even better than the first book.', '2024-06-25'),
    (8, 2, 4, 'A cleverly plotted mystery.', '2024-06-24'),
    (1, 3, 5, 'Another masterpiece by Shakespeare.', '2024-06-23'),
    (2, 3, 5, 'Dickens at his best.', '2024-06-23');
```
## CRUD Operations for Customer Table

```sql

-- Creating a Customer
INSERT INTO public.customers(
    customer_name, customer_email, customer_phone, customer_address, customer_total_spent, customer_last_purchase_date)
VALUES ('Kevin Kang', 'kevin.kang@gmail.com', '555-555-5555', 'KWC', 35.97, '2024-06-25');

-- Reading all Customers
SELECT * FROM public.customers;

-- Read a specific customer by ID
SELECT * FROM public.customers WHERE customer_id = 1;

-- Updating the Customer details
UPDATE public.customers
SET customer_total_spent = 20.98, customer_last_purchase_date = '2024-06-26'
WHERE customer_id = 4;

-- Deleting a Customer with id 4
DELETE FROM public.customers WHERE customer_id = 4;

```
## Identifying DDL commands for Customer table

```sql

CREATE TABLE Customers (
    customer_id SERIAL PRIMARY KEY,
    customer_name VARCHAR(255) NOT NULL,
    customer_email VARCHAR(255) NOT NULL,
    customer_phone VARCHAR(50),
    customer_address VARCHAR(255),
    customer_total_spent FLOAT,
    customer_last_purchase_date DATE
);
```
## Identifying DML commands for Customer table

```sql
-- Creating a Customer
INSERT INTO public.customers(
    customer_name, customer_email, customer_phone, customer_address, customer_total_spent, customer_last_purchase_date)
VALUES ('Kevin Kang', 'kevin.kang@gmail.com', '555-555-5555', 'KWC', 35.97, '2024-06-25');

-- Reading all Customers
SELECT * FROM public.customers;

-- Read a specific customer by ID
SELECT * FROM public.customers WHERE customer_id = 1;

-- Updating the Customer details
UPDATE public.customers
SET customer_total_spent = 20.98, customer_last_purchase_date = '2024-06-26'
WHERE customer_id = 4;

-- Deleting a Customer with id 4
DELETE FROM public.customers WHERE customer_id = 4;
```

## Queries 

**Power writers (authors) with more than 1 book in the for the Fantasy genre published within the last 200 years**

```sql

-- The book_genre can be changed to Mystery and Fiction

SELECT author_id, author_name
FROM public.authors
WHERE author_id IN (
    SELECT author_id
    FROM public.books
    WHERE book_genre = 'Fantasy' AND book_publish_date > (CURRENT_DATE - INTERVAL '200 years')
    GROUP BY author_id
    HAVING COUNT(*) > 1
);

```

**Loyal Customers who has spent more than 50 dollars in the last year**

```sql
SELECT customer_id, customer_name
FROM public.customers
WHERE customer_total_spent > 50 AND customer_last_purchase_date > (CURRENT_DATE - INTERVAL '1 year');

```

**Well Reviewed Books (Books with a better user rating than average)**

```sql
SELECT book_id, book_title
FROM public.books
WHERE book_avg_rating > (SELECT AVG(book_avg_rating) FROM public.books);
```

**The most popular genre by sales**

```sql
SELECT book_genre
FROM public.books b
JOIN public.sales s ON b.book_id = s.book_id
GROUP BY book_genre
ORDER BY SUM(s.sale_quantity) DESC
LIMIT 1;
```

**The 10 most recent posted reviews by Customers**

```sql
SELECT *
FROM public.reviews
ORDER BY review_date DESC
LIMIT 10;
```

## Typescript Interface for Customers Table

```typescript

interface Customer {
  customer_id: number;
  customer_name: string;
  customer_email: string;
  customer_phone: string;
  customer_address: string;
  customer_total_spent: number;
  customer_last_purchase_date: Date;
}

interface CustomerService {
  createCustomer(customer: Customer): Promise<Customer>;
  readCustomer(customer_id: number): Promise<Customer | null>;
  updateCustomer(customer: Partial<Customer>): Promise<Customer | null>;
  deleteCustomer(customer_id: number): Promise<boolean>;
}

class CustomerServiceImpl implements CustomerService {
  private customers: Customer[] = [];
  private nextId: number = 1;

  async createCustomer(customer: Customer): Promise<Customer> {
    customer.customer_id = this.nextId++;
    this.customers.push(customer);
    return customer;
  }

  async readCustomer(customer_id: number): Promise<Customer | null> {
    const customer = this.customers.find(c => c.customer_id === customer_id);
    return customer || null;
  }

  async updateCustomer(customer: Partial<Customer>): Promise<Customer | null> {
    const index = this.customers.findIndex(c => c.customer_id === customer.customer_id);
    if (index === -1) {
      return null;
    }
    this.customers[index] = { ...this.customers[index], ...customer };
    return this.customers[index];
  }

  async deleteCustomer(customer_id: number): Promise<boolean> {
    const index = this.customers.findIndex(c => c.customer_id === customer_id);
    if (index === -1) {
      return false;
    }
    this.customers.splice(index, 1);
    return true;
  }
}

// Example usage
const customerService = new CustomerServiceImpl();

const newCustomer: Customer = {
  customer_id: 0, // This will be set by createCustomer
  customer_name: 'Binita Khua',
  customer_email: 'binitakhua@gmail.com',
  customer_phone: '548-555-2586',
  customer_address: 'Waterloo',
  customer_total_spent: 250.00,
  customer_last_purchase_date: new Date('2024-06-24')
};

async function runExample() {
  await customerService.createCustomer(newCustomer);
  console.log('Customer created:', newCustomer);

  const customer = await customerService.readCustomer(newCustomer.customer_id);
  console.log('Read customer:', customer);

  await customerService.updateCustomer({ customer_id: newCustomer.customer_id, customer_total_spent: 300.00 });
  console.log('Updated customer:', await customerService.readCustomer(newCustomer.customer_id));

  await customerService.deleteCustomer(newCustomer.customer_id);
  console.log('Deleted customer:', await customerService.readCustomer(newCustomer.customer_id));
}

runExample();
```

## References for Insert Data

### Authors and their Bios:
- [William Shakespeare](https://en.wikipedia.org/wiki/William_Shakespeare)
- [Charles Dickens](https://en.wikipedia.org/wiki/Charles_Dickens)
- [J.K. Rowling](https://en.wikipedia.org/wiki/J._K._Rowling)
- [Agatha Christie](https://en.wikipedia.org/wiki/Agatha_Christie)

### Publishers and their Addresses:
- [Penguin Random House](https://www.penguinrandomhouse.com/)
- [HarperCollins](https://www.harpercollins.com/)
- [Hachette Book Group](https://www.hachettebookgroup.com/)
- [Simon & Schuster](https://www.simonandschuster.com/)
- [Macmillan Publishers](https://us.macmillan.com/)
- [Scholastic](https://www.scholastic.com/)
- [Oxford University Press](https://global.oup.com/)
- [Cengage Learning](https://www.cengage.com/)

### Books and their Details:
- [Hamlet](https://en.wikipedia.org/wiki/Hamlet)
- [Great Expectations](https://en.wikipedia.org/wiki/Great_Expectations)
- [Harry Potter and the Sorcerer's Stone](https://en.wikipedia.org/wiki/Harry_Potter_and_the_Philosopher%27s_Stone)
- [Murder on the Orient Express](https://en.wikipedia.org/wiki/Murder_on_the_Orient_Express)
- [Macbeth](https://en.wikipedia.org/wiki/Macbeth)
- [A Tale of Two Cities](https://en.wikipedia.org/wiki/A_Tale_of_Two_Cities)
- [Harry Potter and the Chamber of Secrets](https://en.wikipedia.org/wiki/Harry_Potter_and_the_Chamber_of_Secrets)
- [The ABC Murders](https://en.wikipedia.org/wiki/The_A.B.C._Murders)

