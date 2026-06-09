# Book API – ASP.NET Core / EF Core / SQL Server

A RESTful API for managing books, showcasing backend development skills using **ASP.NET Core 8**, **Entity Framework Core**, and **SQL Server**.

---

## Overview

This project demonstrates:

- Full **CRUD operations**: Create, Read, Update, Delete books
- **Database migrations** and **data seeding** with Entity Framework Core
- Proper **REST API conventions** and **HTTP status codes** (200, 201, 204, 404)
- **Async database operations** with proper error handling
- **Swagger/OpenAPI** integration for interactive API documentation
- **HTTPS enforcement** for secure communications

---

## Key Features

- **GET /api/books** – Retrieve all books  
- **GET /api/books/{id}** – Retrieve a book by ID  
- **POST /api/books** – Add a new book  
- **PUT /api/books/{id}** – Update an existing book  
- **DELETE /api/books/{id}** – Remove a book  

Example JSON for POST/PUT:

```json
{
  "title": "C# / .NET",
  "author": "Ani",
  "yearPublished": 2025
}
```

---

## Tech Stack

* **Backend:** ASP.NET Core 8
* **ORM:** Entity Framework Core 8
* **Database:** SQL Server
* **API Documentation:** Swagger / OpenAPI
* **API Testing:** Postman / REST Client

---

## Skills Demonstrated

* Designed and implemented a **fully functional backend API**
* Used **EF Core migrations** to manage database schema changes
* Applied **real-world problem solving**: identity columns, data seeding, HTTP status handling
* Demonstrated ability to **debug and handle exceptions** in database operations
* Implemented **XML documentation** for comprehensive API documentation
* Configured **HTTPS redirection** for production security

## Seeded Data

The database is pre-populated with classic literature:

- 1984 – George Orwell (1949)  
- To Kill a Mockingbird – Harper Lee (1960)  
- The Great Gatsby – F. Scott Fitzgerald (1925)  
- Pride and Prejudice – Jane Austen (1813)  
- The Catcher in the Rye – J.D. Salinger (1951)

---

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/anipiro/Book-API.git
   cd Book-API
   ```

2. Configure the database connection in `appsettings.json`:

   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=YOUR_SERVER;Database=BookDB;Trusted_Connection=True;"
   }
   ```

3. Apply migrations and seed the database:

   ```bash
   dotnet ef database update
   ```

4. Run the application:

   ```bash
   dotnet run
   ```

5. Access the API via Swagger UI:

   ```
   https://localhost:5001/swagger
   ```