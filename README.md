# Inventory Management REST API

A Spring Boot REST API to manage products and stock levels.

## Tech stack
Java 17 · Spring Boot 3 · Spring Data JPA (Hibernate) · MySQL · Bean Validation · Lombok · Maven

## Features
- Full CRUD for products
- Increase / decrease stock with protection against negative stock
- Low-stock alert endpoint
- Filter by category and search by name
- Unique SKU check (409 Conflict on duplicates)
- Validation and clean JSON error responses

## Project structure
```
src/main/java/com/akash/inventory
├── controller   # REST endpoints
├── service      # business logic
├── repository   # database access (Spring Data JPA)
├── model        # Product entity
└── exception    # custom exceptions + global handler
```

## Run locally
1. Install Java 17+, Maven and MySQL.
2. Set your database password as an environment variable:
   ```bash
   export DB_PASSWORD=your_mysql_password      # Windows PowerShell: $env:DB_PASSWORD="your_mysql_password"
   ```
   Optional: `DB_USER` (default `root`), `DB_HOST`, `DB_PORT`, `DB_NAME` (default `inventory_db`).
3. Start the app:
   ```bash
   mvn spring-boot:run
   ```
   The database `inventory_db` and the `products` table are created automatically.
4. API is available at `http://localhost:8080/api/products`

Run tests: `mvn test`

## Endpoints
| Method | URL | Description |
|--------|-----|-------------|
| POST | `/api/products` | Create a product |
| GET | `/api/products` | List all (optional `?category=` or `?search=`) |
| GET | `/api/products/{id}` | Get one product |
| PUT | `/api/products/{id}` | Update a product |
| PATCH | `/api/products/{id}/stock?change=5` | Add stock (use a negative number to remove) |
| GET | `/api/products/low-stock?threshold=10` | Products below the threshold |
| DELETE | `/api/products/{id}` | Delete a product |

## Sample request
`POST /api/products`
```json
{ "name": "Keyboard", "sku": "KB-001", "quantity": 25, "price": 799.00, "category": "Electronics" }
```

## Error format
```json
{ "timestamp": "2026-09-29T11:30:00", "status": 404, "error": "Product not found: 99" }
```

A ready-to-import Postman collection is included: `postman_collection.json`.

## Author
Akash — Java Developer
