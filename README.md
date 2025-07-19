# REST API Store

A simple REST API for managing stores and items built with Flask. This project demonstrates RESTful API design principles, HTTP methods, JSON data handling, and containerized deployment using Docker.

## 🎯 Project Overview

This REST API provides a backend service for managing stores and their inventory items. It includes endpoints for creating, reading, and managing stores and items with proper HTTP status codes and error handling.

## ✨ Features

- **Store Management**: Create and retrieve stores
- **Item Management**: Add and retrieve items associated with stores
- **RESTful Design**: Proper HTTP methods and status codes
- **JSON API**: Clean JSON request/response format
- **Error Handling**: Appropriate error messages and status codes
- **Docker Support**: Containerized deployment with Docker and Docker Compose
- **UUID Generation**: Unique identifiers for stores and items

## 🚀 Quick Start

### Local Development

1. **Clone and navigate to the project:**

```bash
cd REST_API_STORE
```

2. **Install dependencies:**

```bash
pip install -r requirements.txt
```

3. **Run the application:**

```bash
python app.py
```

The API will be available at `http://localhost:8080`

### Docker Deployment

1. **Using Docker Compose (Recommended):**

```bash
docker-compose up --build
```

2. **Using Docker directly:**

```bash
docker build -t rest-api-store .
docker run -p 8080:8080 rest-api-store
```

## 📚 API Documentation

### Store Endpoints

#### Get All Stores

```http
GET /store
```

**Response:**

```json
{
  "stores": [
    {
      "id": "store_uuid",
      "name": "Store Name"
    }
  ]
}
```

#### Create Store

```http
POST /store
Content-Type: application/json

{
  "name": "My Store"
}
```

**Response:**

```json
{
  "id": "generated_uuid",
  "name": "My Store"
}
```

#### Get Single Store

```http
GET /store/{store_id}
```

**Response:**

```json
{
  "id": "store_uuid",
  "name": "Store Name"
}
```

### Item Endpoints

#### Get All Items

```http
GET /item
```

**Response:**

```json
{
  "items": [
    {
      "id": "item_uuid",
      "name": "Item Name",
      "price": 29.99,
      "store_id": "store_uuid"
    }
  ]
}
```

#### Create Item

```http
POST /item
Content-Type: application/json

{
  "name": "New Item",
  "price": 19.99,
  "store_id": "existing_store_uuid"
}
```

**Response:**

```json
{
  "id": "generated_uuid",
  "name": "New Item",
  "price": 19.99,
  "store_id": "existing_store_uuid"
}
```

#### Get Single Item

```http
GET /item/{item_id}
```

**Response:**

```json
{
  "id": "item_uuid",
  "name": "Item Name",
  "price": 29.99,
  "store_id": "store_uuid"
}
```

## 🏗️ Project Structure

```text
REST_API_STORE/
├── app.py                 # Main Flask application
├── db.py                  # In-memory data storage
├── requirements.txt       # Python dependencies
├── Dockerfile            # Docker configuration
├── docker-compose.yml    # Docker Compose setup
├── docker-compose.debug.yml # Debug configuration
├── .flaskenv             # Flask environment variables
└── .gitignore           # Git ignore rules
```

## 🔧 Technical Implementation

### Flask Application Structure

- **app.py**: Main application with route definitions
- **db.py**: Simple in-memory storage using Python dictionaries
- **RESTful Routes**: Proper HTTP method usage (GET, POST)
- **JSON Handling**: Request/response data in JSON format

### Data Storage

```python
# In-memory storage (db.py)
stores = {}  # Store data by UUID
items = {    # Item data with sample items
    1: {"name": "Chair", "price": 10.99},
    2: {"name": "Table", "price": 20.99}
}
```

### Error Handling

- **404 Not Found**: When store or item doesn't exist
- **Proper Status Codes**: HTTP status codes for different scenarios
- **JSON Error Messages**: Consistent error response format

## 📊 API Testing Examples

### Using curl

**Create a store:**

