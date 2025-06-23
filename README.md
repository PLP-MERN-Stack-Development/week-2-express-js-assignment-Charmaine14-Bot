# Product API Server

A RESTful API server built with Express.js for managing products. This server provides CRUD operations for products with authentication middleware and comprehensive error handling.

## Features

- **CRUD Operations**: Create, Read, Update, and Delete products
- **Authentication**: Token-based authentication for protected routes
- **Input Validation**: Comprehensive validation for product data
- **Error Handling**: Custom error handling middleware
- **Request Logging**: Automatic logging of all incoming requests
- **In-Memory Storage**: Simple in-memory database for development

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager

## Installation

1. Clone the repository or download the server files
2. Install dependencies:
   ```bash
   npm install express body-parser uuid
   ```
3. Start the server:
   ```bash
   node server.js
   ```

The server will start on `http://localhost:3000` by default.

## API Endpoints

### Public Endpoints

#### Get All Products
- **GET** `/api/products`
- **Description**: Retrieve all products
- **Response**: Array of product objects

#### Get Product by ID
- **GET** `/api/products/:id`
- **Description**: Retrieve a specific product by its ID
- **Parameters**: `id` - Product ID
- **Response**: Product object or 404 if not found

### Protected Endpoints (Require Authentication)

#### Create Product
- **POST** `/api/products`
- **Description**: Create a new product
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "name": "Product Name",
    "description": "Product description",
    "price": 99.99,
    "category": "electronics",
    "inStock": true
  }
  ```
- **Response**: Created product with generated ID

#### Update Product
- **PUT** `/api/products/:id`
- **Description**: Update an existing product
- **Headers**: `Authorization: Bearer <token>`
- **Parameters**: `id` - Product ID
- **Body**: Any combination of product fields to update
- **Response**: Updated product object

#### Delete Product
- **DELETE** `/api/products/:id`
- **Description**: Delete a product
- **Headers**: `Authorization: Bearer <token>`
- **Parameters**: `id` - Product ID
- **Response**: Deleted product object

## Authentication

Protected endpoints require an `Authorization` header with a Bearer token:

```
Authorization: Bearer your-token-here
```

**Note**: For demonstration purposes, any token starting with "Bearer " is accepted. In production, implement proper token validation.

## Sample Data

The server comes with sample products:

```json
[
  {
    "id": "1",
    "name": "Laptop",
    "description": "High-performance laptop with 16GB RAM",
    "price": 1200,
    "category": "electronics",
    "inStock": true
  },
  {
    "id": "2",
    "name": "Smartphone",
    "description": "Latest model with 128GB storage",
    "price": 800,
    "category": "electronics",
    "inStock": true
  },
  {
    "id": "3",
    "name": "Coffee Maker",
    "description": "Programmable coffee maker with timer",
    "price": 50,
    "category": "kitchen",
    "inStock": false
  }
]
```

## Testing the API

### Using curl

**Get all products:**
```bash
curl http://localhost:3000/api/products
```

**Get specific product:**
```bash
curl http://localhost:3000/api/products/1
```

**Create new product:**
```bash
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer test-token" \
  -d '{
    "name": "Wireless Mouse",
    "description": "Ergonomic wireless mouse",
    "price": 25.99,
    "category": "electronics",
    "inStock": true
  }'
```

**Update product:**
```bash
curl -X PUT http://localhost:3000/api/products/1 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer test-token" \
  -d '{
    "price": 1100,
    "inStock": false
  }'
```

**Delete product:**
```bash
curl -X DELETE http://localhost:3000/api/products/1 \
  -H "Authorization: Bearer test-token"
```

## Error Handling

The API provides comprehensive error responses:

- **400**: Validation errors (missing fields, invalid data types)
- **401**: Unauthorized (missing or invalid token)
- **404**: Resource not found
- **500**: Internal server errors

Example error response:
```json
{
  "error": "Validation Error",
  "message": "Missing required fields: name, description, price, and category are required"
}
```

## Environment Variables

- `PORT`: Server port (default: 3000)

Set environment variables:
```bash
PORT=4000 node server.js
```

## Development Notes

- **In-Memory Storage**: Data is stored in memory and will be lost when the server restarts
- **Demo Authentication**: Current authentication accepts any Bearer token for demonstration
- **Request Logging**: All requests are logged with timestamps to the console
- **UUID Generation**: Product IDs are generated using UUID v4

## Production Considerations

For production deployment, consider implementing:

- **Database Integration**: Replace in-memory storage with a persistent database
- **Real Authentication**: Implement JWT tokens or OAuth
- **Input Sanitization**: Add additional security measures
- **Rate Limiting**: Prevent API abuse
- **CORS Configuration**: Configure cross-origin requests
- **Environment Configuration**: Use environment variables for sensitive data
- **Health Check Endpoints**: Add monitoring endpoints
- **API Documentation**: Implement Swagger/OpenAPI documentation

## License

This project is provided as educational material for learning Express.js and RESTful API development.