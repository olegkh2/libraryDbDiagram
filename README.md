# Library System Database UML Diagram

This project is a database schema designed to manage the processes of a library network. It tracks the libraries, books, authors, genres, languages, readers, and the loaning of books. The schema supports features like borrowing and returning books, managing multiple libraries, and tracking the availability of books across libraries.

The schema is designed with scalability in mind, allowing for easy expansion and adding new features as the system evolves.

## UML Diagram
![Diagram]([https://github.com/jon/coolproject/raw/master/image/image.png](https://github.com/olegkh2/libraryDbDiagram/blob/main/Libraries%20DB%20Diagram.png))

## Database Tables

### 1. **Books Table**
Stores information about the books in the library network.

### 2. **Authors Table**
Stores biographical information about authors.

### 3. **Libraries Table**
Stores information about each library branch in the network.

### 4. **Readers Table**
Stores information about individuals who are members of the library and can borrow books.

### 5. **Loans Table**
Tracks the loan transactions between readers and the library system.

### 6. **Books_Libraries , Loan_Book, Book_Genre, Book_Author Tables**
Junction tables, allowing many-to-many relations (ex. One author can have many books, and one book can have many authors).


### 7. **Genres, Languages, Statuses Tables**
Stores different information for classification. 
Added to normalize the database main tables. Also, possible to add some other tables in the future based on requirements.  

## Relationships

- **Books ↔ Authors**: Many-to-Many relationship. A book can have many authors, and an author can write multiple books. This is managed by the `Books_Authors` junction table.
- **Books ↔ Genres**: Many-to-Many relationship. A book belongs to many genres, and a genre can contain many books. This is managed by the `Books_Genres` junction table.
- **Books ↔ Languages**: Many-to-One relationship. A book is written in one language, but a language can be associated with many books.
- **Books ↔ Libraries**: Many-to-Many relationship. A book can be available in many libraries, and each library can hold many books. This is managed by the `Books_Libraries` junction table.
- **Readers ↔ Loans**: One-to-Many relationship. A reader can have many loans, but each loan is associated with one reader.
- **Loans ↔ Books**: Many-to-Many relationship. A loan can involve multiple books, and each book can be in many loans over time. This is managed by the `Books_Loans` junction table.
- **Loans ↔ Statuses**: Each loan has a status that tracks whether the book is borrowed, returned, overdue, etc.

## How It Works

- **Tracking Books**: Books are stored in libraries, and their availability is managed through the `Books_Libraries` table, which tracks how many copies are available in each library.
- **Loaning Books**: Readers can borrow books from any library. The `Loans` table tracks the loan transactions, and the `Books_Loans` table tracks the specific books borrowed in each transaction.
- **Statuses**: Loan statuses are used to determine if a book is borrowed, returned, overdue, or lost.

## Future Improvements

- Implementing a **LoanHistory** table to track status changes and overdue fee adjustments over time.
- Adding support for **reservations** and **book holds**.
- Extending the **Reader** table with more user activity metrics.
