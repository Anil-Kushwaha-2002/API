# 🔗 API & RESTful API

## 🔹 What is an API?
- **API (Application Programming Interface)** = A way for two software systems to talk to each other.  
- Works like a **bridge** between client (frontend) and server (backend).  
- Example: Weather app calls weather API → gets temperature data.

---

## 📌 Types of APIs
- **Web API** → Used over HTTP/HTTPS (e.g., REST, GraphQL).  
- **Library/API** → Functions provided by libraries/frameworks.  
- **OS API** → System-level services (e.g., Windows API, POSIX).  

---

## 🔹 What is REST?
- **REST (Representational State Transfer)** = An **architecture style** for designing APIs.  
- RESTful APIs follow rules to make communication simple & scalable.  
- Uses **HTTP methods** for actions.

---

## ⚡ RESTful API Principles
1. **Stateless** → Each request contains all info (no server memory of past requests).  
2. **Client-Server** → Separation of frontend (client) & backend (server).  
3. **Uniform Interface** → Consistent way to access resources.  
4. **Cacheable** → Responses can be cached for speed.  
5. **Layered System** → Can use load balancers, proxies between client & server.  

---

## 🔑 HTTP Methods in REST
- **GET** → Retrieve data.  
- **POST** → Create new data.  
- **PUT** → Update existing data (replace).  
- **PATCH** → Update partially.  
- **DELETE** → Remove data.  

---

## 🛠️ Example REST API (Users)

### URL: `https://api.example.com/users`

```http
GET /users                 → Get all users
GET /users/1               → Get user with id=1
POST /users                → Create new user
PUT /users/1               → Update user with id=1
DELETE /users/1            → Delete user with id=1
```
✅ Benefits of RESTful APIs
- 🌍 Platform independent (works on web, mobile, IoT).
- 📦 Uses lightweight format (JSON).
- 🚀 Fast & scalable.
- 🔗 Widely used across industries.
---
---

# ⚡ FastAPI

## 🔹 What is FastAPI?
- FastAPI = Modern, fast (high-performance) **Python web framework** for building APIs.  
- Built on **Starlette** (for web) + **Pydantic** (for data validation).  
- Auto-generates **API docs** (Swagger & Redoc).  
- Async support → super fast 🚀.  

---

## ✅ Features
- ⚡ Very fast (comparable to Node.js & Go).  
- 📑 Automatic docs (Swagger UI / ReDoc).  
- 🔐 Validation using Pydantic models.  
- 🛠️ Easy async programming with `async`/`await`.  
- 👨‍💻 Great for microservices, REST APIs, ML model serving.  

---

## 🛠️ Installation
```bash
pip install fastapi uvicorn
```
## 📌 Basic Example
```bash
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")  
def read_root():
    return {"message": "Hello, FastAPI!"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```
### Run server:
`uvicorn main:app --reload`

### 🌍 Auto Docs
- Swagger UI → http://127.0.0.1:8000/docs
- Redoc → http://127.0.0.1:8000/redoc

### 🔑 Request Body Example
```bash
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    in_stock: bool = True

@app.post("/items/")
def create_item(item: Item):
    return {"message": "Item created", "item": item}
```

## ⚡ Common Use Cases
- REST APIs & Microservices.
- ML / AI model serving (with TensorFlow, PyTorch, Scikit-Learn).
- Backend for web/mobile apps.
- Async event-driven apps.

## ✅ Benefits of FastAPI
- 🔥 Super fast & easy to learn.
- 📦 Automatic docs.
- 🧪 Built-in validation.
- 🚀 Great async support.

---
---
# 🚀 API & FastAPI
# 1️⃣ API Basics (Before FastAPI)
- API = Application Programming Interface → allows two apps to talk to each other.
- Example: Your app requests data from a weather API → gets JSON response.

## Types of APIs:
- **REST API →** most common, uses HTTP verbs (GET, POST, PUT, DELETE).
- **GraphQL →** flexible querying.
- **SOAP →** older XML-based.
- **gRPC →** high-performance, binary-based.

## HTTP Basics for APIs:
- **Methods:→** `GET` (read), `POST` (create), `PUT/PATCH` (update), `DELETE` (remove).
- **Status Codes:→** `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `500 Internal Server Error`.
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
- `uvicorn main:app --reload`
- 👉 Open http://127.0.0.1:8000/docs → Swagger UI auto generated.

# 3️⃣ Request Handling  
### 🔹 Path Parameters  
Values inside the URL.  
```python
@app.get("/items/{item_id}")
def get_item(item_id: int):
    return {"item_id": item_id}
```
➡️ Example: /items/5 → {"item_id": 5}

### 🔹 Query Parameters
Values after ? in URL.
```python
@app.get("/search/")
def search(q: str, limit: int = 10):
    return {"query": q, "limit": limit}
