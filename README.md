# SQL-PROJECT
# Library Management Schema

Below is the SQL schema for the Library Management System:

```sql
DROP SCHEMA IF EXISTS library_management;
CREATE SCHEMA IF NOT EXISTS library_management;

DROP TABLE IF EXISTS library_management.user_login;
CREATE TABLE IF NOT EXISTS library_management.user_login (
    user_id TEXT PRIMARY KEY,
    user_password TEXT,
    first_name TEXT,
    last_name TEXT,
    sign_up_on DATE DEFAULT CURRENT_DATE,
    email_id TEXT UNIQUE
);

DROP TABLE IF EXISTS library_management.publisher;
CREATE TABLE IF NOT EXISTS library_management.publisher (
    publisher_id TEXT PRIMARY KEY,
    publisher TEXT,
    distributor TEXT,
    releases_count INT DEFAULT 0,
    last_release DATE
);

DROP TABLE IF EXISTS library_management.author;
CREATE TABLE IF NOT EXISTS library_management.author (
    author_id TEXT PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    publications_count INT DEFAULT 0
);

DROP TABLE IF EXISTS library_management.books;
CREATE TABLE IF NOT EXISTS library_management.books (
    book_id TEXT PRIMARY KEY,
    book_code TEXT UNIQUE,
    book_name TEXT,
    author_id TEXT REFERENCES library_management.author(author_id),
    publisher_id TEXT REFERENCES library_management.publisher(publisher_id),
    book_version TEXT,
    release_date DATE,
    available_from DATE,
    is_available BOOLEAN DEFAULT TRUE
);

DROP TABLE IF EXISTS library_management.staff;
CREATE TABLE IF NOT EXISTS library_management.staff (
    staff_id TEXT PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    staff_role TEXT,
    start_date DATE DEFAULT CURRENT_DATE,
    last_date DATE,
    is_active BOOLEAN DEFAULT TRUE,
    work_shift_start TIME,
    work_shift_end TIME
);

DROP TABLE IF EXISTS library_management.readers;
CREATE TABLE IF NOT EXISTS library_management.readers (
    reader_id TEXT PRIMARY KEY,
    first_name TEXT,
    last_name TEXT,
    registered_on DATE DEFAULT CURRENT_DATE,
    books_issued_total INT DEFAULT 0,
    books_issued_current INT DEFAULT 0,
    is_issued BOOLEAN DEFAULT FALSE,
    last_issue_date DATE,
    total_fine DECIMAL(10, 2) DEFAULT 0.00,
    current_fine DECIMAL(10, 2) DEFAULT 0.00
);

DROP TABLE IF EXISTS library_management.books_issue;
CREATE TABLE IF NOT EXISTS library_management.books_issue (
    issue_id SERIAL PRIMARY KEY,
    book_id TEXT REFERENCES library_management.books(book_id),
    issued_to TEXT REFERENCES library_management.readers(reader_id),
    issued_on DATE DEFAULT CURRENT_DATE,
    return_on DATE,
    current_fine DECIMAL(10, 2) DEFAULT 0.00,
    fine_paid BOOLEAN DEFAULT FALSE,
    payment_transaction_id TEXT
);

DROP TABLE IF EXISTS library_management.settings;
CREATE TABLE IF NOT EXISTS library_management.settings (
    book_issue_count_per_reader INT DEFAULT 5,
    fine_per_day DECIMAL(10, 2) DEFAULT 1.00,
    book_return_in_days INT DEFAULT 14
);
