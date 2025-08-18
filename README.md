# 🚀 API & FastAPI
Beginner → Advanced
# 1️⃣ API Basics (Before FastAPI)
- API = Application Programming Interface → allows two apps to talk to each other.
- Example: Your app requests data from a weather API → gets JSON response.

## Types of APIs:
- **REST API →** most common, uses HTTP verbs (GET, POST, PUT, DELETE).
- **GraphQL →** flexible querying.
- **SOAP →** older XML-based.
- **gRPC →** high-performance, binary-based.

## HTTP Basics for APIs:
- **Methods:→** GET (read), POST (create), PUT/PATCH (update), DELETE (remove).
- **Status Codes:→** 200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Server Error.
- **Request/Response format:→** JSON is standard.

# 2️⃣ Getting Started with FastAPI

**FastAPI -**
- Super fast (based on Starlette + Pydantic).
- Async support.
- Automatic Swagger & ReDoc documentation.
- Strong typing & validation.

## Install & Hello World
`pip install fastapi uvicorn`
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello FastAPI"}
```
Run:
`uvicorn main:app --reload`
👉 Open http://127.0.0.1:8000/docs → Swagger UI auto generated.