```bash
curl -X POST http://localhost:8080/store \
  -H "Content-Type: application/json" \
  -d '{"name": "Electronics Store"}'
```

**Get all stores:**

```bash
curl http://localhost:8080/store
```

**Create an item:**

```bash
curl -X POST http://localhost:8080/item \
  -H "Content-Type: application/json" \
  -d '{"name": "Laptop", "price": 999.99, "store_id": "your_store_uuid"}'
```

### Using Postman

1. Import the API endpoints
2. Set Content-Type to `application/json`
3. Use the JSON examples provided above

## 🐳 Docker Configuration

### Dockerfile Features

- **Base Image**: Python 3.13
- **Port Exposure**: 8080
- **Working Directory**: /app
- **Flask Installation**: Automatic dependency installation
- **Development Mode**: Flask development server

### Docker Compose Benefits

- **Simplified Deployment**: One-command startup
- **Volume Mounting**: Live code reloading during development
- **Port Mapping**: Automatic port configuration
- **Build Automation**: Automatic image building

## 📚 Learning Objectives

This project demonstrates:

**REST API Design:**

- RESTful routing principles
- HTTP method usage (GET, POST)
- Status code implementation
- JSON API design patterns

**Flask Development:**

- Route definition and handling
- Request/response processing
- Error handling and validation
- Application structure organization

**Docker Containerization:**

- Dockerfile creation and optimization
- Docker Compose orchestration
- Container deployment strategies
- Development vs production configurations

**Data Management:**

- In-memory data storage
- UUID generation for unique identifiers
- Dictionary-based data structures
- Relationship management (stores and items)

## 🚀 Possible Enhancements

### API Features

- **PUT/PATCH Endpoints**: Update existing stores and items
- **DELETE Endpoints**: Remove stores and items
- **Search Functionality**: Filter items by name, price, or store
- **Pagination**: Handle large datasets efficiently
- **Authentication**: User authentication and authorization
- **Validation**: Input validation with detailed error messages

### Data Persistence

- **Database Integration**: PostgreSQL, MongoDB, or SQLite
- **ORM Implementation**: SQLAlchemy for database operations
- **Data Migration**: Database schema management
- **Backup and Recovery**: Data persistence strategies

### Advanced Features

- **API Documentation**: Swagger/OpenAPI integration
- **Testing Suite**: Unit and integration tests
- **Logging**: Comprehensive logging system
- **Monitoring**: Health checks and metrics
- **Rate Limiting**: API usage control
- **CORS Support**: Cross-origin resource sharing

### Deployment

- **Production Configuration**: Gunicorn or uWSGI setup
- **Environment Management**: Development, staging, production
- **CI/CD Pipeline**: Automated testing and deployment
- **Cloud Deployment**: AWS, GCP, or Azure deployment

## 🔍 Error Handling

The API includes proper error handling for common scenarios:

**Store Not Found (404):**

```json
{
  "message": "Store not found"
}
```

**Item Not Found (404):**

```json
{
  "message": "Item not found"
}
```

## 🧪 Testing the API

### Manual Testing Workflow

1. Start the application
2. Create a store using POST /store
3. Note the returned store UUID
4. Create items for that store using POST /item
5. Retrieve stores and items using GET endpoints
6. Test error scenarios with invalid UUIDs

### Automated Testing (Future Enhancement)

Consider adding pytest-based tests for:

- Endpoint functionality
- Error handling
- Data validation
- Integration scenarios

## 🤝 Contributing

Feel free to contribute by:

- Adding new API endpoints
- Improving error handling
- Adding data validation
- Implementing database persistence
- Writing tests
- Improving documentation

## 📝 Notes

- **In-Memory Storage**: Data is lost when application restarts
- **Development Mode**: Currently configured for development use
- **Port Configuration**: Default port is 8080
- **JSON Only**: API only accepts and returns JSON data
- **UUID Identifiers**: All stores and items use UUID for unique identification

---

**A foundational REST API implementation demonstrating Flask web services and containerized deployment**