```
➡️ Example: /search/?q=phone&limit=2

### 🔹 Request Body
Send JSON data with POST/PUT.
```python
from pydantic import BaseModel
class Item(BaseModel):
    name: str
    price: float
    in_stock: bool = True

@app.post("/items/")
def create_item(item: Item):
    return {"item": item}
```
➡️ Example: POST → /items/ with JSON body

# 4️⃣ Response Handling
### 🔹 Custom Response Models
Ensure structured & validated responses.
```python
from typing import List

@app.get("/items/", response_model=List[Item])
def list_items():
    return [
        {"name": "Laptop", "price": 1200.5, "in_stock": True},
        {"name": "Phone", "price": 800.0, "in_stock": False}
    ]
```
### 🔹 Custom Status Codes
Control HTTP status code.
```python
from fastapi import status

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def add_item(item: Item):
    return item
```  
# 5️⃣ Dependency Injection
Re-use common logic (DB, auth, etc.).
```python
from fastapi import Depends

def get_db():
    db = "fake_db_connection"
    try:
        yield db
    finally:
        print("DB closed")

@app.get("/users/")
def get_users(db=Depends(get_db)):
    return {"db": db, "users": ["Alice", "Bob"]}
```
# 6️⃣ Authentication & Security
### 🔹 OAuth2 (with JWT)
```python
from fastapi.security import OAuth2PasswordBearer
from fastapi import Depends

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/profile/")
def read_profile(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```
✅ Real-world: use python-jose to create/verify JWT tokens.

# 7️⃣ Middleware & Background Tasks
### 🔹 Middleware
Run logic before/after each request.
```python
@app.middleware("http")
async def log_requests(request, call_next):
    print("Incoming:", request.url.path)
    return await call_next(request)
```
### 🔹 Background Tasks
Run tasks after response is sent.
```python
from fastapi import BackgroundTasks
def send_email(email: str):
    print(f"Sending email to {email}")

@app.post("/notify/")
def notify(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(send_email, email)
    return {"message": "Email scheduled"}
```
# 8️⃣ Database Integration
- SQLAlchemy (sync, relational DBs)
- Tortoise ORM (async ORM)
- Motor (MongoDB async client)
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
```
# 9️⃣ Advanced Topics
- Async & Await → high performance APIs
- CORS Middleware → allow frontend apps
- File Uploads
```python
from fastapi import File, UploadFile

@app.post("/upload/")
async def upload(file: UploadFile = File(...)):
    return {"filename": file.filename}
```
- WebSockets → real-time apps (chat, live updates)
- Event Handling → startup/shutdown tasks
- Rate Limiting → via third-party libs

# 🔟 Deployment
- Run with Uvicorn + Gunicorn in production
- Containerize with Docker
- Deploy on Heroku, AWS, GCP, Azure, or Render

---
---
📌 Quick Recap

| Feature              | Purpose                          | Example Keyword      |
| -------------------- | -------------------------------- | -------------------- |
| Request Handling     | Get input from user              | Path, Query, Body    |
| Response Handling    | Send structured data             | response\_model      |
| Dependency Injection | Reusable shared logic            | Depends()            |
| Authentication       | Secure endpoints with JWT/OAuth2 | OAuth2PasswordBearer |
| Middleware           | Pre/Post request logic           | @app.middleware      |
| Background Tasks     | Run async jobs after response    | BackgroundTasks      |
| Database             | Store/retrieve data              | SQLAlchemy, ORM      |
| Advanced Topics      | Async, CORS, WebSockets, Uploads | async/await          |
| Deployment           | Run & scale API in production    | Docker, Uvicorn      |

---
---

# REST APIs with Django / Django REST Framework (DRF)
- Install DRF: `pip install djangorestframework`
- Add `rest_framework` in `INSTALLED_APPS`.
### Example: Simple CRUD API
```python
# models.py
from django.db import models
class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)

# serializers.py
from rest_framework import serializers
from .models import Book
class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = '__all__'

# views.py
from rest_framework import viewsets
from .models import Book
from .serializers import BookSerializer
class BookViewSet(viewsets.ModelViewSet):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

# urls.py
from rest_framework.routers import DefaultRouter
from .views import BookViewSet
router = DefaultRouter()
router.register(r'books', BookViewSet)
urlpatterns = router.urls
```
👉 Now you have full CRUD: /books/

# Testing APIs
DRF: APITestCase.
```python
from rest_framework.test import APITestCase
from django.urls import reverse

class BookTests(APITestCase):
    def test_list_books(self):
        url = reverse('book-list')
        response = self.client.get(url)
        self.assertEqual(response.status_code, 200)
```

---
---
# APIs in Odoo
Controllers provide APIs.
```python
from odoo import http
from odoo.http import request

class BookAPI(http.Controller):
    @http.route('/api/books', auth='public', methods=['GET'], type='json')
    def get_books(self):
        books = request.env['library.book'].search([])
        return [{"id": b.id, "name": b.name} for b in books]
```
Odoo also has XML-RPC APIs for integrations.
