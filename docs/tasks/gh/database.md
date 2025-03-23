# **Database documents**

## **Database Schema**

<iframe frameborder="0" style="width:100%;height:676px;" src="https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=GH%20Task.drawio&page-id=0iseU8rjfOJXkiRPLyTz&dark=auto#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1eTmku-6ciqhX5Y2q62kzyoNo1PVqc2V8%26export%3Ddownload"></iframe>


```sql
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY,
    Name VARCHAR(255),
    Biography TEXT
);

CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY,
    Name VARCHAR(255),
    Description TEXT
);

CREATE TABLE Books (
    ISBN VARCHAR(13) PRIMARY KEY,
    Title VARCHAR(255),
    Publisher VARCHAR(255),
    PublicationDate DATE,
    AuthorID INT,
    CategoryID INT,
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID),
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);

CREATE TABLE Libraries (
    LibraryID INT PRIMARY KEY,
    Name VARCHAR(255),
    Location VARCHAR(255)
);

CREATE TABLE BookCopies (
    CopyID INT PRIMARY KEY,
    ISBN VARCHAR(13),
    LibraryID INT,
    FOREIGN KEY (ISBN) REFERENCES Books(ISBN),
    FOREIGN KEY (LibraryID) REFERENCES Libraries(LibraryID)
);

CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Username VARCHAR(255),
    Email VARCHAR(255)
);

CREATE TABLE Borrowings (
    BorrowingID INT PRIMARY KEY,
    CopyID INT,
    UserID INT,
    BorrowDate DATE,
    ReturnDate DATE,
    FOREIGN KEY (CopyID) REFERENCES BookCopies(CopyID),
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);
```

## Step 2: Brief Description of the Created Schema

The database schema is designed to manage books, authors, categories, libraries, users, and borrowing transactions efficiently. It includes tables for:

- **Authors**: Stores author information.
- **Categories**: Stores book categories.
- **Books**: Stores book details with foreign keys to authors and categories.
- **Libraries**: Stores library information.
- **BookCopies**: Manages multiple copies of books across libraries.
- **Users**: Stores user information.
- **Borrowings**: Tracks borrowing transactions with foreign keys to book copies and users.


## Step 3: Sample Queries with Their Purpose

Here are some sample SQL queries with their purposes:

### 1. Retrieve All Books by a Specific Author

**Purpose:** To list all books written by a particular author.

```sql
SELECT b.Title
FROM Books b
JOIN Authors a ON b.AuthorID = a.AuthorID
WHERE a.Name = 'John Doe';
```

### 2. Find Available Book Copies in a Library

**Purpose:** To identify available book copies in a specific library.

```sql
SELECT bc.CopyID, b.Title
FROM BookCopies bc
JOIN Books b ON bc.ISBN = b.ISBN
JOIN Libraries l ON bc.LibraryID = l.LibraryID
WHERE l.Name = 'Main Library' AND bc.CopyID NOT IN (
    SELECT CopyID FROM Borrowings WHERE ReturnDate IS NULL
);
```

### 3. List Borrowing History for a User

**Purpose:** To retrieve the borrowing history of a user.

```sql
SELECT b.Title, bo.BorrowDate, bo.ReturnDate
FROM Borrowings bo
JOIN BookCopies bc ON bo.CopyID = bc.CopyID
JOIN Books b ON bc.ISBN = b.ISBN
WHERE bo.UserID = 1;
```

### 4. Add a New Book to the Library

**Purpose:** To add a new book to the system.

```sql
INSERT INTO Books (ISBN, Title, Publisher, PublicationDate, AuthorID, CategoryID)
VALUES ('1234567890123', 'New Book Title', 'Publisher Name', '2023-01-01', 1, 1);

INSERT INTO BookCopies (CopyID, ISBN, LibraryID)
VALUES (1, '1234567890123', 1);
```

