# Application for Managing Publishing Houses

## 1. Description of Requirements:
The theme I chose for the course **"Databases"** was the management of publishing houses. In the first stage, I designed the database structure, including defining the architecture and functional requirements. Subsequently, I independently connected the database to the application and implemented the first page, which includes the login functionality through a login menu. I also completed all the project requirements, implementing operations for data management (insert, update, delete) and executing the necessary queries.

## 2. Tables Used:

- **PublishingHouses (Publishing Houses)**:
    - `ID_editura` (Primary Key)
    - `Name`
    - `Address`
    - `Phone`
    - `Email`
    - `Website`

- **Books (Books)**:
    - `ID_carte` (Primary Key)
    - `Title`
    - `Genre`
    - `Publication Date`
    - `ID_editura` (Foreign Key to PublishingHouses)
    - `ID_autori` (Foreign Key to Authors)

- **Authors (Authors)**:
    - `ID_autor` (Primary Key)
    - `First Name`
    - `Last Name`
    - `Nationality`

- **Contracts (Contracts)**:
    - `ID_contract` (Primary Key)
    - `ID_editura` (Foreign Key to PublishingHouses)
    - `ID_autor` (Foreign Key to Authors)
    - `Start Date`
    - `End Date`
    - `Contract Type`

- **Order (Orders)**:
    - `ID_comanda` (Primary Key)
    - `ID_client` (Foreign Key to Customers)
    - `Issue Date`
    - `Total`
    - `Order Status`

- **Order_Details (Order Details)**:
    - `ID_item` (Primary Key)
    - `ID_comanda` (Foreign Key to Order)
    - `Quantity`
    - `ID_carte` (Foreign Key to Books)
    - `Unit Price`

- **Customers (Customers)**:
    - `ID_client` (Primary Key)
    - `Name`
    - `Address`
    - `Email`
    - `Phone`

## 3. Relationships:

### 1:N Relationships:
1. **PublishingHouses (Publishing Houses) <-> Books (Books)**:
    - A publishing house can publish multiple books.
    - The relationship is managed through the foreign key `ID_editura` in the `Books` table.

2. **Authors (Authors) <-> Contracts (Contracts)**:
    - An author can have multiple contracts.
    - The relationship is managed through the foreign key `ID_autor` in the `Contracts` table.

3. **PublishingHouses (Publishing Houses) <-> Contracts (Contracts)**:
    - A publishing house can have multiple contracts.
    - The relationship is managed through the foreign key `ID_editura` in the `Contracts` table.

4. **Customers (Customers) <-> Orders**:
    - A customer can place multiple orders.
    - The relationship is managed through the foreign key `ID_client` in the `Orders` table.

5. **Orders <-> Order_Details (Order Details)**:
    - An order can have multiple details about books.
    - The relationship is managed through the foreign key `ID_comanda` in the `Order_Details` table.

6. **Books (Books) <-> Order_Details (Order Details)**:
    - A book can appear in multiple order details.
    - The relationship is managed through the foreign key `ID_carte` in the `Order_Details` table.

### N:N Relationships:
1. **Authors <-> Books (via Authors_Books)**:
    - An author can write multiple books, and a book can be written by multiple authors.
    - The relationship is managed by the intermediate table **Authors_Books** with the following columns:
        - `ID_autor` (Foreign Key to Authors)
        - `ID_carte` (Foreign Key to Books)

2. **PublishingHouses <-> Authors (via Contracts)**:
    - A publishing house can collaborate with multiple authors, and an author can have contracts with multiple publishing houses.
    - The relationship is managed through the **Contracts** table with the following columns:
        - `ID_editura` (Foreign Key to PublishingHouses)
        - `ID_autor` (Foreign Key to Authors)

3. **Books <-> Orders (via Order_Details)**:
    - An order can include multiple books, and a book can appear in multiple orders.
    - The relationship is managed through the **Order_Details** table with the following columns:
        - `ID_comanda` (Foreign Key to Orders)
        - `ID_carte` (Foreign Key to Books)

## 4. Design Stage:
The application is composed of two main parts: **frontend** and **backend**.

### Frontend (HTML):
- Creates the visual interface for the user (e.g., login forms, data display).
- Sends requests to the backend (e.g., when a "Submit" button is pressed).

### Backend (Python):
- Receives requests from the frontend.
- Processes the data, performs logical operations, and communicates with the MySQL database to save or retrieve information.

### Database (MySQL):
- Stores the necessary information for the application (e.g., books, orders).
- Returns the data to the backend for it to be sent back to the frontend.

## 5. Application Functionality:
To ensure the correct functioning of the application, the working environment must first be initialized by opening the MySQL Command Line, where the user must log in. Then, in another terminal, navigate to the directory containing the application files, and start the application using the command: `python3 main.py`.

## 6. Queries:

### Simple Queries:
1. **carti_si_edituri (Books and their publishing houses)**:
    - Finds the book titles and the publishing houses that published them.
    
2. **comenzi_si_clienti (Orders and their customers)**:
    - Lists the orders and the names of the customers who placed them.

3. **clienti_si_comenzi (Customers and their orders)**:
    - Displays customers and the IDs of their orders.

4. **carti_gen_specific (Books of a specific genre)**:
    - Selects book titles from a specific genre.

5. **comenzi_dupa_data (Orders after a certain date)**:
    - Finds orders placed after a specific date.

6. **clienti_cu_email (Customers with a specific email domain)**:
    - Finds customers who use a specific email domain.

### Complex Queries:
1. **autori_si_carti (Authors and their books)**:
    - Finds the names of authors and the titles of the books they have written.

2. **carti_si_comenzi (Books and their orders)**:
    - Displays the titles of books and the order IDs they appear in.

3. **comenzi_valoare_medie (Orders above the average value)**:
    - Selects orders whose total value is above the average of all orders.

4. **clienti_minim_2_comenzi (Customers with at least two orders)**:
    - Finds customers who have placed at least two orders.

5. **client_detalii (Customer details)**:
    - Displays information about a customer and their orders (including order status and total).
