# Java Document Task

## **Sample Classe Diagram**

!!! warning "Since you have not provided any details, I have choose to create a class digram for a library"

<iframe frameborder="0" style="width:100%;height:579px;" src="https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=GH%20Task.drawio&transparent=1&dark=auto#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1eTmku-6ciqhX5Y2q62kzyoNo1PVqc2V8%26export%3Ddownload" allowtransparency="true"></iframe>

### **Classes and Relationships**

- Book: Represents a book with attributes like title, publisher, author, and category. It has methods like `getTitle()` and `getAuthor()`.
- Author: Represents an author with attributes like name and biography. It has methods like `getName()` and `getBiography()`.
- Category: Represents a category of books (e.g., fiction, non-fiction) with attributes like name and description. It has methods like `getName()` and `getDescription()`.
- Library: Represents a library with attributes like name, location, and a list of books. It has methods like `addBook(Book book)` and `removeBook(Book book)`.
- User: Represents a user with attributes like username, email, and a list of borrowed books. It has methods like `borrowBook(Book book)` and `returnBook(Book book)`.
- Borrowing: Represents a borrowing transaction with attributes like borrowDate, returnDate, book, and user. It has methods like `getBorrowDate()` and `getReturnDate()`.

#### Relationships

- A book is written by one author (one-to-one).
- A book belongs to one category (one-to-one).
- A library can have many books (one-to-many).
- A user can borrow many books (one-to-many).
- A borrowing transaction involves one book and one user (many-to-one).


Let's enhance the system by adding more features and complexity to the class diagram and REST API specification.

## Step 1: Advanced Class Diagram

We'll expand the system to include additional classes for `User`, `Borrowing`, and `Category`. This will allow us to manage user accounts, borrowing history, and categorize books.

### Classes and Relationships

- **Book**: Represents a book with attributes like `title`, `publisher`, `author`, and `category`. It has methods like `getTitle()` and `getAuthor()`.
- **Author**: Represents an author with attributes like `name` and `biography`. It has methods like `getName()` and `getBiography()`.
- **Category**: Represents a category of books (e.g., fiction, non-fiction) with attributes like `name` and `description`. It has methods like `getName()` and `getDescription()`.
- **Library**: Represents a library with attributes like `name`, `location`, and a list of books. It has methods like `addBook(Book book)` and `removeBook(Book book)`.
- **User**: Represents a user with attributes like `username`, `email`, and a list of borrowed books. It has methods like `borrowBook(Book book)` and `returnBook(Book book)`.
- **Borrowing**: Represents a borrowing transaction with attributes like `borrowDate`, `returnDate`, `book`, and `user`. It has methods like `getBorrowDate()` and `getReturnDate()`.


## Advanced REST API Specification

Here is an enhanced specification for REST APIs that interact with these advanced classes:

### Book API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /books | Retrieve all books |
| GET    | /books/{id} | Retrieve a book by ID |
| POST   | /books | Create a new book |
| PUT    | /books/{id} | Update an existing book |
| DELETE | /books/{id} | Delete a book |
| GET    | /books/category/{categoryId} | Retrieve books by category ID |

### Author API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /authors | Retrieve all authors |
| GET    | /authors/{id} | Retrieve an author by ID |
| POST   | /authors | Create a new author |
| PUT    | /authors/{id} | Update an existing author |
| DELETE | /authors/{id} | Delete an author |

### Category API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /categories | Retrieve all categories |
| GET    | /categories/{id} | Retrieve a category by ID |
| POST   | /categories | Create a new category |
| PUT    | /categories/{id} | Update an existing category |
| DELETE | /categories/{id} | Delete a category |

### Library API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /libraries | Retrieve all libraries |
| GET    | /libraries/{id} | Retrieve a library by ID |
| POST   | /libraries | Create a new library |
| PUT    | /libraries/{id} | Update an existing library |
| DELETE | /libraries/{id} | Delete a library |
| POST   | /libraries/{id}/books | Add a book to a library |
| DELETE | /libraries/{id}/books/{bookId} | Remove a book from a library |

### User API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /users | Retrieve all users |
| GET    | /users/{id} | Retrieve a user by ID |
| POST   | /users | Create a new user |
| PUT    | /users/{id} | Update an existing user |
| DELETE | /users/{id} | Delete a user |
| POST   | /users/{id}/borrow | Borrow a book |
| POST   | /users/{id}/return | Return a borrowed book |

### Borrowing API

| Method | Path | Description |
|--------|------|-------------|
| GET    | /borrowings | Retrieve all borrowing transactions |
| GET    | /borrowings/{id} | Retrieve a borrowing transaction by ID |
| POST   | /borrowings | Create a new borrowing transaction |
| PUT    | /borrowings/{id} | Update an existing borrowing transaction |
| DELETE | /borrowings/{id} | Delete a borrowing transaction |

