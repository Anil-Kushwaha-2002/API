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

###🔹 Query Parameters
Values after ? in URL.
```python
@app.get("/search/")
def search(q: str, limit: int = 10):
    return {"query": q, "limit": limit}
```
➡️ Example: /search/?q=phone&limit=2
###🔹 Request Body
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
###🔹 OAuth2 (with JWT)
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
###🔹 Middleware
Run logic before/after each request.
```python
@app.middleware("http")
async def log_requests(request, call_next):
    print("Incoming:", request.url.path)
    return await call_next(request)
```
###🔹 Background Tasks
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

