# Book API

A small ASP.NET Core Web API that stores books in SQL Server and exposes create, read, update and delete endpoints for them.

## What it does

- **Book records.** A book has an id, a title, an author and a publication year. The API lists all books, fetches one by id, adds, updates and deletes them.
- **Status codes that match the outcome.** Reads return 200, a create returns 201 with a `Location` header pointing at the new book, updates and deletes return 204. A missing id returns 404, and an update whose body id differs from the URL id returns 400.
- **Seeded data.** The migrations create the `Book` table and insert five books (1984, To Kill a Mockingbird, The Great Gatsby, Pride and Prejudice, The Catcher in the Rye), so the API has data on first run.
- **Swagger UI.** In the Development environment the app serves an OpenAPI document and Swagger UI at `/swagger`.

## How it is built

| Part | Technology |
|------|------------|
| App framework | ASP.NET Core Web API on .NET 8 |
| Data access | Entity Framework Core 8.0.11 (`Microsoft.EntityFrameworkCore.SqlServer`) |
| Database | SQL Server |
| API docs | Swashbuckle.AspNetCore 8.1.0 |

The project lives in the `API` folder. `Controllers/BooksController.cs` holds all five actions and talks to the database directly through `Data/APIContext.cs`, the EF Core `DbContext`; there is no separate service layer. `Models/Book.cs` is the only entity, and the seed rows are declared in `APIContext.OnModelCreating`. `Program.cs` registers the controllers, the `DbContext` and Swagger, and every database call is async.

## API

| Method | Path | What it does |
|--------|------|--------------|
| GET | `/api/books` | Returns all books. |
| GET | `/api/books/{id}` | Returns one book, or 404 if the id does not exist. |
| POST | `/api/books` | Creates a book and returns it with its new id (201). |
| PUT | `/api/books/{id}` | Replaces the title, author and year of a book. The body must carry the same `id` as the URL. Returns 204. |
| DELETE | `/api/books/{id}` | Deletes a book. Returns 204, or 404 if the id does not exist. |

Body for a POST:

```json
{
  "title": "C# / .NET",
  "author": "Ani",
  "yearPublished": 2025
}
```

A PUT uses the same shape plus `"id"`. `API/API.http` has sample requests for the REST Client extension or Visual Studio.

## Run it locally

You need the .NET 8 SDK (or later), a SQL Server instance (SQL Server Express is enough), and the EF Core command-line tool:

```bash
dotnet tool install --global dotnet-ef
```

1. Clone the repository and go to the project folder.

   ```bash
   git clone https://github.com/anipiro/Book-API.git
   cd Book-API/API
   ```

2. Set the connection string. It lives in `API/appsettings.json` under `ConnectionStrings:DefaultConnection`. The committed value uses a local SQL Server Express instance and a database called `BookDB`. To use another server, change it:

   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=YOUR_SERVER;Database=BookDB;Trusted_Connection=True;TrustServerCertificate=True"
   }
   ```

3. Create the database, the table and the seed rows.

   ```bash
   dotnet restore
   dotnet ef database update
   ```

4. Start the API.

   ```bash
   dotnet run
   ```

`dotnet run` uses the `http` launch profile and listens on `http://localhost:5216`; Swagger UI is at `http://localhost:5216/swagger`. To serve HTTPS on `https://localhost:7260` as well, use `dotnet run --launch-profile https`.

Released under the MIT License; see `LICENSE`.
