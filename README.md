# AI Viva Question Module

A FastAPI backend for managing Viva Question Banks.

Teachers can:

- Register and Login using JWT Authentication
- Upload PDF, DOCX, XLSX, PPTX, and CSV files
- Store Question–Answer pairs
- View Question Sets
- Retrieve Questions for Viva
- Provide Answers to the Evaluation Module

---

# Tech Stack

- FastAPI
- SQLAlchemy
- PostgreSQL / SQLite
- Pydantic v2
- JWT Authentication
- Passlib + Bcrypt
- PDFPlumber
- Python-Docx
- OpenPyXL
- Python-PPTX

---

# Project Structure

```text
ai_viva_question_module/
│
├── main.py
├── database.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

---

# Setup Guide

## macOS

### 1. Open Terminal

```bash
cd ai_viva_question_module
```

### 2. Create Virtual Environment

```bash
python3 -m venv venv
```

### 3. Activate Virtual Environment

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

Create a file named:

```text
.env
```

Example:

```env
DATABASE_URL=postgresql://YOUR_USERNAME@localhost:5432/viva_db

SECRET_KEY=your-secret-key

ALGORITHM=HS256

ACCESS_TOKEN_EXPIRE_MINUTES=60
```

### 6. Run FastAPI Server

```bash
uvicorn main:app --reload
```

Open:

```text
http://127.0.0.1:8000/docs
```

---

# Windows Setup

### 1. Open Command Prompt

```cmd
cd ai_viva_question_module
```

### 2. Create Virtual Environment

```cmd
python -m venv venv
```

### 3. Activate Virtual Environment

```cmd
venv\Scripts\activate
```

### 4. Install Dependencies

```cmd
pip install -r requirements.txt
```

### 5. Configure .env

```env
DATABASE_URL=postgresql://postgres:YOUR_PASSWORD@localhost:5432/viva_db

SECRET_KEY=your-secret-key

ALGORITHM=HS256

ACCESS_TOKEN_EXPIRE_MINUTES=60
```

### 6. Run Server

```cmd
uvicorn main:app --reload
```

Open:

```text
http://127.0.0.1:8000/docs
```

---

# PostgreSQL Setup (macOS)

Install PostgreSQL:

```bash
brew install postgresql@18
```

Start PostgreSQL:

```bash
brew services start postgresql@18
```

Open PostgreSQL:

```bash
psql postgres
```

Create Database:

```sql
CREATE DATABASE viva_db;
```

Verify:

```sql
\l
```

Connect:

```sql
\c viva_db
```

Exit:

```sql
\q
```

---

# PostgreSQL Setup (Windows)

1. Download PostgreSQL:

https://www.postgresql.org/download/windows/

2. Install PostgreSQL

3. Open pgAdmin 4

4. Create Database

```text
Databases
 └── Create
      └── Database
           Name: viva_db
```

5. Update .env

```env
DATABASE_URL=postgresql://postgres:YOUR_PASSWORD@localhost:5432/viva_db
```

6. Run Server

```cmd
uvicorn main:app --reload
```

---

# API Endpoints

## Authentication

### Register

```http
POST /auth/register
```

Request:

```json
{
  "name": "Isha",
  "email": "isha@example.com",
  "password": "123456"
}
```

---

### Login

```http
POST /auth/login
```

Request:

```json
{
  "email": "isha@example.com",
  "password": "123456"
}
```

Response:

```json
{
  "access_token": "...",
  "token_type": "bearer"
}
```

---

### Get Current User

```http
GET /auth/me
```

Requires Authorization Token.

---

# Question Routes

## Upload Questions

```http
POST /questions/upload
```

Supports:

- PDF
- DOCX
- XLSX
- PPTX
- CSV

Requirements:

- Minimum 10 Questions
- Maximum 15 Questions
- Maximum File Size 5 MB

---

## Get My Question Sets

```http
GET /questions/my-sets
```

---

## Teacher View

```http
GET /questions/set/{id}/teacher
```

Returns Questions + Answers.

---

## Viva View

```http
GET /questions/set/{id}/viva
```

Returns Questions Only.

---

## Answers View

```http
GET /questions/set/{id}/answers
```

Returns Answer Mapping for Evaluation Module.

---

## Delete Question Set

```http
DELETE /questions/set/{id}
```

---

# Database Tables

## teachers

| Column | Type |
|----------|----------|
| id | Integer |
| name | String |
| email | String |
| hashed_password | String |
| created_at | DateTime |

---

## question_sets

| Column | Type |
|----------|----------|
| id | Integer |
| title | String |
| subject | String |
| original_filename | String |
| teacher_id | Integer |
| created_at | DateTime |

---

## questions

| Column | Type |
|----------|----------|
| id | Integer |
| question_number | Integer |
| question_text | Text |
| answer_text | Text |
| question_set_id | Integer |

---

# Testing

Start FastAPI:

```bash
uvicorn main:app --reload
```

Open:

```text
http://127.0.0.1:8000/docs
```

Test:

1. Register
2. Login
3. Authorize
4. Get Current User
5. Upload Question File
6. Retrieve Question Sets

---

# Troubleshooting

### Uvicorn Not Found

Activate virtual environment:

```bash
source venv/bin/activate
```

Then:

```bash
uvicorn main:app --reload
```

---

### PostgreSQL Connection Refused

Verify PostgreSQL is running:

```bash
brew services list | grep postgresql
```

---

### Missing Tables

Restart FastAPI:

```bash
uvicorn main:app --reload
```

Tables are created automatically.

---

# Author

AI Viva Question Module Team
